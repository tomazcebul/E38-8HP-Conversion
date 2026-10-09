# E38 Selector Integration

This document defines project selector **Option B**, which retains the original E38 Steptronic selector with CANTCU Race+. Project **Option A** remains BMW F-series 8HP GWS `61 31 9 296 898` as described in [CANTCU Installation](CANTCU-Installation.md).

Option B uses the console-mounted S227 selector-lever-position contacts that originally drove the E82 gear-indicator light, plus the S224 Steptronic contacts. It does not use the Bowden cable, transmission-mounted S8532 switch, or coded L1-L4 signals.

> [!IMPORTANT]
> This design is electrically plausible and fits the available CANTCU inputs, but it remains conditional on measurements of the actual S227 and S224 assemblies and written CANformance confirmation of the input configuration and conflicting-input behavior. Do not commission it from the diagram alone.

## Signal Architecture

The BMW wiring diagram shows S227 as four individual contacts with a common return:

- E82/X1599 pin 2: selector position P
- E82/X1599 pin 3: selector position R
- E82/X1599 pin 4: selector position N
- E82/X1599 pin 5: selector position D
- E82/X1599 pin 1: terminal 31/common return

The S224 Steptronic switch has three active-ground contacts with a common return:

- S224/X1561 pin 2: strike-down/downshift
- S224/X1561 pin 3: strike-up/upshift
- S224/X1561 pin 4: maintained manual-gate contact
- S224/X1561 pin 1: terminal 31/common return

The manual-gate contact closes when the lever moves from the automatic gate into the manual gate and remains closed there. Moving the lever forward or backward additionally closes one momentary strike contact while the manual-gate contact remains closed. Verify on the actual selector which physical direction closes pin 2 and pin 3 before assigning driver-facing `+` and `-` labels; do not infer direction from the words forward and backward alone.

The original AGS is removed. Reuse suitable original selector conductors by identifying them end-to-end at the disconnected A7000 harness plugs, verifying that they have no hidden branches, and fitting the correct CANTCU terminals or approved sealed splices. Isolate abandoned connector terminals and any remaining E82 or vehicle-voltage branches before repurposing the conductors. Do not parallel an unverified E82 signal onto CANTCU: the four CANTCU analog inputs are limited to `0-5 V`, and the four digital inputs may connect only to ground.

The selected CANTCU profile is CANformance `Universal DIN/CAN Shifter`. CANformance documents P, R, N, and D buttons through analog inputs configured as `AIN to DIN`, while its four digital inputs accept ground-switching functions. This permits the following complete allocation:

<!-- markdownlint-disable MD060 -->

| Function | Original contact | CANTCU pin/mode | Required electrical behavior |
| --- | --- | --- | --- |
| P | E82/X1599 pin 2 | B2 / AIN1, `AIN to DIN`, `Shifter P` | Defined 0-5 V signal; active when S227 grounds the P contact |
| R | E82/X1599 pin 3 | B3 / AIN2, `AIN to DIN`, `Shifter R` | Defined 0-5 V signal; active when S227 grounds the R contact |
| N | E82/X1599 pin 4 | B4 / AIN3, `AIN to DIN`, `Shifter N` | Defined 0-5 V signal; active when S227 grounds the N contact |
| D | E82/X1599 pin 5 | B5 / AIN4, `AIN to DIN`, `Shifter D` | Defined 0-5 V signal; active when S227 grounds the D contact |
| S227 common | E82/X1599 pin 1 | C7 sensor ground | Dedicated selector return after isolation from E82 |
| Manual gate | S224/X1561 pin 4 | B6 / DIN1, `Shifter Mode` | Maintained active-ground contact throughout manual-gate operation |
| Strike-down/downshift | S224/X1561 pin 2 | B7 / DIN2, `Shifter Gear Down` | Momentary active-ground contact; valid only while manual-gate contact is closed |
| Strike-up/upshift | S224/X1561 pin 3 | C5 / DIN3, `Shifter Gear Up` | Momentary active-ground contact; valid only while manual-gate contact is closed |
| S224 common | S224/X1561 pin 1 | C7 sensor ground | Dedicated selector return after isolation from original ground/loads |
| Brake | M67 DDE 4.1 brake-status CAN signal | DDE/CAN input to CANTCU | Use the validated DDE4.1 CAN brake signal; do not add a raw E38 12 V brake wire to the selector interface |
| Kickdown | Pedal position/driver demand through the validated DDE4.1 CAN integration | CANTCU CAN input | Preferred implementation; the 8HP does not require a dedicated hardwired kick-down switch |
| Optional external kickdown | Former X70003 pin 17 conductor from the original kick-down switch | C6 / DIN4, `Kickdown Active` | Leave disconnected unless CANformance confirms that a separate external request is required or deliberately retained |

<!-- markdownlint-enable MD060 -->

## PRND Input Conditioning

An open S227 contact must not leave an analog input floating. Two implementations are possible: four separate automotive-rated conditioning channels, or a verified modification of the E82 gear-indicator module that combines the indicator LEDs and conditioning network.

### Modified E82 Gear-Indicator Module

The E82 module can be a practical interface if the original P/R/N/D bulb circuits are fully isolated from every 12 V feed and rebuilt as four identical 5 V channels. Replacing each bulb with an LED and series resistor is not sufficient by itself: an LED is nonlinear and does not provide a defined pull-up at the CANTCU analog-input leakage current. Each channel requires a separate linear pull-up:

```text
protected +5 V ---- R_LED ---- LED ----+---- S227 contact ---- CANTCU C7
                                       |
protected +5 V ---- R_PULLUP ----------+---- R_PROTECT ------- CANTCU AIN
```

With the contact open, `R_PULLUP` must hold the AIN at a stable inactive high level and the LED must be off. With the contact closed, the AIN must be pulled near C7, the corresponding LED must illuminate, and the combined LED and pull-up current must remain within the S227 contact and C7 current limits. Provide one independent channel for P, R, N, and D.

Use a fused, automotive-rated 12 V-to-5 V supply with reverse-polarity, load-dump/transient, crank-voltage, thermal, and output-overvoltage protection. Its worst-case output, including tolerance, ripple, startup, shutdown, and faults, must never exceed the CANTCU AIN `0-5 V` limit. Do not use CANTCU C2 to power the indicator LEDs unless CANformance confirms its available current and permits that load. Reference the conditioner to C7 only through a CANformance-approved grounding arrangement; do not inject unrelated module or illumination current into the sensor-ground circuit.

Select each LED resistor from the measured LED forward voltage and required brightness, and select each pull-up from the measured CANTCU AIN impedance, configured thresholds, and required S227 wetting current. The original bulb contacts may require more wetting current than a low-current LED circuit provides. Verify reliable switching after oxidation, vibration, temperature cycling, and repeated slow lever movement. Use `R_PROTECT` and approved clamps or buffering where required so a regulator or wiring fault cannot apply destructive current or more than 5 V to B2-B5.

Before connecting CANTCU, inspect and map the E82 circuit board and prove that the modified PRND nodes have no continuity to terminal R, terminal 58g, the general-module load-shed signal, any abandoned AGS-bound trace or conductor, chassis voltage, or any remaining 12 V lamp circuit. Retain the original panel illumination only if it is electrically isolated from all four 5 V signal nodes under normal and single-fault conditions.

The modified LEDs indicate lever-contact state, not confirmed transmission state. They may be retained as a local selector-position display, but EWS authorization, reverse lamps, and any final gear indication must continue to use confirmed CANTCU/transmission state.

### Separate Conditioner Alternative

If the E82 board cannot be fully isolated or the contact wetting-current requirement cannot be met, disconnect X1599 from E82 and use four separate conditioning channels:

```text
approved +5 V -- approved pull-up/conditioning --+-- CANTCU AIN
                                                  |
                                                  +-- S227 contact -- CANTCU C7
```

For either implementation, each open contact must produce a stable inactive voltage within the configured `AIN to DIN` range and each closed contact must produce a stable active voltage near C7. Do not apply vehicle voltage to B2-B5 and do not assume CANTCU provides a suitable internal analog-input pull-up.

## Contact Truth Table

The drawing implies a one-hot ground-switching arrangement, but the actual selector must establish the final truth table.

<!-- markdownlint-disable MD060 -->

| Lever detent | P contact | R contact | N contact | D contact | Required interpretation |
| --- | ---: | ---: | ---: | ---: | --- |
| P | Closed | Open | Open | Open | `Shifter P` |
| R | Open | Closed | Open | Open | `Shifter R` |
| N | Open | Open | Closed | Open | `Shifter N` |
| D/automatic gate | Open | Open | Open | Closed | `Shifter D` |
| Manual gate | Open | Open | Open | Verify D remains closed | `Shifter D` plus `Shifter Mode` |
| Between detents/invalid | Measured result | Measured result | Measured result | Measured result | No new range request |

<!-- markdownlint-enable MD060 -->

Confirm whether D remains asserted when the lever moves sideways into the manual gate. If it does not, obtain CANformance approval for the required mode-entry sequence before using this design.

## Steptronic Contact Truth Table

<!-- markdownlint-disable MD060 -->

| Selector action | Manual gate, pin 4 | Strike-down, pin 2 | Strike-up, pin 3 | Required interpretation |
| --- | ---: | ---: | ---: | --- |
| Automatic gate | Open | Open | Open | Automatic mode; no manual request |
| Manual gate, centred | Closed | Open | Open | Manual mode maintained |
| Downshift strike | Closed | Closed | Open | One downshift request |
| Upshift strike | Closed | Open | Closed | One upshift request |
| Either strike outside manual gate | Open | Closed | Closed/Open | Invalid; no shift request |
| Both strike contacts closed | Closed/Open | Closed | Closed | Invalid; no shift request |

<!-- markdownlint-enable MD060 -->

The strike contact is additional to the maintained manual-gate contact, not an alternative to it. Configure or externally gate the inputs so Race+ accepts `Shifter Gear Up` and `Shifter Gear Down` only while `Shifter Mode` is active. Each strike must create one request per transition; a held, bouncing, or shorted contact must not repeat shifts. If the installed Race+ Universal Shifter profile does not enforce this relationship, obtain a CANformance-approved interlock or conditioning circuit before commissioning.

## Safety and Fault Behavior

Direct contacts eliminate the Bowden mechanism and L1-L4 decoder, but they do not provide an independent validity bit or rolling counter. Before accepting Option B, obtain CANformance confirmation of:

1. How Universal Shifter handles no asserted range, multiple asserted ranges, and a range input that remains asserted because of a short to ground.
2. Whether a new R or D request is inhibited when the brake condition, vehicle speed, or current transmission state makes it unsafe.
3. Whether P should be configured and how Park requests are handled by this 8HP/Race+ combination.
4. The input threshold, hysteresis, filtering, and debounce to use for each `AIN to DIN` channel.
5. Confirmation that `Shifter Mode` is configured as a maintained state and gates both momentary strike inputs.
6. How the profile handles an up/down strike outside manual mode, both strike contacts active, a held strike, and contact bounce.
7. The exact DDE4.1 CAN brake-status message, polarity, timeout, and behavior when the CAN signal is missing or implausible.
8. Whether the validated DDE4.1 integration provides sufficient pedal-position/driver-demand data for Race+ kickdown behavior without a separate `Kickdown Active` input.
9. If an external request is retained, the former X70003 pin 17 conductor route, switch polarity, active state, debounce, retermination, and supported CANTCU `Kickdown Active` mapping.

Use confirmed transmission state, not the lever contacts alone, for EWS Park/Neutral start authorization, reverse lamps, and final gear indication.

## Shift Lock

Retain the E38 Y19 shift-lock solenoid and mechanical emergency release. The project assignment is **B1/DOUT1** for the shift-lock relay command. B1 is a low-side, ground-switching output with a maximum load of `0.5 A`; do not connect Y19 directly if either its steady-state or inrush current exceeds that limit. In that case B1 must drive only an automotive relay coil or protected driver whose own steady-state and inrush current remain below `0.5 A`.

The current planning values for Y19 are:

| Parameter | Planning value | Design implication |
| --- | ---: | --- |
| Energized current | `0.5-1.0 A` | Exceeds or approaches the CANTCU B1/DOUT1 rating; do not drive Y19 directly |
| Inrush current | `1.5-2.0 A` for a few milliseconds | Relay contacts, fuse, wiring, and suppression must tolerate the measured peak |
| Coil resistance | `12-24 ohm` | Check the measured cold and hot resistance against the expected supply voltage and current |

Treat these as planning values until the installed solenoid is measured. A nominal `12-24 ohm` coil at approximately `12 V` is consistent with roughly `0.5-1.0 A`, but resistance alone does not establish the inrush profile or the powered-to-lock/release behavior.

Before selecting relay contacts or output polarity, bench-test Y19 and record:

- steady-state and inrush current;
- whether energizing Y19 locks or releases the lever;
- which X1178 terminal is the supply and which is the controlled return; and
- the mechanical state after loss of Y19 power.

The BMW drawing identifies X1178 pin 1 as the positive supply and pin 3 as the P/N lockout-magnet connection, but both originally terminate at the AGS. Do not permanently connect either conductor to battery or ground until measurements confirm the required polarity.

### Relay Interface

Wire the relay coil as follows:

```text
fused switched +12 V ---- relay coil 86
B1 / DOUT1 -------------- relay coil 85
flyback diode cathode ---- coil 86
flyback diode anode ------ coil 85
```

Size the relay contacts, wiring, fuse, and suppression for the measured Y19 inrush current. Keep the relay-coil fuse and Y19-load fuse appropriately separated. Add suitable suppression for Y19 without delaying release beyond the validated limit.

Select a relay or protected high-current driver with:

- a relay-coil steady-state and turn-on current comfortably below `0.5 A` at the lowest specified supply voltage;
- contact ratings with engineering margin above the measured Y19 steady-state and inrush current;
- an automotive coil and contact rating suitable for the measured load-dump, crank, temperature, and vibration environment; and
- coil suppression that does not cause B1 to exceed its voltage or current limits.

Do not use a relay whose coil is itself close to the `0.5 A` CANTCU output limit. Record the actual coil resistance/current, contact rating, fuse rating, flyback or transient-suppression part, and loaded B1 voltage during acceptance testing.

Define **B1 active** as a *release request*. Select the relay contact so B1 inactive retains the locked state whenever the ignition-fed shift-lock supply is available:

- If Y19 is **powered to release**, switch its supply through a normally-open contact.
- If Y19 is **powered to lock**, switch its supply through a normally-closed contact so energizing the B1 relay opens the Y19 circuit.

This contact choice must follow the bench result; do not assume either Y19 polarity from the diagram. Record and test the resulting behavior for CANTCU power loss, relay-coil open/short circuit, welded contacts, Y19 power loss, and complete vehicle power loss. Retain the mechanical emergency release because no electrical design can keep an energized lock active after total power loss.

### CANTCU Output Configuration

The original E38 shift-lock function evaluates:

- selector position P or N;
- both brake indications: the 12 V normally-open brake-light switch and the ground-referenced normally-open brake-light test switch;
- road speed;
- engine speed; and
- an approximately `0.5 s` time delay intended to support winter operation.

With the engine running and vehicle stationary, Y19 locks the selector when no valid brake signal is detected. Shifting out of P or N is permitted only after the complete OEM logic has evaluated the required signals. Record the exact stationary-speed threshold, running-speed threshold, and delay edge from authoritative BMW information or measurements of the original system; do not invent threshold values.

The required functional expression is:

```text
Lock request = selector position is P or N
            AND engine is running
            AND vehicle is stationary
            AND no valid brake-applied signal is present
            AND the OEM time condition is satisfied
```

CANTCU `Variable Controlled` supports no more than two realtime conditions joined by `AND` or `OR`. It therefore cannot directly reproduce this complete OEM expression from separate selector, brake, road-speed, and engine-speed values. Do not replace the OEM logic with only `P AND Brake`, brake-only logic, or any other two-condition approximation.

Use B1/DOUT1 only through one of these CANformance-confirmed implementations:

1. `CAN / External Trigger`, driven by one validated composite **shift-lock release** command that evaluates all OEM conditions and fails inactive when any required message is missing, stale, or implausible.
2. `Variable Controlled`, only if the installed Race+ firmware exposes a single realtime value that already represents the complete validated OEM release request, including position, brake, speed, RPM, timing, and invalid-data handling.
3. A CANformance-supported dedicated shift-lock function with documented equivalent behavior.

The conversion currently expects brake, road speed, and engine speed through validated CAN data. Confirm whether the DDE4.1 brake status preserves the plausibility checking provided by the original two opposite-reference brake contacts. If it does not, provide an approved redundant brake interface or obtain CANformance acceptance of the reduced diagnostic coverage.

Configure the final command with:

```text
Logical meaning:    B1 active = validated release request
Startup pulse:      disabled
Missing data:       release request inactive
Invalid data:       release request inactive
Timing:             approximately 0.5 s, on the OEM-defined transition
```

On configuration startup, controller reset, or loss of the composite command, B1 must be inactive. Confirm that this inactive state produces the intended mechanical lock with the selected relay contact and measured Y19 polarity. The mechanical emergency release remains necessary for power or data failure.

## Bench and Vehicle Acceptance Tests

1. Disconnect X1599 and X1561 from their original circuits and prove isolation from battery voltage, chassis ground, E82, and the removed AGS.
2. Record resistance from each S227 and S224 signal to its common at every lever position, including slow movement between detents.
3. Confirm exactly one valid PRND contact at each automatic-gate detent and record the manual-gate state.
4. Measure every conditioned AIN voltage open and closed at minimum and maximum supply voltage, during harness movement, and across the expected temperature range.
5. Verify P, R, N, D, maintained manual mode, momentary strike-up, and momentary strike-down independently in CANTCU live data, and verify the brake status from the DDE4.1 CAN signal.
6. Verify that CANTCU pedal position/driver demand reaches the calibrated minimum and maximum values and produces the intended full-pedal downshift without a discrete kick-down input.
7. If the optional external request is retained, verify continuity and absence of hidden branches from the kick-down switch to the former X70003 pin 17 conductor, reterminate it at C6/DIN4, and test released, active, held, bounced, and disconnected states in CANTCU live data.
8. Open and short each signal wire individually to C7, C2, chassis ground, and battery voltage through a current-limited test interface appropriate to the protection design.
9. Test no-contact and multiple-contact states and verify that neither can create an unintended R or D request.
10. Confirm physical strike-up/down direction, prove each strike is accepted only with the manual-gate contact closed, and ensure an outside-gate, held, bouncing, shorted, or simultaneous strike cannot create an unintended or repeated request.
11. Measure Y19 steady-state/inrush current and prove whether it is powered to lock or powered to release.
12. Verify B1/DOUT1 current, active-low electrical behavior, composite-command source, configured realtime variables, approximately 0.5 s OEM timing, startup behavior, and relay-contact selection.
13. In both P and N, test every combination of brake released/applied, engine stopped/running, and vehicle stationary/moving; verify the lock follows the OEM truth table.
14. Test slow selector transitions, missing/stale brake, road-speed and engine-speed CAN data, invalid selector state, CANTCU reset/power loss, relay-coil open circuit, and simulated welded contacts.
15. Verify Park/Neutral start authorization, reverse lamps, shift lock, full-pedal downshift response, and displayed gear from confirmed transmission state.
16. Repeat the complete test after final harness installation and before enabling engine torque.

## Original Wiring References

S224 Steptronic switch pinout:

![S224 Steptronic switch pinout](8HP70/S224-SteptronicSwitch-Pinout.png)

S224 Steptronic switch wiring:

![S224 Steptronic switch wiring](8HP70/SteptronicSwitch-Wiring.png)

E82 gear-indicator-light and S227 selector-contact pinout:

![E82 gear indicator light pinout](8HP70/GearIndicatorLight-Pinout.png)

E82 gear-indicator-light and S227 selector-contact wiring:

![E82 gear indicator light wiring](8HP70/GearIndicatorLight-Wiring.png)

Y19 shift-lock pinout:

![Y19 shift lock pinout](8HP70/ShiftSelectorLock-Pinout.png)

Y19 shift-lock wiring:

![Y19 shift lock wiring](8HP70/ShiftSelectorLock-Wiring.png)

## References

- [CANformance Universal DIN/CAN Shifter](https://wiki.canformance.net/CANTCU/integrations/supportedshifters/universalshifter)
- [CANformance input configuration](https://wiki.canformance.net/CANTCU/software/config/inputcfg)
- [CANformance output configuration](https://wiki.canformance.net/CANTCU/software/config/outputcfg)
- [CANformance CANTCU pinout](https://wiki.canformance.net/CANTCU/hardware/CANTCU_pinout)
- BMW NewTIS wiring information represented by the project images above
