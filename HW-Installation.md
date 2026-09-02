# Hardware Installation

## Scope

This document covers the mechanical installation of the ZF 8HP50Z in the 2001 BMW E38 740d: removal, trial fitting, engine adapter and converter interface, mounts, driveshaft, cooling, final assembly, and mechanical validation.

Read the project overview and record the exact donor transmission and converter identities in [Introduction](Introduction.md) before ordering conversion parts. CANTCU wiring and configuration are covered separately in [CANTCU Installation](CANTCU-Installation.md) and [CANTCU Programming and Parameter Tuning](CANTCU-Programming.md).

> [!WARNING]
> Fabrication, welding, driveshaft modification, and drivetrain alignment affect road safety. Use suitably qualified specialists and comply with local inspection requirements.

## Components

- Complete 8HP50Z with matched mechatronics, oil pan, connector, and torque converter
- Engine-to-transmission adapter plate
- Original M67-specific starter and M67 flexplate/ring gear, subject to inspection and dimensional validation
- Modified or custom crankshaft-to-converter adapter for the retained M67 components
- Converter bolts, bellhousing bolts, dowels, and all safety-critical fasteners
- Original BMW E38 gearbox support `22 32 1 096 427`
- Custom 8HP50Z-to-OEM-support adapter and correctly rated transmission mounts
- Professionally fabricated two-piece driveshaft, dynamically balanced as a complete assembly
- Output flange installed on the exact donor 8HP50Z, matching RWD F3x transmission-end coupling, and E38 rear section with differential-end CV joint
- Serviceable OEM E38 transmission oil cooler or a suitably rated replacement
- Donor-specific 8HP50 oil-port adapter with compatible seals and fittings
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

## 3. Trial-Fit the 8HP50Z

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

### Selected M62-to-8HP Adapter Basis for the M67

Research completed on 29 August 2026 did not find an OEM drawing, shared converter-housing part number, or measured coordinate comparison proving that the M67 bellhousing bolt-and-dowel pattern is identical to the M60/M62 pattern. Subsequent correspondence with PMC provides customer-history context but does not confirm dimensional compatibility.

On 30 August 2026, James Scott Foley provided a firsthand account of the adapter used for his publicly shown M67D44/8HP75 conversion in response to a Facebook 8HP swap-group question:

> For the adapter I got one for M62 from PMC, and modified it to suit. The bolt pattern was ok, but I had to machine for the starter, make some custom nuts and modify the spacer they provided.

Foley's [8HP swap-group post and comments](https://www.facebook.com/groups/zf8hpswaptech/permalink/1037322348805229/) identify the build as an E65 M67D44 installed in an E46 coupe with an 8HP75 and a 25 mm-thick PMC adapter. He states that the adapter fits, but the starter opening required machining and the crank-position sensor sat too far out. The thread does not answer whether the stock M67 flexplate was used.

The supplied flexplate spacer reportedly clamped the torque converter between the crankshaft and transmission and required machining. The account does not provide a verified final spacer dimension or converter pull-forward specification. It also reports a torque-converter-area rattle after startup, so it does not prove that the final rotating interface was correct or undamaged.

This is practical evidence that the PMC M62 adapter bolt pattern was usable on one M67D44/8HP75 build. It also confirms that the kit was not a direct-fit solution: starter machining, custom fasteners, crank-sensor correction, and spacer modification were required. No drawing, runout result, final pull-forward measurement, transmission assembly number, or converter part number was provided. Because this project uses an earlier M67B39 and an 8HP50Z, treat this as evidence from one modified M67D44 installation, not as verification of M67-family or M67B39 compatibility.

Establish the correct installed converter clearance and pull-forward from documentation for the exact converter, flexplate, adapter, and transmission. Reject any stack-up that clamps the converter when the bellhousing is tightened or leaves inadequate pump engagement.

#### PMC Manufacturer Response

In an email received on 30 August 2026, PMC representative Norbert Borkowski stated that PMC knows of two customers who used its M62 adapter kit for an M67 swap. Those customers did not share installation details, so PMC cannot confirm whether modifications were required or whether every flange bolt fitted the M67.

James Scott Foley is likely one of those two customers because his documented build used the same PMC M62 adapter for an M67D44 swap. PMC did not identify its customers in the correspondence, so this overlap is probable but unconfirmed. Count the available evidence as two reported PMC customer swaps in total, not as PMC's two reports plus Foley as a third independent installation.

PMC described the M67 V8 diesel pattern as unique to that engine family and said the M62 flange might fit because PMC designs its flanges to cover multiple engines where possible. PMC explicitly identified torque-converter offset as unresolved because it lacks data for the rare M67 application. This is not manufacturer approval of M67 compatibility.

PMC offered to accept a return after a careful test-fit if the kit proves incompatible, provided it is not marked. Confirm the current return conditions in writing before ordering. A non-marking test-fit may indicate bolt alignment but cannot validate converter offset, dowel registration, starter geometry, crank-sensor position, or running concentricity.

DomiWorks reports that all seven 8HP50/51 variants it has identified, including the F-series B58 8HP50, share the small bellhousing pattern commonly called the N57 pattern. It also records a flat converter mounting face with six M10 fasteners and a 32 mm guide nose for this family. This supports transmission-side compatibility with an adapter designed for the N57-pattern 8HP family.

A shared transmission pattern does not establish the M67 crank register, flywheel attachment, starter/ring-gear geometry, crank-sensor operation, converter pilot engagement, or axial spacing. Treat the PMC product below as **unconfirmed for the M67** until those engine-side details are verified.

**PMC:** The [PMC Motorsport product 5072](https://pmcmotorsport-shop.com/product-eng-5072-Adapter-kit-BMW-V8-M62-BMW-ZF-8HP-8HP75-8HP70.html), symbol `A-M62-8HP`, has a manufacturer-published gearbox-adapter thickness of `25 mm` (`0.98 in`). PMC specifies M62B35/M62B44/M62B46 and S62B50 engines with N57/N57N 8HP70, N57/N57N 8HP70X, and B57 8HP75 transmissions. The product specification does not list the M67 or B58 8HP50, although PMC's installation diagram is captioned for B58 8HP50/51 as well as N57/N57N2 8HP70/75/76. DomiWorks' identification data independently places the B58 GA8HP50Z in the same N57-pattern bellhousing family.

PMC's advertised M62 configuration specifies M60/M62 starter `12 41 1 729 981` or `12 41 1 736 921` and M62 flexplate/ring gear `11 22 1 435 235` or `11 22 1 741 143`. Those parts are not the project specification: BMW catalogs the starter and flexplate/ring gear as M67-specific components, and this conversion will retain the M67 parts. Consequently, the supplied PMC starter opening, crankshaft-position-sensor adapter, torque-converter adapter, spacer, and associated fasteners must be treated as modification inputs rather than direct-fit parts.

The listed PMC kit contents are the aluminium gearbox adapter, gearbox-adapter bolts, torque-converter adapter, crankshaft-bolt kit, and crankshaft-position-sensor adapter. Its instructions describe an M62 automatic flexplate with an N57 torque converter and show bellhousing cutting for starter clearance. That assembly procedure cannot be transferred unchanged to the M67. Establish the M67 starter position and engagement, M67 ring-gear position, crank-sensor geometry, converter pilot engagement, and complete axial stack by measurement before machining or final assembly.

PMC reports two customer M67 swaps using this kit but cannot confirm modifications, complete bolt fit, or converter offset. Foley, likely one of those two customers, supplies one detailed M67D44/8HP75 precedent for modifying the 25 mm kit, including starter machining, custom nuts, crank-sensor-position correction, and spacer correction. His reported thickness now agrees with PMC's published specification, but the exact M67B39 geometry and 8HP50 converter interface remain to be established for this project.

Use the 25 mm PMC kit as the project basis because its shorter axial package is preferable to the previously considered 50 mm alternative. This selection does not establish compatibility. The kit is not documented as a direct-fit M67B39/8HP50 solution, so do not approve it for final installation until the required modifications and compatibility with `M67B39`, the transmission assembly number, and the torque-converter number are established.

Request a drawing or written values for:

1. Engine-side adapter bolt and dowel coordinates, dowel diameters, and register diameter/depth.
2. Crankshaft bolt count, pitch-circle diameter, fastener size, locating register, flange stand-off, and flywheel mounting-face offset.
3. Flywheel/flexplate part used, ring-gear tooth count and axial position, required starter part number and mounting position, and pinion engagement.
4. Crankshaft-sensor type, target pattern, tooth count, index angle, air gap, and whether the M67 DDE can retain its original speed/reference signal.
5. Exact compatible 8HP50 converter, converter pilot diameter/depth, mounting pattern, installed clearance, and specified pull-forward distance.
6. Adapter thickness, bellhousing modifications, fastener lengths and grades, access for converter bolts, and required machining.
7. Maximum rated engine torque and whether the supplied flywheel has been balanced independently or with a specified converter/crank assembly.

If the vendor confirms only the bellhousing bolt pattern, the kit remains unapproved. The quickest conclusive pattern check is to trace or scan the rear face of the bare M67 block and compare its bolt centers, dowels, starter opening, and crank center with an M60/M62 adapter drawing. Alternatively, offer the original M67 5HP30 converter housing to the adapter supplier for direct coordinate measurement.

## 5. Fabricate the Transmission-Support Adapter and Driveshaft

Retain the original BMW E38 gearbox support `22 32 1 096 427` at the body-side mounting points. BMW catalog data identifies it as an E38 gearbox support used from April 1999; its listed weight is `1.176 kg`. Fabricate an intermediate adapter between the 8HP50Z transmission-mount interface and this OEM support rather than replacing the support with a fully custom crossmember.

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

Published BMW E38 and transmission-reference data give the following internal ratios for the A5S 560Z / ZF 5HP30 and the second-generation ZF 8HP50. Record the exact donor assembly number and confirm its ratio set from ZF or BMW data before entering ratios in CANTCU.

<!-- markdownlint-disable MD060 -->

| Gear | 5HP30 ratio | 5HP30 overall with 2.65 final drive | 8HP50 ratio | 8HP50 overall with 2.65 final drive |
| --- | ---: | ---: | ---: | ---: |
| 1 | 3.550 | 9.408 | 5.000 | 13.250 |
| 2 | 2.240 | 5.936 | 3.200 | 8.480 |
| 3 | 1.540 | 4.081 | 2.143 | 5.679 |
| 4 | 1.000 | 2.650 | 1.720 | 4.558 |
| 5 | 0.790 | 2.094 | 1.314 | 3.482 |
| 6 | - | - | 1.000 | 2.650 |
| 7 | - | - | 0.822 | 2.178 |
| 8 | - | - | 0.640 | 1.696 |
| Reverse | 3.680 | 9.752 | 3.456 | 9.158 |

<!-- markdownlint-enable MD060 -->

The 8HP50 first gear is `40.8%` shorter than the 5HP30 first gear with the same final drive, increasing torque multiplication at launch. Its eighth gear gives `19.0%` lower engine speed than the 5HP30 fifth gear at the same road speed, ignoring converter slip. Direct drive moves from fourth gear in the 5HP30 to sixth gear in the 8HP50. The forward-ratio span increases from approximately `4.49` to `7.81`.

These ratios do not by themselves determine shift points, launch traction, converter behavior, maximum road speed, or acceptable output-shaft speed. Confirm tyre rolling circumference, engine speed range, converter characteristics, and the exact donor ratio set when configuring and validating CANTCU.

### Transmission Length Comparison

Research completed on 30 August 2026 found one usable 8HP50 measurement but no reliable same-datum published length for the E38 740d A5S 560Z / ZF 5HP30:

- DomiWorks' technical-information table lists `682.9 mm` from the bellhousing mating plane to the output-flange mating plane for a BMW B58 RWD generation-2 8HP50. That table labels the entry G-series, while DomiWorks' identification page lists the B58 8HP50 under F-series applications. Because the source is internally inconsistent on platform, use the dimension only as an indicative packaging value and do not use the platform label to identify the donor.
- The ZF 5HP30 spare-parts catalog and other located public sources do not state an equivalent external length. Parts diagrams are not dimensioned and must not be scaled.
- The `682.9 mm` value is not a universal 8HP50 specification. The exact donor assembly remains unidentified, so its length must also be measured.

Measure both transmissions between the same reference planes: place a straightedge across the engine mating face and measure parallel to the transmission axis to the propshaft-coupling face of the installed output flange. Record the flange fitted to each transmission because flange height changes this result.

For installation planning, adapter thickness moves the 8HP output farther rearward relative to the engine. As a first-order comparison:

$$
\Delta L = (L_{\mathrm{8HP50}} + t_{\mathrm{adapter}}) - L_{\mathrm{5HP30}}
$$

For PMC product 5072, use `25 mm` as the nominal published adapter thickness for preliminary packaging only. Measure the received adapter and use the actual assembled axial stack for final calculations.

Confirm the actual output-flange position by trial-fitting the complete adapter, transmission, mounts, and retained donor flange. Account separately for any register, spacer, or engine-side geometry that changes the effective axial stack. Do not order or cut the driveshaft from published transmission lengths alone.

Because the effective 8HP50Z output position is not yet established, measure the installed drivetrain before fabricating the driveshaft. Retain the donor 8HP50Z output flange. The selected solution is a professionally fabricated two-piece hybrid driveshaft that retains as much of the OEM E38 assembly as practicable, including the rear CV joint, centre joint, centre support and bearing, and rear shaft section. Adapt only the forward section using the transmission-end portion of a rear-wheel-drive F3x driveshaft matched to the retained flange.

Finalize the engine mounts, OEM support position, custom support adapter, transmission mounts, and differential position first. With the vehicle at normal ride height, measure the required installed length between the 8HP50Z coupling face and rear differential interface using the driveshaft fabricator's specified datums and allowance. Supply the specialist with the complete E38 shaft and the matching RWD F3x 8HP50 donor shaft. The specialist must establish cut positions, tube overlap or replacement, joint phasing, centre-bearing preload and position, spline engagement and plunge allowance, critical speed, torque capacity, runout, weld design, reinforcement, and final installed length. Dynamically balance the complete two-piece assembly together after all welding and refurbishment.

The E38 740d catalog identifies two different driveshaft end interfaces. At the transmission end it lists universal joint `26 11 7 572 664`, specified as `LK=110MM/12`, with three M12 fasteners. At the differential end it lists constant-velocity joint with knurled bush `26 11 1 229 772`, specified as `LK=94MM (Z=34)`, with six M10 fasteners. Do not describe the rear connection as a 110 mm flange; the `110 mm / M12` specification belongs to the transmission-end coupling.

DomiWorks lists a 105 mm output-flange bolt circle with 22 mm inserts for the B58 RWD 8HP50 entry. Confirm the flange dimensions on the exact donor and select a matching RWD F3x transmission-end driveshaft section. Retain the E38 rear section and its `94 mm` CV-joint interface at the differential unless inspection or the driveshaft specialist requires replacement.

### Rejected Output-Flange Substitutions

Research completed on 29 August 2026 does **not** support fitting the original 5HP30 flange to the 8HP50Z. The E38 740d catalog identifies its output flange as BMW `24 20 1 423 752`; this diesel E38-specific 2.19 kg part is listed for the 730d and 740d, with no 8HP application or supersession. It is not the gasoline-E38 5HP30 flange `24 20 1 422 521`.

The 5HP30 catalog places `24 20 1 423 752` in an output assembly with drive extension `24 13 1 422 520`, 57 x 73 x 8 mm shaft seal `24 13 1 422 667`, ring nut `24 20 1 421 170`, and selective adjusting plates. Documented replacement flanges for the RWD 8HP45/50/70/75 family have 43 internal splines; one measured listing is 78 mm high. No BMW, ZF, or transmission-parts source cross-references the 5HP30 flange to that family.

The original 5HP30 flange is not interchangeable with the 8HP50Z on the available evidence and is not part of the selected design.

BMW 110 mm 8HP output-flange kit `24 20 7 604 955`, superseded by `24 00 8 743 416`, was also evaluated. BMW catalogs it for N63 8HP70Z and N74 8HP90Z applications, but no BMW fitment record confirms it for the exact donor 8HP50Z. Substituting this flange would also change the axial stack and require validation of splines, retention, seal journal, installed height, housing clearance, and coupling geometry. Because the custom driveshaft can use a transmission-end section matched to the donor flange, the 110 mm substitution adds risk without a defined engineering benefit and is rejected for this design.

### Professional 8HP/E38 Driveshaft Fabrication

The intended construction preserves the OEM E38 rear and centre assemblies and replaces only the required length at the gearbox end with the matching F3x 8HP50 front section. A qualified driveshaft specialist must select the exact cut locations and specify the joint, sleeve, tube, weld, and reinforcement design; do not prescribe reinforcement dimensions without the fabricator's material, load, and balancing data.

1. Select a rear-wheel-drive F3x donor shaft from the same output-flange family as the exact 8HP50Z. Record the donor VIN and complete part number. Do not use an xDrive front propshaft.
2. Give the complete F3x and E38 shafts to the specialist for assessment before either is cut.
3. Install the complete drivetrain in its final mounted position and measure between the gearbox and differential at normal ride height, following the fabricator's required reference points and working-length allowance.
4. Preserve the E38 rear shaft section, rear CV joint, centre joint, centre support, bearing, and their vehicle mounting relationship unless inspection shows that a component is unserviceable.
5. Cut the E38 shaft only toward the front, gearbox end, at the location selected by the specialist.
6. Cut or re-tube the matching F3x front shaft section to produce the required overall installed length and correct 8HP50Z gearbox connection.
7. Add sleeves, tube transitions, weld preparation, and other reinforcements required by the fabricator's approved process for the shaft materials, diameters, M67 torque, and calculated maximum shaft speed.
8. Establish joint phasing from actual joint geometry. Maintain correct spline engagement, plunge allowance, centre-bearing position and preload, and clearance through the full drivetrain movement range.
9. Inspect CV joint `26 11 1 229 772`, its boot and lubricant, the `94 mm` differential flange, 34-tooth interface, six M10 knurled bolts, mating nuts, and sealing washer. Replace worn or damaged components.
10. Inspect every retained joint, spline, bearing, carrier, boot, seal, tube, and fastener. Replace parts that exceed the applicable wear, damage, or runout limits; clean, lubricate, and refurbish accepted parts according to their specifications.
11. After all fabrication and refurbishment, check straightness and runout and dynamically balance the complete two-piece driveshaft as one indexed assembly, including the centre support arrangement. Mark the balanced orientation and obtain the fabricator's maximum-speed and torque rating.

> [!CAUTION]
> A poorly aligned or unbalanced driveshaft can damage the transmission and differential and can fail dangerously at road speed.

## 6. Install Transmission Cooling

### Selected Cooling Architecture

The July 2001 E38 740d has a dedicated transmission-oil cooler circuit rather than the engine-coolant heat exchanger used by many F-series 8HP donor installations. BMW catalog data identifies:

- Oil cooler `17 21 2 248 569`
- A5S 560Z cooler inlet pipe `17 22 2 248 641`
- A5S 560Z cooler outlet pipe `17 22 2 248 642`
- Four FPM O-rings `17 21 1 742 636`, size `10.82 x 1.78 mm`

Retain the E38 air-to-oil cooler only if it passes inspection, pressure testing, and a professional contamination assessment. The original rigid pipes are transmission-specific and should not be forced onto the 8HP50. Replace or modify them with correctly supported ATF hose assemblies. If the 5HP30 failed internally or the cooler cannot be verified clean, replace the cooler and contaminated lines rather than risking debris entering the 8HP50.

The selected circuit is:

```text
8HP50 hot outlet -> full-flow bypass thermostat -> E38 oil cooler -> thermostat -> 8HP50 return
```

Follow the markings and installation diagram supplied with the chosen adapter and thermostat; confirm the 8HP50 outlet and return ports instead of inferring direction from physical position. The thermostat must bypass the cooler during warm-up while preserving an unrestricted return path to the transmission.

### 8HP50 Cooler Adapter

Use an adapter made for the exact donor transmission casting. DomiWorks Type 1, SKU `22001001`, is the provisional choice only if donor inspection confirms its specified interface. Its published specification is:

- 8HP50 B58, 8HP70 N57, and 8HP45 N47 application
- `17 mm` offset transmission bores with an M6 retaining bolt
- Two female `ORB-8` ports, `3/4-16 UNF`
- Supplied bolt and O-rings; hose-end fittings are optional

DomiWorks states that BMW 8HP cooler-port bore size, offset, and retaining-bolt geometry vary among transmissions. Before ordering, measure the exact donor's bore diameters, centre spacing/offset, bolt size and position, sealing arrangement, and available tunnel clearance. Confirm the choice with the adapter manufacturer using the donor tag and photographs.

PMC `OC-BMW8HP` is an alternative published for BMW B58 8HP50, N57/N57N 8HP70, and B57 8HP76. It converts the transmission interface to two `M18x1.5-to-AN10` fittings. Treat this as a separate plumbing system: do not combine PMC's M18/AN10 parts with DomiWorks ORB-8 parts without deliberately specified reducers and a flow review.

### Thermostat and Lines

Use BMW `17 22 7 592 723` / MAHLE-BEHR `TO 15 80`, a four-port, full-flow bypass thermostat, in this standalone air-to-oil circuit to shorten cold warm-up and prevent over-cooling. The shortened marking `7 592 723-02` or `759272302` on a used housing is a casting or production-revision marking, not the complete orderable BMW number. BMW-derived catalogs identify the assembly as "Thermostat, oil cooler line," and MAHLE-BEHR specifies an `80 degrees C` opening temperature. Published applications include BMW M-DCT vehicles and xDrive automatic-transmission vehicles; application history alone does not establish compatibility with this standalone 8HP50 circuit.

The purchased thermostat includes the associated F80 LCI M3 GS7D36SG cooler lines. BMW catalogs the relevant flow and return sections as `17 22 2 284 548` and `17 22 2 284 549`. Their two gearbox-end connections use FPM O-rings `17 21 1 742 636`, specified as `10.82 x 1.78 mm`, and are retained together by one M8 x 28 screw `17 22 7 555 715`. The O-ring dimensions mean `10.82 mm` inside diameter and `1.78 mm` cross-section, giving a free outside diameter of `14.38 mm`; this indicates an approximately 14 mm-class GS7D36SG interface but does not specify its machined bore or spigot diameter.

These DCT gearbox ends do not match the provisional DomiWorks adapter's `17 mm` 8HP50 bores. Retain the purchased lines as thermostat-end connection hardware only if their condition and routing are acceptable, and replace or adapt their DCT ends with purpose-made transitions for the selected 8HP50 adapter. Do not force the DCT ends into the 8HP50 ports or treat the O-ring's `14.38 mm` free outside diameter as an adapter machining dimension. Record the measured DCT end and 8HP50 adapter interfaces before specifying transitions.

The BMW housing incorporates a thermostatic flow-control/bypass function as well as joining the cooler lines; used-parts descriptions that call it a junction block do not mean it is passive. Because it is an OEM thermostat used in the F80 M3 transmission-oil circuit, separate calibrated hydraulic characterization is not required for this conversion. The custom plumbing must still reproduce the original flow and return routing without introducing restrictive adapters. Before installation:

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
- [ ] Cooler flow, fluid level, and operating temperature verified
- [ ] No leaks, abnormal noise, driveline vibration, or clutch slip
- [ ] Post-test fastener, mount, driveshaft, and fluid inspection completed

## Mechanical Build Record

<!-- markdownlint-disable MD060 -->

| Measurement | Value | Method/date |
| --- | --- | --- |
| Adapter plate thickness |  |  |
| Crank register diameter |  |  |
| Converter pilot diameter/depth |  |  |
| Converter pull-forward distance |  |  |
| Bellhousing runout |  |  |
| Flexplate/converter runout |  |  |
| Original 5HP30 mating-face-to-output-flange length |  |  |
| Donor 8HP50 mating-face-to-output-flange length |  |  |
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
| F3x donor VIN/driveshaft part number |  |  |
| E38 rear/centre assembly condition |  |  |
| Gearbox-to-differential measured length and datums |  |  |
| E38 and F3x forward-section cut locations |  |  |
| Tube joint, weld, and reinforcement specification |  |  |
| Centre-bearing mount position/preload |  |  |
| Final installed driveshaft length |  |  |
| Dynamic-balance report and indexed orientation |  |  |
| Fabricator maximum-speed/torque rating |  |  |
| Front/rear driveline angles |  |  |
| E38 cooler part/condition/pressure test | BMW 17 21 2 248 569 /  |  |
| 8HP cooler-port bore/offset/bolt measurements |  |  |
| Cooler adapter manufacturer/SKU/ports | DomiWorks 22001001 / ORB-8 provisional |  |
| Donor 8HP50 ratio set verified from assembly number |  |  |
| Thermostat model and rated range | BMW 17 22 7 592 723 / MAHLE-BEHR TO 15 80 / opens 80 degrees C, validation pending |  |
| Hose/fitting specification and minimum bore |  |  |
| Cooler return flow and routing verified |  |  |
| Cold warm-up and loaded temperature results |  |  |

<!-- markdownlint-enable MD060 -->

## References

- BMW E38 workshop information
- ZF service information for the identified 8HP50Z assembly
- Driveshaft manufacturer's measurement and installation requirements
- [PMC Motorsport M62 to 8HP70/8HP75 adapter kit](https://pmcmotorsport-shop.com/product-eng-5072-Adapter-kit-BMW-V8-M62-BMW-ZF-8HP-8HP75-8HP70.html)
- [RealOEM cross-reference for BMW gearbox support 22 32 1 096 427](https://www.realoem.com/bmw/enUS/partxref?q=22321096427)
- [DomiWorks BMW 8HP transmission identification](https://www.domi-works.com/pages/identify-your-transmission-bmw-8hp)
- [DomiWorks transmission technical information](https://www.domi-works.com/pages/transmission-information)
- [BMW E38 automatic-transmission specifications](https://www.bmwman.ru/en/7er/E38/transmission/automatic/specifikacii-avtomaticheskoy-transmissii)
- [ZF 5HP30 ratio reference](https://gearboxlist.com/zf/5hp30/)
- [ZF 8HP50 ratio reference](https://gearboxlist.com/zf/8hp50/)
- [BMWfans E38 740d oil cooler and cooling pipes](https://bmwfans.info/parts-catalog/E38/Europe/740d-M67/L-A/jul2001/browse/radiator/oil_cooler_oil_cooling_pipe/)
- [DomiWorks Type 1 N47/N57/B58 8HP oil-cooler adapter](https://www.domi-works.com/products/8hp-oil-cooler-adapter-n57)
- [PMC OC-BMW8HP N57/B58 oil-cooler adapter](https://pmcmotorsport-shop.com/product-eng-6512-Oil-Cooler-Adapter-for-ZF-8HP-BMW-N57-B58-Transmission-M18x1-5-AN10-Adapters.html)
- [BMWfans BMW 17 22 7 592 723 thermostat, oil cooler line](https://bmwfans.info/parts-catalog/17227592723)
- [BMWfans F80 LCI M3 transmission-oil cooling lines and seals](https://bmwfans.info/parts-catalog/F80N/Europe/M3-S55/L-N/browse/radiator/transmission_oil_cooling/)
- [MAHLE-BEHR TO 15 80 transmission-oil thermostat specification](https://www.autohausaz.com/pn/MH-TO1580)
- [BimmerWorld BMW 17 22 7 592 723 transmission-oil thermostat function and applications](https://www.bimmerworld.com/Driveline-Shifter/Transmission-Service/OEM-Thermostat-for-Transmission-Oil-Cooler-17227592723.html)
- [Mopar 68210018AA cooler-bypass valve](https://store.mopar.com/oem-parts/mopar-cooler-bypass-valve-68210018aa)
- [BMWfans E38 740d driveshaft, centre bearing, and CV joint](https://bmwfans.info/parts-catalog/E38/Europe/740d-M67/L-A/jul2001/browse/drive_shaft/drive_shaft_cen_bearing_const_vel_joint/)
- [RealOEM E38 740d A5S560Z output assembly](https://www.realoem.com/bmw/enUS/showparts?id=GE81-EUR-01-2001-E38-BMW-740d&diagId=24_0703)
- [Hubauer BMW 24 20 1 423 752 application](https://www.hubauer-shop.de/en/output-flange-24201423752.html)
- [BMWfans E38 740d A5S560Z output assembly](https://bmwfans.info/parts-catalog/E38/Europe/740d-M67/L-A/browse/automatic_transmission/a5s560z_output/)
- [BMWfans N74 GA8HP90Z output catalog](https://bmwfans.info/parts-catalog/F01/Europe/760i-N74/L-A/browse/automatic_transmission/ga8hp90z_output/)
- [Hubauer BMW 110 mm output-flange kit](https://www.hubauer-shop.de/en/repair-kit-output-flange-24207604955.html)
- [Hubauer BMW 105 mm output-flange kit](https://www.hubauer-shop.de/en/repair-kit-output-flange-24207604961.html)
- [Hubauer shared GA8HP70Z output-retention kit](https://www.hubauer-shop.de/en/repair-kit-output-24207588897.html)
- [Maktrans shared 43-spline 8HP output flange](https://maktrans.net/output-shaft-flange-zf-8hp45-8hp50-8hp70-8hp75-height-78-mm-43-splines-4-mounting-holes-intoe-995-mm-8hp-flg-4h995)
- [SpeedingParts 8HP swap guide](https://www.speedingparts.eu/i/guides-and-information/powertrain/8hp-gearbox-swap.html)
- [Power Test driveshaft phasing guidance](https://powertestdyno.com/proper-driveshaft-phasing-and-alignment/)
- James Scott Foley, direct Facebook response regarding his M67D44/8HP75 conversion, received 30 August 2026
- [James Scott Foley's M67D44/8HP75 fitment post and comments in ZF 8HP Transmission Swap & Tech](https://www.facebook.com/groups/zf8hpswaptech/permalink/1037322348805229/)
- Norbert Borkowski, PMC, email correspondence regarding M67 use of PMC product 5072, received 30 August 2026
