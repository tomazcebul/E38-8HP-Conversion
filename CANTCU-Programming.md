# CANTCU Programming and Parameter Tuning

## Scope

This document covers CANTCU firmware identification, initial configuration, parameter tuning, static commissioning, controlled road testing, and calibration records for the E38 740d 8HP50Z conversion.

Complete [CANTCU Installation](CANTCU-Installation.md) and the relevant mechanical checks in [Hardware Installation](HW-Installation.md) before commissioning. Use a conservative base calibration supplied or approved by CANformance for the exact transmission and vehicle characteristics.

> [!WARNING]
> Incorrect transmission profiles, clutch pressures, torque limits, or converter settings can damage the transmission and create unsafe vehicle behavior. Do not copy calibration values from an unrelated 8HP variant.

## Required Information and Equipment

- CANTCU hardware revision `1.9`, serial number `468B`
- Installed firmware version and matching configuration software
- Exact 8HP50Z assembly and mechatronics identities
- Exact torque-converter identity
- M67B39 torque characteristics, including any engine modifications
- Differential ratio `2.65`
- Measured tyre rolling circumference
- CANTCU configuration interface and laptop
- CAN diagnostic interface and logging capability
- Safe test area and a second person to monitor data where practical

## 1. Preserve the Starting State

1. Record the installed firmware and configuration-software versions.
2. Read and save the controller's existing configuration before changing it.
3. Use dated, immutable copies for each tested configuration.
4. Record the transmission, converter, tyre, differential, and vehicle details with the configuration.
5. Define a rollback configuration before first startup.

Do not update firmware solely because a newer version exists. Confirm hardware revision support, migration requirements, and configuration compatibility first.

## 2. Configure the Base Parameters

Verify every item against the exact firmware documentation:

- Exact transmission and mechatronics profile
- Engine cylinder count and RPM source
- Tyre rolling circumference
- Differential ratio
- Input- and output-speed scaling
- Selector type and direction logic
- Selector firmware profile and CAN-bus assignment, or custom PRND/manual input mapping and truth table
- Brake input polarity
- Reverse and Park/Neutral output behavior
- Engine torque model, torque limits, and torque-reduction strategy
- CAN bitrate, receive messages, transmit messages, and termination setting
- Manual mode, paddle, and mode-switch behavior
- Maximum transmission temperature and protection behavior

Confirm that calculated road speed agrees with an independent measured speed. Incorrect tyre or final-drive scaling can corrupt shift scheduling and protection logic.

## 3. Establish a Conservative Calibration

Start with a CANformance-approved baseline for the exact mechatronics and the closest supported vehicle characteristics. Initially use conservative engine torque limits and prohibit full-load operation.

Review these calibration groups:

- Drive and Sport shift schedules
- Upshift and downshift hysteresis
- Kickdown behavior
- Clutch fill and shift-pressure settings
- Shift timing and overlap
- Converter lock-up enable conditions and slip target
- Coast-downshift behavior
- Manual-mode limits and automatic interventions
- Temperature, speed, and pressure protection behavior

Change one related group at a time, assign a new configuration version, and record the reason. Pressure should not be used to conceal an incorrect transmission profile, missing torque reduction, mechanical fault, or adaptation problem.

## 4. Verify Live Data Before Startup

With ignition on and the engine stopped, confirm that these values are present and plausible:

- Engine speed is zero
- Throttle or calculated load tracks pedal input
- Brake status changes correctly
- Selector position and direction are correct
- F-series GWS online status and indication are correct, or every E38 custom-input state and invalid combination is handled safely
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
5. Test manual selection, kickdown, coast downshifts, and braking behavior progressively.
6. Increase load in small steps and review each log before continuing.
7. Stop and inspect mounts, adapter, fasteners, driveshaft, cooler lines, wiring, fluid level, and leaks.

Do not begin full-load testing until shift quality, torque reduction, clutch slip, temperatures, and driveline vibration have been reviewed by a competent calibrator.

## 7. Parameter Tuning Workflow

For each issue, preserve the log and classify it before changing parameters:

1. Check for mechanical faults, incorrect fluid level, temperature problems, and active diagnostic codes.
2. Confirm that the selected transmission profile and all input data are correct.
3. Compare commanded gear, actual ratio, input/output speed, engine torque, torque reduction, converter state, and clutch slip.
4. Change the smallest relevant parameter set.
5. Repeat the same controlled test conditions.
6. Accept the change only when logs improve without creating faults elsewhere.

Evaluate shift duration and firmness together with thermal response, clutch slip, torque reduction, and driveline shock. A shorter or firmer shift is not evidence of acceptable calibration without supporting log data.

## Programming and Tuning Acceptance Checklist

- [ ] Firmware and configuration-software versions recorded
- [ ] Original, base, and final configurations archived
- [ ] Exact transmission/mechatronics profile confirmed
- [ ] Differential and tyre scaling verified against measured speed
- [ ] All required live inputs are plausible and stable
- [ ] Selector, brake, reverse, and Park/Neutral logic verified
- [ ] Selector loss-of-communication or electrical-fault behavior verified
- [ ] Conservative torque, shift, and lock-up calibration installed
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
| Original configuration |  |
| Base configuration |  |
| Final configuration |  |
| Transmission profile |  |
| Selector type/profile and BMW part number |  |
| Selector input map or CAN assignment |  |
| CAN definition/version |  |
| Tyre circumference |  |
| Differential ratio | 2.65 |
| First-start log |  |
| Static commissioning report |  |
| Final validation log |  |

<!-- markdownlint-enable MD060 -->

## References

- Current CANTCU firmware, configuration, and calibration documentation
- CANformance-approved base calibration for the exact 8HP50Z mechatronics
- ZF service information for the identified 8HP50Z assembly
- BMW E38 and M67 diagnostic information
