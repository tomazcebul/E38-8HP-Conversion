# CANTCU Programming and Calibration

## Scope

This document specifies Race+ backup, programming, configuration, commissioning, validation, and calibration for the E38 740d 8HP70 conversion. Complete [CANTCU Installation](CANTCU-Installation.md) and the applicable [Hardware Installation](HW-Installation.md) checks before commissioning. Use a CANformance-supplied or approved baseline for the identified mechatronics.

> [!WARNING]
> Incorrect transmission profiles, clutch pressures, torque limits, or converter settings can damage the transmission and create unsafe vehicle behavior. Do not copy calibration values from an unrelated 8HP variant.

## Required Information and Equipment

- CANTCU hardware revision `1.9`, serial number `468B`, installed firmware, and matching configuration software
- Exact F10 8HP70 assembly and mechatronics identities
- Exact torque-converter identity
- M67B39 torque characteristics, including any engine modifications
- Dual BMW DDE 4.1 / Bosch EDC15C4 engine-control architecture
- BMW/Bosch identifiers, hardware/software indices, and confirmed master/slave role for both DDE units
- CANformance-approved engine-data, engine-cut, and torque-reduction strategy for the dual-DDE arrangement
- EDC15C4 blip strategy: disabled with stock DDE software, or documented custom software validated on both DDE units
- Selected selector implementation: Option A, BMW F-series 8HP GWS; or Option B, original E38 Steptronic selector with its validated interface
- Brake input source: validated M67 DDE 4.1 CAN signal; exact message, bit, polarity, update rate, and timeout behavior to be recorded
- Differential ratio `2.65`
- Measured tyre rolling circumference
- CANTCU configuration interface and laptop
- CANformance 8HP TCM Tool and verified stock TCM backup
- Race+ software entitlement/version and current installation instructions
- CAN diagnostic interface and logging capability
- Controlled test area and independent data monitoring where required

## DDE 4.1 CAN Interface and Torque Intervention

This section summarizes the transmission interface of the M67 DDE 4.1 (Bosch EDC15C), based on the Bosch software function description *EDC15C B079.CC0* (Y 445 S00 003-CC0, January 2001). The Markdown translation is in the sibling `Bosch-EDC15C/EDC15C-Function-Description` folder: chapter 3.1.8 covers the external quantity intervention, chapter 3.1.12 the active surge damper, and chapter 9 the CAN messages. The messages follow BMW CAN-STAND Rev. 1.5. Treat bit positions and coding values as reference data. Confirm them against the installed DDE software and CANformance documentation, and verify them with a CAN log before relying on them.

### CAN Messages

The DDE evaluates only the following EGS1 signals. It ignores the other EGS1 fields: output speed, oil temperature switches, EGS/SMG type, and transmission torque absorption.

<!-- markdownlint-disable MD060 -->

| Direction | Message | ID | Signals used by DDE / provided to TCU |
| --- | --- | --- | --- |
| TCU → DDE | EGS1 | `0x43F` | `GANG_INF` (bits 0–2, target/current gear), `S_SCHALT` (bit 3, shift active), `S_WK` (bits 6–7, converter lock-up state), `GANG_WHL_ANZ` (bits 8–11, selector position; P/N replaces the clutch switch input `dimKUP`), `MD_IND_GS` (bits 24–31, requested torque relative to `MD_NORM`; `0xFF` = no intervention) |
| DDE → TCU | DDE1 | `0x316` | Terminal 15, engine speed `N_MOT`, driver demand torque `MD_IND`, torque after interventions `MD_IND_NE`, friction torque `MD_REIB`, intervention status `STAT_MD_E`, `F_GE` (1 = transmission intervention not reliably executed: EGS1 timeout or manual gearbox), `F_N_MOT` |
| DDE → TCU | DDE2 | `0x329` | Engine temperature, ambient pressure, accelerator pedal angle `W_FPDK`, kickdown `S_KD`, brake `S_BS`/`F_BS`, cruise status, shiftlock request, and multiplexed `MD_NORM` (torque scale: transmitted value 255 = `MD_NORM`, sent as Nm/16) |
| DDE → cluster | DDE4 | `0x545` | Lamps and fuel consumption; no transmission-control content |
| DSC → DDE | ASC1 | `0x153` | ASR torque reduction and MSR torque increase (see below); sent by the vehicle DSC, not by CANTCU |

<!-- markdownlint-enable MD060 -->

The DDE coding word `cawINF_CAB` enables the CAN interventions. Bit 6 = CAN fitted (enables the intervention), bit 0 = EGS fitted (enables EGS1 failure diagnosis), bit 1 = ASC fitted. With an automatic transmission and ASC, use `0x43` or `0x67`. The E38 740d already runs an automatic transmission, so the existing coding is expected to suit CANTCU. Confirm it by reading both DDEs.

CANTCU CAN3 connects only to the master DDE, as the original AGS did. In the OEM wiring the master is the only DDE on the AGS and vehicle CAN. The slave DDE's only CAN connection is the private CANP link to the master (see [Engine-Control CAN Topology](CANTCU-Installation.md#engine-control-can-topology)). The master therefore receives EGS1, processes the torque request, and passes the result to the slave over CANP, as it did with the original AGS. The CANP message content is not documented. During commissioning, confirm from logs that a torque reduction affects both cylinder banks equally.

### Engine Response to Torque-Reduction Requests

1. The DDE converts `MD_IND_GS` (`mroMD_EGS`) into a fuel quantity (`mroM_EXGS`) using the specific-consumption map `mrwKFVB_KF` (engine speed and torque).
2. It takes the minimum of the driver demand (pedal/cruise), EGS, ASR and transfer-case requests. It then compares this minimum with the MSR request from DSC and uses the higher value. **An EGS request can only reduce fuel.** A request above the driver demand has no effect.
3. The resulting quantity passes through the active surge damper (ARD):
   - During an external intervention, the ARD switches to dedicated CAN parameter sets (`mrwFFCan…`, `mrwDSCAN…`, `mrwPSCAN…`). These have separate settings for falling and rising quantity, so the torque cut-in and the torque restore are filtered by the DDE calibration and are not instantaneous.
   - When `S_SCHALT` = `mrwARDS_I` or `S_WK` = `mrwARDWK_I`, the ARD disturbance controller is initialized. When `S_SCHALT` = `mrwARDS_L` or `S_WK` = `mrwARDWK_L`, the ARD can switch to idle mode.
   - `GANG_INF` selects the gear-dependent ARD parameter sets.
   - These functions apply only when there is no CAN fault and EGS1 is present.
4. DDE1 reports back `MD_IND`, `MD_IND_NE` and `STAT_MD_E`. The torque reduction actually achieved is `MD_IND` − `MD_IND_NE`. If `F_GE` = 1, the DDE has rejected the intervention.

If EGS1 is lost, the DDE stores `fbeEEGS_F`, sets `F_GE`, and stops accepting EGS interventions. It also replaces the driver demand with a substitute quantity (`mroM_EEGS`):

- below `mrwV_ANFAH`: the drive-off curve `mrwANFAHKL`
- above `mrwV_ANFAH`: a ramp at `mrwEGSRAMP` up to `mrwM_EGSMX`

The car remains driveable, but with limited power, until EGS1 is present again.

CANTCU requirements:

- Send EGS1 continuously, at the OEM rate, from ignition on.
- Hold `MD_IND_GS` at `0xFF` except during an active reduction.
- Scale reduction requests against the received `MD_NORM`.
- Drive `S_SCHALT`, `GANG_INF`, `S_WK` and `GANG_WHL_ANZ` from confirmed transmission state.

### Upshifts and Downshifts Without Engine Blips

The stock EDC15C software has no EGS torque-increase path. Upshifts work as designed: the torque reduction covers the clutch handover. Downshifts depend on load:

<!-- markdownlint-disable MD060 -->

| Downshift type | Behaviour without a blip | Severity |
| --- | --- | --- |
| Power-on / kickdown | The engine's own torque raises the input speed once the off-going clutch releases. A torque reduction near synchronous speed prevents flare. | Normal |
| Coast / braking (pedal released, overrun fuel cut) | The on-coming clutch must drag the engine to the higher speed using vehicle inertia. Expect a deceleration jolt or clunk, longer shift time, and more clutch heat and wear. The large M67 rotating inertia makes this worse. | Main concern |
| Multi-gear coast skips (e.g. 7→4) and high-rpm manual downshifts | Largest rpm jump, so the strongest jolt and the most clutch work. Most noticeable in Sport and manual modes. | Highest |
| Low-speed coast (3→2→1) | Small rpm jump near idle, partly helped by the idle speed controller. | Usually acceptable |

<!-- markdownlint-enable MD060 -->

Compensate in the CANTCU/Race+ calibration rather than in the engine:

1. Use a softer on-coming clutch pressure ramp and a longer overlap on coast downshifts, so the clutch accelerates the engine progressively.
2. Open, or allow controlled slip of, the converter lock-up clutch during coast downshifts so the converter fluid absorbs the speed step.
3. Move coast-downshift points to lower speeds, so each shift starts from a lower rpm and the rpm step is smaller.
4. Shift sequentially on coast; avoid skip-downshifts.
5. Limit manual and paddle downshifts by a maximum resulting engine speed, and reject or delay requests above it.
6. On power-on downshifts, let engine torque raise the input speed and use `MD_IND_GS` only to prevent flare near synchronous speed.

The DDE does accept a torque increase through the DSC MSR request in ASC1 `0x153`. The request is valid when `B_MSR` = 1, `B_ASC` = 0 and `MD_IND_MSR` ≠ 0, and it has priority over the EGS intervention. Do not use this path as a blip substitute:

- The vehicle DSC already transmits `0x153`. Injecting it would need a gateway that rewrites DSC traffic, which CANTCU firmware is not known to support.
- The DDE checks the request's plausibility and ramps it out if invalid (`mrwS_MDASC`/`ASC_ALIVE`, `mrwMSRRAMP`), and the ARD filters it.
- An MSR request would pass from the master to the slave over the undocumented CANP link, so the response of the second bank is unverified.
- An injected or stuck MSR frame produces unintended engine torque.

The only supported blip route remains validated custom software on both DDE units (see below).

## 1. Back Up and Install Race+

1. Record the installed firmware and configuration-software versions.
2. Read and save the controller's existing configuration before changing it.
3. Connect the transmission using the completed Race+ CAN1, power, ground, and WUP wiring and a stable power supply.
4. Use the CANformance 8HP TCM Tool to identify the TCM and create a stock backup before programming Race+.
5. Verify that the backup is readable, preserve an immutable copy, and record its checksum, tool version, date, and transmission identity.
6. Confirm Race+ support, entitlement, and the programming procedure for the exact 8HP70 mechatronics.
7. Program Race+ with the 8HP TCM Tool and save the programming report.
8. After Race+ is installed, configure its settings through CANTCU Configurator.
9. Use dated, immutable copies for each tested CANTCU/Race+ configuration.
10. Record the transmission, converter, tyre, differential, and vehicle details with the configuration.
11. Define and document the approved rollback procedure before first startup.

Do not interrupt TCM programming or improvise a recovery procedure. Maintain the power supply and communications required by the current 8HP TCM Tool instructions. Do not update unrelated CANTCU firmware solely because a newer version exists; confirm hardware revision support, migration requirements, and Race+ compatibility first.

## 2. Configure the Base Parameters

Verify every item against the exact firmware documentation:

- Exact transmission and mechatronics profile
- Engine cylinder count and RPM source
- Tyre rolling circumference
- Differential ratio
- Input- and output-speed scaling
- Selector type and direction logic
- Selector firmware profile and CAN-bus assignment
- Brake input polarity
- Reverse and Park/Neutral output behavior
- Option B B1/DOUT1 shift-lock composite command, including OEM P/N, brake, road-speed, engine-speed, approximately 0.5 s timing, Y19 polarity, relay-contact selection, and missing-data behavior
- Engine torque model, torque limits, and torque-reduction strategy
- Engine-cut behavior and dual-DDE arbitration
- Throttle blips disabled for the stock EDC15C4 DDEs
- CAN bitrate, receive messages, transmit messages, and termination setting
- Manual mode, paddle, and mode-switch behavior
- Maximum transmission temperature and protection behavior

Confirm that calculated road speed agrees with an independent measured speed. Incorrect tyre or final-drive scaling can corrupt shift scheduling and protection logic.

## 3. Establish a Conservative Calibration

Start with a CANformance-approved Race+ baseline for the exact mechatronics and the closest supported vehicle characteristics. Initially use conservative engine torque limits and prohibit full-load operation.

Review these calibration groups:

- Drive and Sport shift schedules
- Upshift and downshift hysteresis
- Downshift strategy without native engine blips (see [Upshifts and Downshifts Without Engine Blips](#upshifts-and-downshifts-without-engine-blips))
- Kickdown behavior
- Clutch fill and shift-pressure settings
- Shift timing and overlap
- Converter lock-up enable conditions and slip target
- Coast-downshift behavior
- Manual-mode limits and automatic interventions
- Temperature, speed, and pressure protection behavior

Change one related group at a time, assign a new configuration version, and record the reason. Pressure should not be used to conceal an incorrect transmission profile, missing torque reduction, mechanical fault, or adaptation problem.

CANformance marks EDC15 blips as conditional on ECU-specific custom software rather than native support. Use a no-blip baseline with the stock M67 DDE 4.1 / EDC15C4 software. Do not enable or test blip requests unless the custom software is identified and archived for both DDE units, its master/slave behavior is documented, and CANformance approves the integration. A custom change to only one DDE is not an accepted configuration.

## 4. Verify Live Data Before Startup

With ignition on and the engine stopped, confirm that these values are present and plausible:

- Engine speed is zero
- Throttle or calculated load tracks pedal input
- Brake status changes correctly
- Selector position and direction are correct
- Selected selector interface online/valid status and indication are correct
- Input and output speeds are zero
- Transmission temperature is plausible
- Wheel speed is zero and all wheel-speed sources agree
- Park/Neutral and reverse outputs follow the intended state

Resolve missing, stale, incorrectly scaled, or inverted values before starting the engine.

## 5. Static Commissioning

With the driven wheels safely raised and the area clear:

1. Confirm CANTCU powers up and communicates with the transmission.
2. Verify engine speed, throttle/load, brake, selector, input speed, output speed, and temperature again.
3. Confirm Park and Neutral logic before starting the engine.
4. Start the engine and immediately inspect for abnormal noise, vibration, leaks, or converter/flexplate runout.
5. Apply the brake and select each position briefly, confirming correct engagement and displayed state.
6. Verify reverse lights and the Park/Neutral start interlock.
7. Run the wheels only at low speed and confirm output speed, wheel speed, shift direction, and brake operation.
8. Recheck fluid level using the specified ZF temperature procedure.
9. Save the complete first-start log and fault report.

Stop immediately for harsh engagement, no drive, unexpected wheel movement, abnormal pressure or temperature data, noise, vibration, or leaks.

## 6. Controlled Road Testing

Perform initial tests in a closed, low-risk area with diagnostic logging active.

1. Confirm forward and reverse engagement at idle.
2. Test light-throttle upshifts and downshifts at low speed.
3. Compare road speed, engine speed, input speed, output speed, selected gear, commanded gear, converter slip, and transmission temperature.
4. Confirm converter lock-up only after basic shifts are correct.
5. Test manual selection, kickdown, coast downshifts, and braking behavior progressively using the approved no-blip strategy.
6. Increase load in small steps and review each log before continuing.
7. Stop and inspect mounts, adapter, fasteners, driveshaft, cooler lines, wiring, fluid level, and leaks.

Do not begin full-load testing until shift quality, torque reduction, clutch slip, temperatures, and driveline vibration have been reviewed by a competent calibrator.

## 7. Calibration Workflow

For each issue, preserve the log and classify it before changing parameters:

1. Check for mechanical faults, incorrect fluid level, temperature problems, and active diagnostic codes.
2. Confirm that the selected transmission profile and all input data are correct.
3. Compare commanded gear, actual ratio, input/output speed, engine torque, torque reduction or cut state, blip request state, converter state, and clutch slip.
4. Change the smallest relevant parameter set.
5. Repeat the same controlled test conditions.
6. Accept the change only when logs improve without creating faults elsewhere.

Evaluate shift duration and firmness together with thermal response, clutch slip, torque reduction, and driveline shock. A shorter or firmer shift is not evidence of acceptable calibration without supporting log data.

## Programming and Calibration Acceptance Checklist

- [ ] Firmware and configuration-software versions recorded
- [ ] Stock TCM backup created and verified before Race+ programming
- [ ] 8HP TCM Tool version, Race+ version/entitlement, and programming report archived
- [ ] Approved TCM rollback procedure documented
- [ ] Original, base, and final configurations archived
- [ ] Exact transmission/mechatronics profile confirmed
- [ ] Differential and tyre scaling verified against measured speed
- [ ] All required live inputs are plausible and stable
- [ ] Selector, brake, reverse, and Park/Neutral logic verified
- [ ] Selector loss-of-communication or electrical-fault behavior verified
- [ ] Conservative torque, shift, and lock-up calibration installed
- [ ] Stock-EDC15C4 blip requests disabled, or validated custom software recorded for both DDEs
- [ ] EGS1 `0x43F` transmitted continuously; no `fbeEEGS_F` and `F_GE` = 0 in both DDEs
- [ ] Torque reduction verified from DDE1 `MD_IND` − `MD_IND_NE` on both cylinder banks
- [ ] Coast-downshift and manual-downshift quality accepted without blips
- [ ] Static commissioning completed without faults
- [ ] Light-load shift behavior validated by logs
- [ ] Converter slip and lock-up behavior validated
- [ ] Temperature protection checked
- [ ] No unexplained clutch slip or ratio errors
- [ ] Progressive-load and final validation logs archived

## Software and Calibration Record

<!-- markdownlint-disable MD060 -->

| Item | Value/file |
| --- | --- |
| CANTCU firmware |  |
| Configuration software |  |
| 8HP TCM Tool version |  |
| Stock TCM backup/checksum |  |
| Race+ software version/entitlement |  |
| Race+ programming report |  |
| TCM rollback procedure |  |
| Original configuration |  |
| Base configuration |  |
| Final configuration |  |
| Transmission assembly | BMW `24 00 7 642 542`, GA8HP70Z-WTT, ZF serial `0257888` |
| Mechatronics identity | To be recorded |
| Torque-converter identity | ZF number `1087 322 397`; production year 2013; stamped trace strings `1087322397 8639`, `250700004399`, `3 201311204001`, and `V172`; application and BMW service part number to be confirmed |
| Transmission profile | Race+ / exact 8HP70 profile to be recorded |
| Selected selector option | Option A: BMW F-series 8HP GWS / Option B: original E38 Steptronic selector |
| Selector type/profile and BMW part number | Option A baseline: BMW F-series 8HP GWS `61 31 9 296 898`; Option B: E38 S227/S224 direct contacts with Universal DIN/CAN Shifter |
| Selector input map or CAN assignment |  |
| Option B S224 logic | Maintained manual gate; momentary strike-up/down accepted only in manual mode; physical direction and single-request debounce to be recorded |
| Pedal demand/kickdown strategy | Preferred: validated DDE4.1 CAN pedal position/driver demand; record 0-100% scaling and full-pedal downshift calibration |
| Optional external kickdown | C6/DIN4 using the reterminated former X70003 pin 17 conductor only if CANformance approves `Kickdown Active`; otherwise leave C6 unused |
| Option B conditioner implementation | Separate four-channel conditioner / modified E82 5 V LED module |
| Option B 5 V supply and channel values | Record regulator/protection, worst-case output, LED/resistor, pull-up, protection resistor, contact current, and C7 current |
| Option B AIN open/closed voltages and thresholds |  |
| Option B no-range, multiple-range, and short-to-ground behavior |  |
| Brake CAN message/bit/polarity/timeout |  |
| Option B shift-lock output | B1/DOUT1; record the CANformance-confirmed composite release-command source and output mode |
| Y19 polarity/current and relay contacts | Record powered-to-lock/release result, steady-state/inrush current, and NO/NC contact selection |
| Shift-lock OEM conditions | P/N position, brake status/plausibility, road-speed threshold, engine-running threshold, and approximately 0.5 s timing |
| Shift-lock delay/startup/fault behavior | Record the OEM-defined delay transition; startup pulse disabled; release request inactive for missing, stale, or implausible required data |
| CAN definition/version |  |
| Wiring reference | Current CANformance Race+ installation; legacy `cantcu_8hp_wiring_v15.pdf` retained only as a compatibility/conductor-size reference |
| Engine-control architecture | Dual BMW DDE 4.1 / Bosch EDC15C4, master/slave over CANP |
| CAN3 engine-control connection | Reused former AGS pair: X70004 pin 37 to master DDE X2412 pin 3 = CAN-Low; X70004 pin 36 to X2412 pin 4 = CAN-High |
| `DDE41KRO` BMW/Bosch label numbers |  |
| `DDE41KRO` hardware/software index and role |  |
| `DDE41KLO` BMW/Bosch label numbers |  |
| `DDE41KLO` hardware/software index and role |  |
| Dual-DDE torque-reduction strategy |  |
| DDE `cawINF_CAB` coding (both DDEs) | Expected `0x43` or `0x67`; record read-out values |
| EGS1 `0x43F` rate and `MD_IND_GS` scaling | Record transmit period and `MD_NORM` value received in DDE2 |
| Dual-DDE engine-cut strategy |  |
| Throttle-blip strategy | Disabled for stock EDC15C4 software |
| Custom blip-software supplier/version | Not applicable unless installed on both DDEs |
| Tyre circumference |  |
| Differential ratio | 2.65 |
| First-start log |  |
| Static commissioning report |  |
| Final validation log |  |

<!-- markdownlint-enable MD060 -->

## References

- Current CANTCU firmware, configuration, and calibration documentation
- [CANformance Race+ overview](https://wiki.canformance.net/CANTCU/software/race-plus)
- [CANformance Race+ installation](https://wiki.canformance.net/CANTCU/software/race-plus/installation)
- [CANformance Race+ configuration](https://wiki.canformance.net/CANTCU/software/race-plus/configuration)
- [CANformance 8HP TCM Tool](https://wiki.canformance.net/CANTCU/software/8hp-tcm-tool)
- [CANformance supported ECUs](https://wiki.canformance.net/CANTCU/integrations/supportedECUs) - EDC15 blips require ECU-specific custom software
- CANformance-approved base calibration for the exact F10 8HP70 mechatronics
- BMW and ZF service information for the identified F10 8HP70 assembly
- BMW E38 and M67 diagnostic information
- Bosch *Software Function Description EDC15C B079.CC0* (Y 445 S00 003-CC0, BMW, January 2001): chapter 3.1.8 External quantity intervention, chapter 3.1.12 Active surge damper, chapter 9 CAN functions; English Markdown translation in `Bosch-EDC15C/EDC15C-Function-Description/en`
- [BMW Service Training: Diesel Engines M57/M67 Common Rail](https://pdfcoffee.com/m57enpdf-pdf-free.html)
