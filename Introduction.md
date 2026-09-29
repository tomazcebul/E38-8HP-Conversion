# BMW E38 740d 8HP70 Transmission Conversion

## Purpose

This project replaces the original BMW A5S 560Z / ZF 5HP30 in a 2001 BMW E38 740d with a BMW F10 ZF 8HP70 controlled by CANTCU.

This document is the high-level conversion plan and index. Detailed procedures, measurements, wiring assignments, and calibration records belong in the following guides:

1. [Hardware Installation](HW-Installation.md) - gearbox, adapter and converter, OEM transmission support adapter, driveshaft, cooling, and mechanical validation
2. [CANTCU Installation](CANTCU-Installation.md) - controller mounting, power, wiring, CAN integration, selector, interlocks, and electrical validation
3. [CANTCU Programming and Calibration](CANTCU-Programming.md) - firmware, configuration, commissioning, logging, and calibration
4. [M67B39 Turbocharger Assessment and Upgrade Options](../Turbo/Turbochargers.md) - identification, fault diagnosis, remanufacture, power upgrades, and commissioning

> [!WARNING]
> This conversion affects the drivetrain, vehicle controls, and road safety. Fabrication, welding, driveshaft modification, electrical work, and calibration must be completed and inspected by suitably qualified people. Comply with local inspection, registration, and insurance requirements.

## Vehicle and Donor Summary

<!-- markdownlint-disable MD060 -->

| Item | Build-specific value |
| --- | --- |
| Vehicle | 2001 BMW E38 740d |
| VIN | WBAGE81080... |
| Engine | BMW M67B39 |
| Engine-management architecture | Two BMW DDE 4.1 control units, master/slave communication over the dedicated CANP bus |
| Bosch engine-control platform | Bosch EDC15C4 for both DDE 4.1 units; confirm from physical labels |
| DDE diagnostic variants | `DDE41KRO` and `DDE41KLO` |
| DDE label identities | BMW and Bosch numbers for both units to be recorded |
| Original transmission | BMW A5S 560Z / ZF 5HP30 |
| Original remanufactured transmission | BMW 24 00 7 506 999 |
| Final drive | BMW 33 10 7 508 140, ratio 2.65:1 |
| Original transmission-end driveshaft coupling | 110 mm bolt circle, M12 bolts |
| Original differential-end driveshaft joint | CV joint, BMW 26 11 1 229 772, 94 mm, Z=34, six M10 fasteners |
| Donor transmission | BMW GA8HP70Z-WTT / ZF 8HP70 |
| Donor vehicle, year, and engine application | Actual donor VIN to be recorded; BMW `24 00 7 642 542` is cataloged as GA8HP70Z-WTT for the F10 LCI 535d N57 application |
| Donor configuration | RWD, N57-pattern bellhousing; established from the tagged assembly's F10 LCI 535d application and the photographed rear propshaft output flange |
| BMW transmission assembly number | `24 00 7 642 542` (`LU 7642542`) |
| ZF model/type code | `8HP70` / `WTT`; sticker code `097WTT` |
| ZF serial number | `0257888` |
| ZF Stücklistennummer | `1087 004 050`, transcribed from the split cast tag; confirm against ZF data |
| Donor photographs | Tags: [8HP70-Picture1.jpg](8HP70/8HP70-Picture1.jpg), [8HP70-Picture2.jpg](8HP70/8HP70-Picture2.jpg); output flange: [8HP70-Picture3.jpg](8HP70/8HP70-Picture3.jpg); bellhousing side: [8HP70-Picture4.jpg](8HP70/8HP70-Picture4.jpg); converter markings: [8HP70-Picture5.jpg](8HP70/8HP70-Picture5.jpg) |
| Mechatronics number | To be recorded |
| Torque converter marking | `1087322397 8639` (ZF number formatted as `1087 322 397`); second line `250700004399`; right of QR code: `3 201311204001`, `V172`; production year `2013`; confirm the application and corresponding BMW service part number |
| CANTCU | Serial 468B, hardware revision 1.9 |
| CANTCU firmware | To be recorded |

<!-- markdownlint-enable MD060 -->

BMW assembly `24 00 7 642 542` identifies the donor as a GA8HP70Z-WTT for the F10 LCI 535d N57 application, with an N57-pattern bellhousing and RWD output. The photographed output flange has a nominal `110 mm` bolt circle; verify the bolt circle, fasteners, centering register, cooler interface, mechatronics, and converter before fabrication.

## Key Project Decisions

- Retain the donor 8HP70 output flange and complete original E38 two-piece driveshaft. Both transmission interfaces use a 110 mm bolt circle with M12 fasteners, so no donor shaft section is required. Professionally adjust only the E38 forward shaft length, verify the centering and coupling geometry, and dynamically balance the complete assembly.
- Retain the dedicated E38 transmission oil cooler if it passes cleaning, inspection, pressure testing, and contamination assessment. Connect the exact 8HP70 through a verified cooler-port adapter and BMW `17 22 7 592 723` / MAHLE-BEHR `TO 15 80`, an `80 degrees C` full-flow bypass thermostat. DomiWorks Type 1 remains provisional only if measurement confirms the donor has its listed N57 8HP70 interface. Verify routing, unrestricted flow, and operating temperature on the completed installation.
- Retain BMW E38 gearbox support `22 32 1 096 427` and fabricate an engineered adapter between the 8HP70 mount interface and the OEM support.
- Use the Adamat Performance M67-specific adapter and trigger-flywheel kit. Obtain a drawing and written specification tied to the M67B39, donor 8HP70, converter, and starter; verify the delivered geometry, trigger index, axial stack, runout, and balance before installation.
- Use CANformance Race+ as the selected TCM software and installation baseline. Race+ is the recommended solution for new supported CANTCU installations and supports ZF 8HP70. Back up the stock TCM with the 8HP TCM Tool before programming Race+.
- Reuse both X70001 pin 8 and pin 9 supplies for Race+: they are separate same-source 1.5 mm2 `U_UBR` branches from X6821, which is fed by the 4.0 mm2 `U_HR` conductor through 30 A F4. Combine the two conductors in a rated two-into-one automotive splice, install a dedicated 15 A fuse immediately downstream, then run new 2.5 mm2 conductors to CANTCU A1 and 8HP pin 13 and a 0.5 mm2 supply to F-series GWS pin 10. The additional BMW load relay and HELLA delayed-off timer are not required for Race+.
- Start with a conservative Race+ configuration approved for the exact transmission and mechatronics. Do not copy pressure, clutch, converter, or shift-map settings from another 8HP variant.

## Engineering Gates

Resolve these points before committing parts or beginning fabrication:

1. Record the exact transmission, mechatronics, and converter identities.
2. Confirm transmission and converter suitability for M67 torque, vehicle mass, intended use, and engine tuning.
3. Obtain Adamat's written specification for the complete M67-to-8HP kit and confirm the exact M67B39, 8HP70, converter, starter, trigger, and axial-stack application.
4. Measure tunnel, oil-pan, steering, exhaust, mount, cooler-line, and output-position clearances.
5. Confirm Race+ support and licensing/programming requirements for the exact mechatronics, create and verify a stock TCM backup, and confirm the required vehicle signals.
6. Validate BMW F-series 8HP GWS `61 31 9 296 898`, its connector and CANTCU profile; define fault behavior, Park/Neutral interlock, reverse lights, and cluster indication.
7. Confirm the legal inspection, registration, and insurance requirements for the conversion.

## High-Level Conversion Steps

### 1. Establish a Baseline

Scan the vehicle, repair existing faults, photograph the original installation, and record mechanical dimensions and operating data.

### 2. Identify and Inspect the Donor Assembly

Record all labels and part numbers. Inspect the transmission, mechatronics, converter, connector, pan, output flange, and cooler ports before ordering conversion parts.

### 3. Complete the Hardware Installation

Remove the 5HP30, trial-fit the F10 8HP70, verify the adapter and converter interface, fabricate the 8HP70-to-OEM-support adapter and driveshaft, install cooling, and complete mechanical assembly. Follow [Hardware Installation](HW-Installation.md).

### 4. Install CANTCU and Vehicle Interfaces

Install CANTCU, the 8HP connector, and the F-series GWS using the approved Race+ power and harness-reuse schedule. Verify every reused conductor end-to-end, connect CAN3 to the master DDE through the former AGS pair, and preserve the independent master/slave CANP bus. Follow [CANTCU Installation](CANTCU-Installation.md).

### 5. Configure CANTCU

Archive the initial controller state, verify firmware compatibility, select the exact transmission profile, configure vehicle scaling and CAN signals, and load a conservative calibration. Follow [CANTCU Programming and Calibration](CANTCU-Programming.md).

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
- [ ] Harness protection, Race+ switched power, WUP, grounds, CAN, selector, and interlocks accepted
- [ ] Conservative configuration and calibration validated by logs
- [ ] No leaks, abnormal noise, vibration, bus faults, ratio errors, or unexplained clutch slip
- [ ] Post-test mechanical and electrical inspection completed
- [ ] Build records and final configuration archived
- [ ] Required legal inspection and documentation completed

## Source Hierarchy

Use current documents for the exact installed components in this order:

1. BMW workshop information and wiring diagrams
2. BMW and ZF service information for the identified F10 8HP70 assembly
3. Current CANTCU installation, firmware, and calibration documentation
4. Adapter and driveshaft manufacturer drawings and written specifications
5. Local vehicle modification and inspection regulations

Product research and detailed references are retained in the guide that owns the related work. Avoid unverified forum pinouts, dimensions, and calibration files.
