# BMW E38 740d 8HP50Z Transmission Conversion

## Purpose

This project replaces the original BMW A5S 560Z / ZF 5HP30 in a 2001 BMW E38 740d with a ZF 8HP50Z controlled by CANTCU.

This document is the high-level conversion plan and index. Detailed procedures, measurements, wiring assignments, and calibration records belong in the following guides:

1. [Hardware Installation](HW-Installation.md) - gearbox, adapter and converter, OEM transmission support adapter, driveshaft, cooling, and mechanical validation
2. [CANTCU Installation](CANTCU-Installation.md) - controller mounting, power, wiring, CAN integration, selector, interlocks, and electrical validation
3. [CANTCU Programming and Parameter Tuning](CANTCU-Programming.md) - firmware, configuration, commissioning, logging, and calibration

> [!WARNING]
> This conversion affects the drivetrain, vehicle controls, and road safety. Fabrication, welding, driveshaft modification, electrical work, and calibration must be completed and inspected by suitably qualified people. Comply with local inspection, registration, and insurance requirements.

## Vehicle and Donor Summary

<!-- markdownlint-disable MD060 -->

| Item | Build-specific value |
| --- | --- |
| Vehicle | 2001 BMW E38 740d |
| VIN | WBAGE81 |
| Engine | BMW M67B39 |
| Original transmission | BMW A5S 560Z / ZF 5HP30 |
| Original remanufactured transmission | BMW 24 00 7 506 999 |
| Final drive | BMW 33 10 7 508 140, ratio 2.65:1 |
| Original transmission-end driveshaft coupling | 110 mm bolt circle, M12 bolts |
| Original differential-end driveshaft joint | CV joint, BMW 26 11 1 229 772, 94 mm, Z=34, six M10 fasteners |
| Donor transmission | ZF 8HP50Z |
| Donor vehicle and year | To be recorded |
| Transmission assembly number | To be recorded from label |
| Torque converter number | To be recorded |
| CANTCU | Serial 468B, hardware revision 1.9 |
| CANTCU firmware | To be recorded |

<!-- markdownlint-enable MD060 -->

All 8HP50/51 variants identified by DomiWorks share the N57-pattern bellhousing. Their torque converters, oil pans, cooler ports, output arrangements, mechatronics, and wiring connectors are not necessarily interchangeable.

## Key Project Decisions

- Retain the output flange installed on the exact donor 8HP50Z. Use a professionally fabricated two-piece hybrid driveshaft with a matching RWD F3x 8HP50 transmission-end coupling. Retain the E38 rear shaft, rear CV joint, centre joint, and centre support with bearing; modify only the forward section. Replace parts outside specified wear or runout limits, refurbish accepted parts, and dynamically balance the completed assembly.
- Retain the dedicated E38 transmission oil cooler if it passes cleaning, inspection, pressure testing, and contamination assessment. Connect the exact 8HP50Z through a verified cooler-port adapter and BMW `17 22 7 592 723` / MAHLE-BEHR `TO 15 80`, an `80 degrees C` full-flow bypass thermostat. DomiWorks Type 1 is the provisional transmission adapter. The thermostat selection remains provisional pending port identification and thermal and hydraulic bench validation against the exact transmission's flow and pressure requirements.
- Retain BMW E38 gearbox support `22 32 1 096 427` and fabricate an engineered adapter between the 8HP50Z mount interface and the OEM support.
- PMC reports two customers using its M62 adapter for M67 swaps but cannot confirm modifications, complete bolt fit, or torque-converter offset; PMC also describes the M67 pattern as unique. James Scott Foley is likely, but not confirmed, to be one of those two customers. His documented E65 M67D44/8HP75 build used the 25 mm PMC adapter with starter, fastener, crank-sensor, and spacer modifications. This is not proof of direct fit on the earlier M67B39.
- Supply CANTCU A1 and the 8HP main-power input through a dedicated 15 A fused BMW `61 36 8 373 700` load relay. Use HELLA `5HE 996 152-131`, adjusted and bench-verified to retain its output for at least 60 seconds after terminal 15 switches off, to control the load-relay coil. CANTCU C4 WUP must switch off immediately with ignition while main power remains available for at least 60 seconds.
- Start with a conservative CANTCU calibration approved for the exact transmission and mechatronics. Do not copy pressure or clutch settings from another 8HP variant.

## Engineering Gates

Resolve these points before committing parts or beginning fabrication:

1. Record the exact transmission, mechatronics, and converter identities.
2. Confirm transmission and converter suitability for M67 torque, vehicle mass, intended use, and engine tuning.
3. Obtain dimensional or written manufacturer confirmation for the complete M67-to-8HP adapter system.
4. Measure tunnel, oil-pan, steering, exhaust, mount, cooler-line, and output-position clearances.
5. Confirm CANformance support for the exact mechatronics and required vehicle signals.
6. Select either a supported F-series 8HP CAN GWS or a CANformance-approved custom input conversion of the original E38 Steptronic assembly; define selector operation, fault behavior, Park/Neutral interlock, reverse lights, and cluster display.
7. Confirm the legal inspection, registration, and insurance requirements for the conversion.

## High-Level Conversion Steps

### 1. Establish a Baseline

Scan the vehicle, repair existing faults, photograph the original installation, and record mechanical dimensions and operating data.

### 2. Identify and Inspect the Donor Assembly

Record all labels and part numbers. Inspect the transmission, mechatronics, converter, connector, pan, output flange, and cooler ports before ordering conversion parts.

### 3. Complete the Hardware Installation

Remove the 5HP30, trial-fit the 8HP50Z, verify the adapter and converter interface, fabricate the 8HP50Z-to-OEM-support adapter and driveshaft, install cooling, and complete mechanical assembly. Follow [Hardware Installation](HW-Installation.md).

### 4. Install CANTCU and Vehicle Interfaces

Mount the controller and wire power, grounds, mechatronics, CAN, selector, brake input, reverse output, and Park/Neutral interlock. Follow [CANTCU Installation](CANTCU-Installation.md).

### 5. Configure CANTCU

Archive the initial controller state, verify firmware compatibility, select the exact transmission profile, configure vehicle scaling and CAN signals, and load a conservative calibration. Follow [CANTCU Programming and Parameter Tuning](CANTCU-Programming.md).

### 6. Complete Static Commissioning

Verify all live data and safety interlocks before startup. With the vehicle safely supported, check engagement, direction, speed signals, temperature, noise, vibration, leaks, and fluid level.

### 7. Perform Controlled Road Testing

Begin in a closed, low-risk area at light load. Log every stage, review shift behavior, clutch and converter slip, temperatures, torque reduction, and vibration, then increase load progressively.

### 8. Inspect and Close the Build

Reinspect safety-critical fasteners, mounts, driveshaft, cooler circuit, wiring, fluid level, and leaks. Archive the final mechanical, electrical, software, and road-test records and complete the required legal inspection.

## Project Acceptance Checklist

- [ ] Exact donor transmission, mechatronics, and converter identified
- [ ] Adapter geometry, concentricity, converter spacing, and runout accepted
- [ ] OEM gearbox support, custom support adapter, mounts, driveshaft, cooling, and fluid system accepted
- [ ] Harness protection, fused delayed power, WUP shutdown sequence, grounds, CAN, selector, and interlocks accepted
- [ ] Conservative configuration and calibration validated by logs
- [ ] No leaks, abnormal noise, vibration, bus faults, ratio errors, or unexplained clutch slip
- [ ] Post-test mechanical and electrical inspection completed
- [ ] Build records and final configuration archived
- [ ] Required legal inspection and documentation completed

## Source Hierarchy

Use current documents for the exact installed components in this order:

1. BMW workshop information and wiring diagrams
2. ZF service information for the identified 8HP50Z assembly
3. Current CANTCU installation, firmware, and calibration documentation
4. Adapter and driveshaft manufacturer drawings and written specifications
5. Local vehicle modification and inspection regulations

Product research and detailed references are retained in the guide that owns the related work. Avoid unverified forum pinouts, dimensions, and calibration files.
