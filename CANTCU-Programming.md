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
- Differential ratio `2.65`
- Measured tyre rolling circumference
- CANTCU configuration interface and laptop
- CANformance 8HP TCM Tool and verified stock TCM backup
- Race+ software entitlement/version and current installation instructions
- CAN diagnostic interface and logging capability
- Controlled test area and independent data monitoring where required

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
- Downshift strategy without native engine blips
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
- F-series GWS online status and indication are correct
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
| Selector type/profile and BMW part number | BMW F-series 8HP GWS `61 31 9 296 898`; exact CANTCU profile to be confirmed |
| Selector input map or CAN assignment |  |
| CAN definition/version |  |
| Wiring reference | Current CANformance Race+ installation; legacy `cantcu_8hp_wiring_v15.pdf` retained only as a compatibility/conductor-size reference |
| Engine-control architecture | Dual BMW DDE 4.1 / Bosch EDC15C4, master/slave over CANP |
| CAN3 engine-control connection | Reused former AGS pair: X70004 pin 37 to master DDE X2412 pin 3 = CAN-Low; X70004 pin 36 to X2412 pin 4 = CAN-High |
| `DDE41KRO` BMW/Bosch label numbers |  |
| `DDE41KRO` hardware/software index and role |  |
| `DDE41KLO` BMW/Bosch label numbers |  |
| `DDE41KLO` hardware/software index and role |  |
| Dual-DDE torque-reduction strategy |  |
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
- [BMW Service Training: Diesel Engines M57/M67 Common Rail](https://pdfcoffee.com/m57enpdf-pdf-free.html)
