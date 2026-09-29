# Hardware Installation

## Scope

This document covers the mechanical installation of a BMW F10 ZF 8HP70 in the 2001 BMW E38 740d: removal, trial fitting, engine adapter and converter interface, mounts, driveshaft, cooling, final assembly, and mechanical validation.

Read the project overview and record the exact donor transmission and converter identities in [Introduction](Introduction.md) before ordering conversion parts. CANTCU wiring and configuration are covered separately in [CANTCU Installation](CANTCU-Installation.md) and [CANTCU Programming and Calibration](CANTCU-Programming.md).

> [!WARNING]
> Fabrication, welding, driveshaft modification, and drivetrain alignment affect road safety. Use suitably qualified specialists and comply with local inspection requirements.

## Components

- Complete F10 8HP70 with matched mechatronics, oil pan, connector, output flange, and torque converter
- Adamat Performance M67-specific engine-to-transmission adapter and trigger-flywheel kit, with final contents and application confirmed in writing
- Original M67-specific starter, subject to inspection and compatibility confirmation with the Adamat kit
- Adamat-supplied or specified crankshaft-to-converter adapter, spacer, and associated fasteners
- Converter bolts, bellhousing bolts, dowels, and all safety-critical fasteners
- Original BMW E38 gearbox support `22 32 1 096 427`
- Custom 8HP70-to-OEM-support adapter and correctly rated transmission mounts
- Original E38 two-piece driveshaft, professionally length-adjusted and dynamically balanced as a complete assembly
- Output flange installed on the exact donor 8HP70 and original E38 transmission-end 110 mm/M12 coupling
- Serviceable OEM E38 transmission oil cooler or a suitably rated replacement
- Donor-specific 8HP70 oil-port adapter with compatible seals and fittings
- BMW `17 22 7 592 723` / MAHLE-BEHR `TO 15 80` transmission-oil thermostat with matching line ends or purpose-made adapters, subject to correct routing and installation verification
- ATF-rated hoses, crimps, fittings, line supports, abrasion protection, and heat protection sized for the verified cooler flow
- New transmission fluid, oil pan/filter assembly, seals, and one-time-use hardware specified by ZF
- Fabrication materials and exhaust parts required for clearance

## Tools and Facilities

- Vehicle lift or correctly rated stands on a level surface
- Transmission jack and engine support equipment
- Accurate straightedge, depth gauge, vernier caliper, and angle finder
- Torque wrenches covering all required ranges
- Driveshaft balancing and welding services
- Suitable equipment for identifying the thermostat ports and monitoring transmission-oil temperatures during commissioning
- BMW diagnostic equipment for baseline and final checks

## 1. Record the Mechanical Baseline

Before dismantling the vehicle:

1. Photograph the original installation, cooler lines, exhaust, mounts, and driveshaft orientation.
2. Measure the original transmission output and mount positions, driveshaft length, and driveline angles.
3. Record the differential ratio, tyre size, and road speed versus engine speed in the available gears.
4. Mark the driveshaft orientation before removal.

## 2. Remove the Original Transmission

1. Disconnect the battery according to BMW service procedures.
2. Raise and securely support the vehicle.
3. Remove the required undertrays, exhaust sections, heat shields, and braces.
4. Remove the driveshaft and inspect the transmission-end coupling, centre support bearing, universal joints, rear constant-velocity joint, and differential input flange.
5. Disconnect the selector mechanism, cooler lines, electrical connectors, starter, and torque-converter fasteners.
6. Support the engine and transmission, remove the crossmember, and remove the original transmission.
7. Inspect the rear crankshaft seal area, starter, ring gear, engine mounts, transmission tunnel, and exposed wiring.

Follow the BMW workshop manual for removal details and tightening procedures. Drain and dispose of fluids responsibly.

## 3. Trial-Fit the F10 8HP70

Trial-fit the bare transmission before finalizing adapters, mounts, or the driveshaft. Check and record:

- Bellhousing and tunnel clearance throughout drivetrain movement
- Oil-pan clearance to the front subframe and steering components
- Exhaust and heat-shield clearance
- Mechatronics connector access and harness protection
- Cooler-line routing and service access
- Output-flange location relative to the differential
- Transmission mount position and crossmember geometry
- Propshaft operating angles at normal ride height

Do not use the transmission mount or bellhousing bolts to force components into alignment.

## 4. Establish the Engine Adapter and Converter Interface

The crankshaft, adapter, bellhousing, and transmission input shaft must share a common axis. Incorrect converter spacing can damage the pump, converter, crankshaft thrust bearing, or flexplate.

The design must establish:

- Positive concentric location using machined registers and correctly fitted dowels
- Starter motor position and ring-gear engagement
- Converter pilot diameter and engagement depth
- Converter-to-flexplate bolt pattern and fastener access
- Full converter seating in the transmission before installation
- Correct converter pull-forward distance after the bellhousing is tightened
- Adequate flexplate strength and axial flexibility
- Suitable fastener material, engagement, locking method, and clearance

Record all measured and final dimensions in [Mechanical Build Record](#mechanical-build-record). Have the completed rotating assembly checked for runout and balance.

### Selected Adamat M67-to-8HP Adapter Kit

The selected solution is an Adamat Performance M67-specific adapter and flywheel kit. No OEM drawing or measured coordinate comparison establishes that the M67 and M60/M62 bellhousing patterns are identical; the exact M67B39 and donor-8HP70 geometry therefore requires documented confirmation.

#### Adamat Manufacturer Confirmation

In direct email correspondence supplied for this project, Adamat Performance representative Adam Walczak confirmed that Adamat can manufacture an M67-specific kit. He described its adapter plate as practically the same as the M62 version, while the flywheel is similar but has its trigger teeth positioned correctly so the engine can start using the original DME.

The [published Adamat M60/M62/S62-to-8HP kit](https://adamat.com.pl/en/adapter-bmw-v8-m62-m60-s62-to-bmw-zf-8hp45-8hp50-8hp51-8hp70-8hp75.html) is the design basis for the M67 derivative. Adamat publishes the following base-kit specifications:

- One-piece `AlZnMg+Ti` lightweight-alloy flywheel with a steel starter ring, total weight `4.2 kg`
- Dynamically balanced flywheel and a manufacturer-claimed maximum torque capacity of `2000 Nm`
- `50 mm`-thick AW7075-T651 aluminium transmission adapter
- Adapter socket for the original M62/S62 crankshaft-position sensor
- Flywheel, adapter, and transmission mounting bolts
- Applications including N57/N57N `GA8HP70` and `GA8HP75X`, plus listed B58, B57, B48, B46, and B47C/D20 8HP variants

The M62/S62 crank-sensor socket and trigger arrangement are not the M67 specification. For the selected derivative, Adamat must supply the M67 trigger geometry described in its email and confirm any changes to the base adapter, flywheel, starter ring, converter interface, fasteners, material, thickness, weight, balance, and torque rating. Use the published `50 mm` thickness only for preliminary packaging until Adamat confirms the M67 drawing and the delivered kit is measured.

The project file [M67-8HP4576-1.jpg](Adamat-Adapter/M67-8HP4576-1.jpg) is a still from [BMW 740D E38 V8 TWIN-TURBO. HOW TO INSTALL AN 8-SPEED AUTOMATIC TRANSMISSION?](https://www.youtube.com/watch?v=XtBa4phpDPs) at `6:34`. The pictured Adamat flywheel is engraved `BMW V8 M67` and identifies BMW ZF `8HP45-76` applications. This is direct visual evidence that Adamat has produced an M67-designated flywheel for an 8HP conversion. The accompanying M62 kit photographs show the related adapter and flywheel construction but are not M67 dimensional evidence.

Adamat has not yet identified the M67 variant used for its geometry, the pictured transmission and converter, the final adapter thickness, or the specified converter pull-forward. Before manufacture, obtain a written specification and drawing tied to this M67B39, transmission, and converter. Verify the delivered parts by measurement and trial fit.

Request the following drawing data or written values from Adamat for the selected kit:

1. Engine-side adapter bolt and dowel coordinates, dowel diameters, and register diameter/depth.
2. Crankshaft bolt count, pitch-circle diameter, fastener size, locating register, flange stand-off, and flywheel mounting-face offset.
3. Flywheel/flexplate part used, ring-gear tooth count and axial position, required starter part number and mounting position, and pinion engagement.
4. Crankshaft-sensor type, target pattern, tooth count, index angle, air gap, and whether the M67 DDE can retain its original speed/reference signal.
5. Exact compatible 8HP70 converter, converter pilot diameter/depth, mounting pattern, installed clearance, and specified pull-forward distance.
6. Adapter thickness, bellhousing modifications, fastener lengths and grades, access for converter bolts, and required machining.
7. Maximum rated engine torque and whether the supplied flywheel has been balanced independently or with a specified converter/crank assembly.

If Adamat confirms only the bellhousing bolt pattern, the kit remains unapproved for final installation. The quickest conclusive pattern check is to trace or scan the rear face of the bare M67 block and compare its bolt centers, dowels, starter opening, and crank center with Adamat's drawing. Alternatively, offer the original M67 5HP30 converter housing to Adamat for direct coordinate measurement.

## 5. Fabricate the Transmission-Support Adapter and Driveshaft

Retain the original BMW E38 gearbox support `22 32 1 096 427` at the body-side mounting points. BMW catalog data identifies it as an E38 gearbox support used from April 1999; its listed weight is `1.176 kg`. Fabricate an intermediate adapter between the F10 8HP70 transmission-mount interface and this OEM support rather than replacing the support with a fully custom crossmember.

Position the drivetrain without introducing harmful engine or propshaft angles. Finalize the adapter only after the engine-to-transmission interface and output position are established. The adapter must:

- Positively locate the transmission mount without relying on slotted fasteners to resist drivetrain loads
- Preserve the OEM support's body mounting points without drilling or weakening the vehicle structure
- Carry vertical, longitudinal, lateral, and torque-reaction loads with an appropriate engineering safety factor
- Use transmission mounts with suitable load rating, stiffness, heat resistance, and fail-safe behavior
- Maintain oil-pan, exhaust, heat-shield, tunnel, selector, wiring, cooler-line, and driveshaft clearance throughout drivetrain movement
- Provide tool access and avoid trapped fasteners so the transmission and support remain serviceable
- Avoid welding, uncontrolled heating, or grinding of the OEM support unless an engineer approves and inspects the modification

Create a dimensioned drawing before fabrication. Use suitable structural material, radiused transitions, adequate edge distances, and locking hardware. Have the finished adapter and fastener arrangement reviewed by a qualified fabricator or engineer; inspect welds by an appropriate method if the adapter is welded.

### Gear-Ratio Comparison

Published BMW E38 and transmission-reference data give the following internal ratios for the A5S 560Z / ZF 5HP30 and the common first-generation ZF 8HP70 ratio set. Treat the 8HP70 values as preliminary: record the exact donor assembly number and confirm its ratio set from BMW or ZF data before entering ratios in CANTCU.

<!-- markdownlint-disable MD060 -->

| Gear | 5HP30 ratio | 5HP30 overall with 2.65 final drive | 8HP70 ratio | 8HP70 overall with 2.65 final drive |
| --- | ---: | ---: | ---: | ---: |
| 1 | 3.550 | 9.408 | 4.714 | 12.492 |
| 2 | 2.240 | 5.936 | 3.143 | 8.329 |
| 3 | 1.540 | 4.081 | 2.106 | 5.581 |
| 4 | 1.000 | 2.650 | 1.667 | 4.418 |
| 5 | 0.790 | 2.094 | 1.285 | 3.405 |
| 6 | - | - | 1.000 | 2.650 |
| 7 | - | - | 0.839 | 2.223 |
| 8 | - | - | 0.667 | 1.768 |
| Reverse | 3.680 | 9.752 | 3.317 | 8.790 |

<!-- markdownlint-enable MD060 -->

The preliminary 8HP70 first gear is `32.8%` shorter than the 5HP30 first gear with the same final drive, increasing torque multiplication at launch. Its eighth gear gives `15.6%` lower engine speed than the 5HP30 fifth gear at the same road speed, ignoring converter slip. Direct drive moves from fourth gear in the 5HP30 to sixth gear in the 8HP70. The forward-ratio span increases from approximately `4.49` to `7.07`.

These ratios do not by themselves determine shift points, launch traction, converter behavior, maximum road speed, or acceptable output-shaft speed. Confirm tyre rolling circumference, engine speed range, converter characteristics, and the exact donor ratio set when configuring and validating CANTCU.

### Transmission Length Comparison

No verified same-datum external-length pair is recorded for the exact F10 8HP70 and the E38 740d A5S 560Z / ZF 5HP30. The ZF 5HP30 spare-parts catalog and other located public sources do not state an equivalent external length, and dimensions from other 8HP variants must not be transferred. Parts diagrams are not dimensioned and must not be scaled.

Measure both transmissions between the same reference planes: place a straightedge across the engine mating face and measure parallel to the transmission axis to the propshaft-coupling face of the installed output flange. Record the flange fitted to each transmission because flange height changes this result.

For installation planning, adapter thickness moves the 8HP output farther rearward relative to the engine. As a first-order comparison:

$$
\Delta L = (L_{\mathrm{8HP70}} + t_{\mathrm{adapter}}) - L_{\mathrm{5HP30}}
$$

Use the M62 base kit's published `50 mm` adapter thickness for preliminary packaging only. Obtain confirmation that the M67 derivative retains this thickness, then measure the received adapter and complete assembled axial stack before finalizing the transmission support or driveshaft.

Confirm the actual output-flange position by trial-fitting the complete adapter, transmission, mounts, and retained donor flange. Account separately for any register, spacer, or engine-side geometry that changes the effective axial stack. Do not order or cut the driveshaft from published transmission lengths alone.

Because the effective F10 8HP70 output position is not yet established, measure the installed drivetrain before modifying the driveshaft. Retain the donor 8HP70 output flange and the complete original E38 two-piece driveshaft. Both transmission interfaces use a `110 mm` bolt circle with M12 fasteners; no donor driveshaft section is required. Adjust only the effective length of the E38 forward shaft section.

Finalize the engine mounts, OEM support position, custom support adapter, transmission mounts, and differential position first. With the vehicle at normal ride height, measure the required installed length between the 8HP70 coupling face and differential interface using the driveshaft fabricator's specified datums and allowance. Supply the complete E38 shaft to the specialist. The specialist must establish the length correction, cut and weld locations, joint phasing, centre-bearing position and preload, spline engagement and plunge allowance, critical speed, torque capacity, runout, weld design, and final installed length. Dynamically balance the complete two-piece assembly after modification and refurbishment.

The E38 transmission-end coupling and measured 8HP70 output flange both use a `110 mm` bolt circle with M12 fasteners. Verify the centering register, coupling-face geometry, fastener engagement, and axial clearance during trial fit, then retain the E38 transmission-end coupling. Retain the differential-end CV joint, BMW `26 11 1 229 772`, `94 mm`, `Z=34`, with six M10 fasteners, unless inspection requires replacement.

### Professional 8HP/E38 Driveshaft Fabrication

Retain the complete E38 driveshaft and modify only the length of its forward shaft section. A qualified driveshaft specialist must select the cut location and specify the tube, weld, sleeve, and reinforcement design from the shaft material, dimensions, M67 torque, and calculated maximum shaft speed.

1. Trial-fit the original E38 110 mm/M12 coupling to the 8HP70 output flange and verify bolt alignment, centering register, coupling-face contact, fastener engagement, and clearance.
2. Install the complete drivetrain in its final mounted position and measure between the gearbox and differential at normal ride height using the fabricator's specified datums and working-length allowance.
3. Give the complete E38 two-piece driveshaft and measured installation data to the specialist before cutting.
4. Preserve the transmission-end coupling, rear shaft, rear CV joint, centre joint, centre support, bearing, and their indexed relationship unless inspection identifies an unserviceable component.
5. Modify the forward shaft tube at the location selected by the specialist to achieve the required installed length. Do not alter the 110 mm/M12 transmission-end interface.
6. Apply the fabricator's specified tube, sleeve, weld preparation, and reinforcement process.
7. Preserve joint phasing and maintain the specified spline engagement, plunge allowance, centre-bearing position and preload, and clearance through the full drivetrain movement range.
8. Inspect CV joint `26 11 1 229 772`, its boot and lubricant, the `94 mm` differential flange, 34-tooth interface, six M10 knurled bolts, mating nuts, and sealing washer. Replace worn or damaged components.
9. Inspect every retained joint, spline, tube, coupling, and fastener. Inspect the centre-support bearing for noise, play, roughness, seal damage, and free rotation; inspect its rubber carrier and bracket for cracking, separation, distortion, and loss of stiffness. Replace components outside the applicable wear, damage, or runout limits.
10. Check straightness and runout, then dynamically balance the complete two-piece driveshaft as one indexed assembly. Mark the balanced orientation and record the fabricator's maximum-speed and torque rating.

> [!CAUTION]
> A poorly aligned or unbalanced driveshaft can damage the transmission and differential and can fail dangerously at road speed.

## 6. Install Transmission Cooling

### Selected Cooling Architecture

The July 2001 E38 740d has a dedicated transmission-oil cooler circuit rather than the engine-coolant heat exchanger used by many F-series 8HP donor installations. BMW catalog data identifies:

- Oil cooler `17 21 2 248 569`
- A5S 560Z cooler inlet pipe `17 22 2 248 641`
- A5S 560Z cooler outlet pipe `17 22 2 248 642`
- Four FPM O-rings `17 21 1 742 636`, size `10.82 x 1.78 mm`

Retain the E38 air-to-oil cooler only if it passes inspection, pressure testing, and a professional contamination assessment. The original rigid pipes are transmission-specific and should not be forced onto the 8HP70. Replace or modify them with correctly supported ATF hose assemblies. If the 5HP30 failed internally or the cooler cannot be verified clean, replace the cooler and contaminated lines rather than risking debris entering the 8HP70.

The selected circuit is:

```text
8HP70 hot outlet -> full-flow bypass thermostat -> E38 oil cooler -> thermostat -> 8HP70 return
```

Follow the markings and installation diagram supplied with the chosen adapter and thermostat; confirm the 8HP70 outlet and return ports instead of inferring direction from physical position. The thermostat must bypass the cooler during warm-up while preserving an unrestricted return path to the transmission.

### 8HP70 Cooler Adapter

Use an adapter made for the exact donor transmission casting. The tagged BMW assembly confirms an N57-pattern 8HP70. DomiWorks Type 1, SKU `22001001`, remains the provisional choice until inspection confirms that the donor's cooler interface matches its specified interface. Its published specification is:

- 8HP50 B58, 8HP70 N57, and 8HP45 N47 application
- `17 mm` offset transmission bores with an M6 retaining bolt
- Two female `ORB-8` ports, `3/4-16 UNF`
- Supplied bolt and O-rings; hose-end fittings are optional

DomiWorks states that BMW 8HP cooler-port bore size, offset, and retaining-bolt geometry vary among transmissions. Before ordering, measure the exact donor's bore diameters, centre spacing/offset, bolt size and position, sealing arrangement, and available tunnel clearance. Confirm the choice with the adapter manufacturer using the donor tag and photographs.

### Thermostat and Lines

Use BMW `17 22 7 592 723` / MAHLE-BEHR `TO 15 80`, a four-port full-flow bypass thermostat rated to open at `80 degrees C`. The purchased F80 M3 lines (`17 22 2 284 548` and `17 22 2 284 549`) may provide thermostat-end connections, but their GS7D36SG gearbox ends do not fit the provisional DomiWorks 8HP adapter. Measure both interfaces and use purpose-made, unrestricted transitions. Before installation:

1. Inspect the purchased genuine or OE-supplier thermostat and its four matching OEM pipe ends for damage, contamination, corrosion, and leakage; do not clamp generic hose over its sockets.
2. Identify all four ports from the original F80 M3 cooler-line arrangement and preserve the original flow, return, cooler, and bypass relationships in the adapted circuit.
3. Measure the minimum internal bore of the line ends and adapters and avoid transitions smaller than the retained OEM passages.
4. Reject the thermostat if it is damaged, contaminated, seized, leaking, or cannot be mounted with strain-free supported lines.
5. During commissioning, verify normal warm-up, cooler activation near the rated `80 degrees C` range, stable loaded temperature, and unobstructed return flow.

Use hoses, crimps, seals, and fittings rated for the selected transmission fluid, continuous temperature, peak pressure, pulsation, and vehicle vibration. Keep hose bore consistent, minimize restrictive elbows and reducers, route away from exhaust heat and moving parts, provide strain relief, support long runs, and protect every pass-through from abrasion. Mount the thermostat rigidly where it is protected from impact and can be serviced.

### Commissioning

1. Flush new hose assemblies and either professionally clean and pressure-test the E38 cooler or install a new cooler. Never use shop debris or solvent residue in the circuit.
2. Verify adapter seating, new seal compatibility, port routing, thermostat orientation, hose clearance, and fitting engagement before filling.
3. Prime the circuit as required by the transmission and component manufacturers. Fill only with the specified ZF fluid using the exact transmission's temperature-dependent procedure.
4. At initial start, check immediately for leaks, hose collapse, aeration, abnormal noise, and loss of drive. Do not run the transmission if cooler return flow is absent.
5. Confirm hot-out and cooled-return temperatures with sensors or contact measurements. Verify that the thermostat bypasses during warm-up and progressively sends flow through the cooler near its rated range.
6. Road-test progressively while logging transmission temperature in CANTCU. Test cold start, steady cruise, traffic, repeated shifts, and sustained load; verify both adequate warm-up and temperature control.
7. Recheck fluid level at the specified temperature, inspect every fitting and support, and repeat the leak inspection after the first complete heat cycle.

## 7. Final Assembly and Fluid Fill

1. Seat the torque converter fully in the transmission.
2. Install the transmission without drawing it into place with bellhousing bolts.
3. After tightening the bellhousing, measure converter pull-forward and check bellhousing and flywheel/converter runout.
4. Tighten all fasteners to specifications for the actual components and mark safety-critical fasteners after inspection.
5. Install the OEM gearbox support, custom support adapter, transmission mounts, driveshaft, cooler circuit, exhaust, heat shields, harness, and selector.
6. Confirm wiring and hoses have adequate movement and cannot contact sharp or hot surfaces.
7. Fill the transmission using the ZF procedure for the exact assembly, including fluid specification, vehicle level, engine-running gear cycling, and temperature window.
8. Check for leaks before testing.

## 8. Mechanical Validation

Before and during commissioning:

1. Inspect for abnormal noise, vibration, leaks, and converter/flexplate runout immediately after startup.
2. Stop for harsh engagement, no drive, abnormal noise, vibration, pressure, or temperature.
3. During progressive road testing, inspect mounts, adapter, fasteners, driveshaft, cooler lines, fluid level, and leaks after each load increase.
4. Do not begin full-load testing until shift quality, clutch slip, temperatures, and driveline vibration have been reviewed.

## Mechanical Acceptance Checklist

- [ ] Transmission and converter identities recorded
- [ ] Transmission torque/load suitability confirmed
- [ ] Adapter concentricity and converter spacing measured
- [ ] Rotating assembly runout and balance accepted
- [ ] Safety-critical fasteners torqued and inspected
- [ ] OEM gearbox support, custom adapter, mounts, and fasteners inspected
- [ ] Driveshaft professionally balanced and angles verified
- [ ] Centre-support bearing, rubber carrier, mount position, and preload verified
- [ ] Cooler flow, fluid level, and operating temperature verified
- [ ] No leaks, abnormal noise, driveline vibration, or clutch slip
- [ ] Post-test fastener, mount, driveshaft, and fluid inspection completed

## Mechanical Build Record

<!-- markdownlint-disable MD060 -->

| Measurement | Value | Method/date |
| --- | --- | --- |
| Donor tag photographs | [8HP70-Picture1.jpg](8HP70/8HP70-Picture1.jpg), [8HP70-Picture2.jpg](8HP70/8HP70-Picture2.jpg) | Reviewed 24 September 2026 |
| Donor output-flange photograph | [8HP70-Picture3.jpg](8HP70/8HP70-Picture3.jpg) | Reviewed 24 September 2026 |
| Donor bellhousing-side photograph | [8HP70-Picture4.jpg](8HP70/8HP70-Picture4.jpg) | Reviewed 25 September 2026; shows mating face, installed torque converter, and attached cooler lines |
| Donor torque-converter marking photograph | [8HP70-Picture5.jpg](8HP70/8HP70-Picture5.jpg) | Reviewed 25 September 2026 |
| BMW transmission designation | GA8HP70Z-WTT | Tag and BMW catalog cross-reference |
| BMW transmission assembly number | 24 00 7 642 542 (`LU 7642542`) | Adhesive tag |
| ZF model/type code | 8HP70 / WTT; sticker code `097WTT` | Cast and adhesive tags |
| ZF serial number | 0257888 | Cast tag and barcode text `0257888WTT` |
| ZF Stücklistennummer | 1087 004 050 / confirmation required | Split across the cast-tag fields |
| Secondary ZF sticker code | 1087 010 | Adhesive tag |
| Catalog application used for cross-check | F10 LCI 535d GA8HP70Z; actual donor VIN/application not yet recorded | BMW catalog |
| Bellhousing pattern | N57 pattern | Tagged BMW assembly `24 00 7 642 542`, cataloged F10 LCI 535d N57 application, and bellhousing-side photograph; inspect for prior housing replacement or modification |
| Donor output arrangement | Rear propshaft flexible-disc flange consistent with RWD | Catalog cross-check and output-flange photograph |
| Opposite output-flange coupling-position centre distance / bolt circle | 110 mm | Ruler from centre of one hole to centre of opposite bolt in [8HP70-Picture3.jpg](8HP70/8HP70-Picture3.jpg); confirm directly before fabrication |
| Mechatronics identification |  | Not visible in current tag photographs |
| Torque-converter identification | Stamped first line `1087322397 8639`; ZF number formatted as `1087 322 397`; application and BMW service part number require confirmation | [8HP70-Picture5.jpg](8HP70/8HP70-Picture5.jpg) and owner-verified transcription |
| Additional converter markings | Second line `250700004399`; right of QR code: `3 201311204001` and `V172` | Owner-verified photographic transcription; treat as production/traceability markings until decoded against ZF data |
| Torque-converter production date | Year 2013; trace string likely indicates 20 November 2013, but the complete code has not been formally decoded | Separate `2013` stamp and `20131120` sequence in the QR-adjacent marking |
| Engine-adapter manufacturer/kit | Adamat Performance M67-to-8HP, based on M60/M62/S62 kit / exact designation to be recorded |  |
| Adapter plate material | AW7075-T651 base-kit specification / confirm M67 kit |  |
| Adapter plate thickness | 50 mm base-kit specification / confirm and measure M67 kit |  |
| Adamat drawing and revision |  |  |
| Trigger flywheel identification |  |  |
| Trigger flywheel material/weight | AlZnMg+Ti / 4.2 kg base-kit specification / confirm M67 kit |  |
| Flywheel dynamic-balance report |  |  |
| Kit torque rating | 2000 Nm base-kit claim / obtain M67 confirmation |  |
| Trigger pattern/index accepted by original DME |  |  |
| Crank register diameter |  |  |
| Converter pilot diameter/depth |  |  |
| Converter pull-forward distance |  |  |
| Bellhousing runout |  |  |
| Flexplate/converter runout |  |  |
| Original 5HP30 mating-face-to-output-flange length |  |  |
| Donor F10 8HP70 mating-face-to-output-flange length |  |  |
| Calculated output-position difference including adapter |  |  |
| Trial-fitted output-position difference |  |  |
| Original output-flange position |  |  |
| 8HP output-flange position |  |  |
| OEM gearbox support part/condition | BMW 22 32 1 096 427 /  |  |
| Custom support-adapter drawing revision |  |  |
| Support-adapter material/thickness |  |  |
| Transmission mount part/rating |  |  |
| Support-adapter fastener specification |  |  |
| Rear CV joint part/condition | BMW 26 11 1 229 772 /  |  |
| Rear CV-joint interface | 94 mm, Z=34, six M10 / verify |  |
| Original E38 transmission-end coupling | LK=110 mm, M12 | Retained; verify centering register, face geometry, fastener engagement, and clearance on the 8HP70 |
| Donor 8HP70 output flange | LK=110 mm, M12 | Measured; retain installed flange |
| E38 rear/centre assembly condition |  |  |
| Gearbox-to-differential measured length and datums |  |  |
| E38 and donor forward-section cut locations |  |  |
| Tube joint, weld, and reinforcement specification |  |  |
| Centre-bearing mount position/preload |  |  |
| Final installed driveshaft length |  |  |
| Dynamic-balance report and indexed orientation |  |  |
| Fabricator maximum-speed/torque rating |  |  |
| Front/rear driveline angles |  |  |
| E38 cooler part/condition/pressure test | BMW 17 21 2 248 569 /  |  |
| 8HP cooler-port bore/offset/bolt measurements |  |  |
| Cooler adapter manufacturer/SKU/ports | DomiWorks 22001001 / ORB-8 provisional |  |
| Donor 8HP70 ratio set verified from assembly number |  |  |
| Thermostat model and rated range | BMW 17 22 7 592 723 / MAHLE-BEHR TO 15 80 / opens 80 degrees C |  |
| Hose/fitting specification and minimum bore |  |  |
| Cooler return flow and routing verified |  |  |
| Cold warm-up and loaded temperature results |  |  |

<!-- markdownlint-enable MD060 -->

## References

- BMW E38 workshop information
- BMW and ZF service information for the identified F10 8HP70 assembly
- [BMW part 24 00 7 642 542, GA8HP70Z-WTT](https://www.realoem.com/bmw/enUS/partxref?q=24007642542)
- [F10 LCI 535d GA8HP70Z catalog](https://www.realoem.com/bmw/enUS/showparts?id=5D52-EUR-01-2014-F10N-BMW-535d&diagId=24_1130)
- Driveshaft manufacturer's measurement and installation requirements
- Adamat Performance, Adam Walczak, direct email correspondence regarding an M67-specific 8HP kit
- [Adamat M60/M62/S62 to BMW ZF 8HP45/50/51/70/75 base kit](https://adamat.com.pl/en/adapter-bmw-v8-m62-m60-s62-to-bmw-zf-8hp45-8hp50-8hp51-8hp70-8hp75.html)
- [Adamat M67 flywheel shown in an E38 740d 8HP installation at 6:34](https://www.youtube.com/watch?v=XtBa4phpDPs)
- [RealOEM cross-reference for BMW gearbox support 22 32 1 096 427](https://www.realoem.com/bmw/enUS/partxref?q=22321096427)
- [DomiWorks BMW 8HP transmission identification](https://www.domi-works.com/pages/identify-your-transmission-bmw-8hp)
- [DomiWorks transmission technical information](https://www.domi-works.com/pages/transmission-information)
- [BMW E38 automatic-transmission specifications](https://www.bmwman.ru/en/7er/E38/transmission/automatic/specifikacii-avtomaticheskoy-transmissii)
- [ZF 5HP30 ratio reference](https://gearboxlist.com/zf/5hp30/)
- [ZF 8HP70 ratio reference](https://gearboxlist.com/zf/8hp70/)
- [BMWfans E38 740d oil cooler and cooling pipes](https://bmwfans.info/parts-catalog/E38/Europe/740d-M67/L-A/jul2001/browse/radiator/oil_cooler_oil_cooling_pipe/)
- [DomiWorks Type 1 N47/N57/B58 8HP oil-cooler adapter](https://www.domi-works.com/products/8hp-oil-cooler-adapter-n57)
- [BMWfans BMW 17 22 7 592 723 thermostat, oil cooler line](https://bmwfans.info/parts-catalog/17227592723)
- [BMWfans F80 LCI M3 transmission-oil cooling lines and seals](https://bmwfans.info/parts-catalog/F80N/Europe/M3-S55/L-N/browse/radiator/transmission_oil_cooling/)
- [MAHLE-BEHR TO 15 80 transmission-oil thermostat specification](https://www.autohausaz.com/pn/MH-TO1580)
- [BimmerWorld BMW 17 22 7 592 723 transmission-oil thermostat function and applications](https://www.bimmerworld.com/Driveline-Shifter/Transmission-Service/OEM-Thermostat-for-Transmission-Oil-Cooler-17227592723.html)
- [Mopar 68210018AA cooler-bypass valve](https://store.mopar.com/oem-parts/mopar-cooler-bypass-valve-68210018aa)
- [BMWfans E38 740d driveshaft, centre bearing, and CV joint](https://bmwfans.info/parts-catalog/E38/Europe/740d-M67/L-A/jul2001/browse/drive_shaft/drive_shaft_cen_bearing_const_vel_joint/)
- [SpeedingParts 8HP swap guide](https://www.speedingparts.eu/i/guides-and-information/powertrain/8hp-gearbox-swap.html)
- [Power Test driveshaft phasing guidance](https://powertestdyno.com/proper-driveshaft-phasing-and-alignment/)
