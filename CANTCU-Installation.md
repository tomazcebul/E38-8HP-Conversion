# CANTCU Installation

## Scope

This document covers installation and wiring of CANTCU hardware revision 1.9, serial number 468B, in the E38 740d. It includes power, grounds, transmission wiring, selector integration, CAN wiring, interlocks, reverse lights, and electrical validation.

The [official CANformance CANTCU Installation Manual](https://wiki.canformance.net/CANTCU/installmanual) is the controlling reference. Also use the official pages for the exact [transmission](https://wiki.canformance.net/CANTCU/integrations/supportedtransmissions), [vehicle/ECU integration](https://wiki.canformance.net/CANTCU/integrations/supportedECUs), [shifter](https://wiki.canformance.net/CANTCU/integrations/supportedshifters), and [CANTCU pinout](https://wiki.canformance.net/CANTCU/hardware/CANTCU_pinout). If this guide conflicts with current CANformance documentation, follow CANformance and record the revision used.

Use only the wiring diagram for the exact controller hardware and firmware. Do not infer terminal assignments from another revision. Mechanical work is covered in [Hardware Installation](HW-Installation.md); software setup is covered in [CANTCU Programming and Parameter Tuning](CANTCU-Programming.md).

## Components and Tools

- CANTCU controller and compatible wiring harness
- One complete selector option:
  - Supported BMW F0x/F1x/F2x/F3x 8HP GWS with its 8- or 10-pin connector and mounting parts; or
  - Original E38 Steptronic assembly `25 16 1 423 682` with a custom PRND encoder, input-conditioning circuit, connector, and mounting modifications approved by CANformance
- Brake-pedal signal and optional mode, manual-shift, or paddle switches
- Fuses, relay sockets, and conductors rated for the calculated continuous current, inrush current, and installation temperature
- HELLA `5HE 996 152-131` 12 V adjustable delay-on-release timer, adjusted and bench-verified for at least 60 seconds
- BMW `61 36 8 373 700` white/green 12 V, 30 A make-contact relay and matching socket for the CANTCU/8HP main supply
- Separate 8HP diagnostic OBD connector and BMW DCAN diagnostic cable
- Automotive sealed connectors and suitable power cable
- Twisted-pair CAN wiring
- Crimping tools for the selected automotive terminals
- Digital multimeter and two-channel oscilloscope or CAN diagnostic interface
- BMW wiring diagrams and diagnostic equipment

## 1. Establish the Electrical Baseline

Before modifying the vehicle:

1. Scan all control modules and save the diagnostic report.
2. Verify operation of the engine, charging system, ABS wheel-speed signals, brake switch, instrument cluster, and existing vehicle buses.
3. Photograph wiring routes, connector locations, grounds, and the original selector mechanism.
4. Repair existing faults so they cannot be confused with conversion faults.

## 2. Plan the Installation

Select a dry controller location protected from heat, vibration, water, and physical damage. Plan serviceable harness routes before cutting or terminating wires.

The installation requires:

- Fused main supply for CANTCU and the transmission
- Ignition-switched signal for wake-up control
- Clean power and controller/sensor grounds as specified
- 8HP mechatronics power and communication wiring
- CAN High and CAN Low as a twisted pair
- Brake-pedal input
- Selector position or selector CAN connection
- Manual upshift/downshift inputs, if fitted
- Reverse-light output through a correctly rated relay or vehicle interface
- Park/Neutral start interlock
- Optional mode switch, paddles, display, speed input, and diagnostic connector
- Separate 8HP diagnostic OBD connector on CAN1
- Delayed main-power shutdown so the transmission can save adaptations

Confirm fuse ratings, wire sizes, relay ratings, connector seals, and grounding requirements from the current CANTCU documentation before construction.

### Selector Architecture Decision

CANTCU supports both CAN-bus and configurable input-based shifters, but the two proposed options are not equivalent installations.

<!-- markdownlint-disable MD060 -->

| Requirement | Original E38 Steptronic | BMW F0x/F1x/F2x/F3x 8HP GWS |
| --- | --- | --- |
| CANTCU status | Not listed as a named supported shifter; requires a custom input strategy and written confirmation | Explicitly supported as `BMW F-Series 8HP` |
| PRND command | Custom electrical position encoder required | Native CAN messages |
| Manual mode | Existing Steptronic side gate and `+/-` switches may be reusable after measurement and conditioning | Native GWS Sport/Manual requests over CAN |
| Physical behavior | Stable gated lever positions and an OEM appearance | Monostable joystick with separate Park button |
| Original cable | The 5HP30 Bowden cable cannot select an electronic 8HP range and must not be left attached as a false interlock | Not used |
| Wiring demand | Multiple protected CANTCU inputs; may require both DIN and AIN-to-DIN channels | +12 V, ground, WUP, CAN1 pair, and CAN2 pair |
| Feedback | Original PRND illumination/indication requires a separate design; lever position alone does not prove actual transmission state | Native position LEDs and illumination supported by CANTCU |
| Fabrication | Retains console fit, but needs a fail-safe encoder and revised travel/detents | Needs an engineered console bracket, trim solution, and connector harness |
| Principal risk | Ambiguous or conflicting custom inputs can request the wrong range | Wrong GWS variant, pinout, bus wiring, power behavior, or poor mounting |

<!-- markdownlint-enable MD060 -->

**Preferred functional option:** use a supported F-series 8HP GWS. It has a documented CANTCU interface, conveys complete selector requests, and receives selector indication over CAN. CANformance lists regular and Sport, left- and right-hand-drive variants as supported. Example regular LHD part numbers are `61 31 9 296 904` and `61 31 9 296 896`; these examples do not replace donor-specific verification. Buy the GWS with its connector and a useful length of donor loom, record the BMW number and connector pin count, and confirm it appears in the current firmware before fabricating the console.

**Original-appearance option:** retain the E38 assembly only as the human interface. BMW catalog data identifies complete Steptronic assembly `25 16 1 423 682` and states that it includes the Steptronic switch. The original fore-aft PRND movement selected the 5HP30 mechanically through the transmission selector lever/cable arrangement; the Steptronic `+/-` contacts do not by themselves encode P, R, N, and D for the 8HP. Remove the obsolete transmission cable and add a positive, serviceable electrical encoder for every required range. Do not infer its switch truth table or voltage from another E38/E39: measure this vehicle's assembly against its BMW wiring diagram before designing the interface.

#### Known Builds and Precedent

Research completed in March 2026 found working E38 8HP conversions, but no published conversion in which an original E38 Steptronic assembly is confirmed to command CANTCU or TurboLamik:

- A documented 2001 E38 M57/8HP70 TurboLamik installation uses an F10 selector. The owner modified its housing to fit beneath the E38 leather gaiter, while retaining the later electronic selector mechanism. A commenter proposed adapting the original E38 handle, release button, and indicator board for a stock appearance; the owner described that as a possible future cosmetic change, not the installed control method.
- A separate 2001 E38 S62B50/8HP70 TurboLamik build is documented through installation and road use. Its author still described the display, program switch, and gear lever as unfinished after the car was driving, but the published text does not identify an original E38 selector or provide an E38-selector circuit. Treat it as proof of an E38/TurboLamik powertrain conversion only.
- CANformance's supported-shifter list does not name the E38 or E39 selector. TurboLamik's supported-CAN-selector list names BMW F-series 8- and 10-pin, G-series/Supra, E60 LCI 6HP28, and E84 selectors, but not E38/E39.

Therefore, do not copy an undocumented build or assume that an OEM-looking gaiter proves use of the original mechanism. Until a builder or controller vendor supplies a repeatable schematic, truth table, firmware profile, and fault behavior, classify original E38-selector retention as a custom safety-critical prototype. The supported F-series GWS remains the evidence-based choice for this installation.

The CANTCU input configuration provides `Shifter P`, `Shifter R`, `Shifter N`, `Shifter D`, `Shifter Gear Up`, `Shifter Gear Down`, `Shifter Mode`, and `Park Button` functions. Pins B6, B7, C5, and C6 accept ground only. Pins B2-B5 are 0-5 V analog inputs and can be configured as AIN-to-DIN with selectable thresholds and polarity. Never connect an original 12 V selector or illumination circuit directly to either input type. Use automotive-rated isolation or level conditioning, fusing, defined pull states, and protection against shorts and transients.

Before approving an E38 custom encoder, provide CANformance with the proposed input truth table and confirm the selected firmware/shifter profile. The design must provide one unambiguous request per valid lever position, reject transitions and impossible combinations, default safely after an open circuit or short, and prevent a Park or Reverse request while moving. Verify whether CANTCU's current logic performs each required plausibility and speed check; implement any missing safety independently. Actual transmission state, not lever position, must drive the cluster indication, reverse lamps, and start interlock.

## 3. Install Power, Grounds, and Harness

1. Disconnect the battery according to BMW service procedures.
2. Mount CANTCU in a dry location while retaining access to the USB-B port on its top cover. CANTCU cannot be powered through USB.
3. Connect controller supply to pin A1 and controller ground to pin A8. CANformance recommends a fused 10 A controller supply; for the documented combined CANTCU and 8HP supply, it recommends a 15 A fuse. Follow the exact integration wiring diagram and specified wire sizes.
4. Connect the transmission and shifter wake-up inputs to the CANTCU WUP output on pin C4. WUP must be active only with ignition on.
5. Build a two-stage delayed-off supply using HELLA timer `5HE 996 152-131` to control the coil of BMW relay `61 36 8 373 700`. Set and bench-test the timer for a delay of at least 60 seconds after terminal 15 switches off. The E38 has DDE main and terminal-15 unloader relays, but no genuine BMW relay has been verified as a self-contained delayed-off relay that satisfies this requirement and the circuit load.
6. Connect permanent battery power through the dedicated 15 A fuse to BMW relay contact 30. Connect contact 87 to CANTCU A1 and the 8HP main-power input. Wire the HELLA timer to permanent power and ground, use terminal 15 only as its trigger, and connect its delayed output to the BMW relay coil. The timer carries only coil current; the BMW relay carries the CANTCU/8HP load. Follow the terminal diagram supplied with the actual timer and confirm coil-suppression polarity from the markings on the actual BMW relay before connecting terminals 85 and 86.
7. Keep WUP independent of the retained main-power circuit. At ignition-off, CANTCU C4 must pull WUP low immediately while the BMW relay remains energized for at least 60 seconds so the transmission can save adaptations; the relay must then release without backfeeding terminal 15 or any E38 circuit. Do not add the 8HP load to a DDE or terminal-15 relay output.
8. Treat reuse of an existing vehicle circuit as unapproved unless measurement at the proposed source proves, over repeated hot and cold shutdowns, that WUP falls promptly, the main feed remains at acceptable voltage for at least 60 seconds, and the feed then switches off without backfeeding another E38 circuit.
9. Use pin C2 only as the documented +5 V sensor supply and pin C7 as sensor ground.
10. Route the transmission harness away from exhaust heat, rotating parts, sharp edges, and likely fluid paths.
11. Provide sufficient slack for full drivetrain movement without allowing the harness to rub or hang.
12. Support the harness at suitable intervals and protect all pass-throughs with glands or grommets.
13. Use sealed automotive connectors and approved crimp tooling. Avoid unsupported solder joints in vibration-prone areas.

Do not energize the controller until every supply and ground has been checked for polarity, continuity, short circuits, and expected voltage.

## 4. Connect the Mechatronics and Controls

Wire the 8HP mechatronics connector pin-for-pin from the current CANformance diagram for the exact transmission generation. After inserting the terminals, push the connector center portion outward and lock it with the sleeve; the terminals will not engage the transmission pins if the center remains in its pinning position. Verify connector keying, terminal retention, seals, and strain relief.

Install and verify:

- Brake input with the documented active polarity
- Selector and direction logic
- Manual upshift/downshift inputs or paddles, where fitted
- Mode switch and display, where fitted
- Park/Neutral start-enable output or interface
- Reverse-light output through a suitable relay or vehicle interface

Pins B6, B7, C5, and C6 are ground-triggered digital inputs and must only be switched to ground. Pins B1, B8, C1, and C8 are ground-switching digital outputs rated for a maximum load of 0.5 A each; use a relay for larger loads.

The start interlock must fail safely. The engine must not crank when a drive range is selected. Reverse lamps must follow actual confirmed transmission state rather than an unverified command alone.

### F-Series 8HP GWS Wiring

The supported F-series GWS operates at `500 kbit/s`. For an F-series 8HP transmission, connect it to both CANTCU transmission buses exactly as shown in the current CANformance diagram. CAN1 and CAN2 already have `120 ohm` termination inside CANTCU; measure the completed, unpowered buses and add only the termination required by the documented topology.

<!-- markdownlint-disable MD060 -->

| Function | 10-pin GWS | Early 8-pin GWS | CANTCU connection |
| --- | --- | --- | --- |
| +12 V | 10 | 1 | Fused supply per CANformance diagram |
| Ground | 8 | 5 | Ground |
| Wake-up | 7 | 2 | WUP, CANTCU C4 |
| PTCAN Low | 3 | 3 | CAN1 Low |
| PTCAN High | 4 | 4 | CAN1 High |
| PTCAN2 Low | 5 | 6 | CAN2 Low |
| PTCAN2 High | 6 | 7 | CAN2 High |

<!-- markdownlint-enable MD060 -->

Do not identify the connector by wire color alone. Confirm cavity numbering on the exact housing, preserve twist in each CAN pair, and keep CAN1 and CAN2 as separate networks. Mount the monostable GWS so its full travel, side movement, release-to-center action, Park button, connector, and strain relief operate without console interference.

## 5. Integrate CAN

For the supported BMW E38 integration, use the current CANformance vehicle/ECU integration instructions rather than constructing a universal message map. Confirm support for the M67 DDE variant with CANformance if the exact ECU is not identified on the integration page.

CAN1 and CAN2 are reserved for the transmission and optional 8HP selector; both have built-in 120-ohm termination. CAN3 is used for vehicle/ECU integration and has no built-in termination. Identify the E38 bus used for each required signal and verify voltage levels, bitrate, identifiers, scaling, byte order, and update rate using CANformance documentation or direct measurement.

<!-- markdownlint-disable MD060 -->

| Signal | Proposed source | Verified format/status |
| --- | --- | --- |
| Engine speed | Engine ECU/CAN or conditioned hardwire | To be confirmed |
| Accelerator position/load | Engine ECU/CAN | To be confirmed |
| Brake applied | Brake switch or CAN | To be confirmed |
| Individual/average wheel speed | ABS/DSC | To be confirmed |
| Engine coolant temperature | Engine ECU/CAN | To be confirmed |
| Requested engine torque reduction | CANTCU to engine ECU or alternative strategy | To be confirmed |
| Selected gear/status | CANTCU to display/cluster interface | To be confirmed |
| Reverse selected | CANTCU output | To be confirmed |

<!-- markdownlint-enable MD060 -->

Preserve the twist in CAN High and CAN Low up to each termination point. Avoid unnecessary stubs and route the pair away from ignition and high-current switching circuits.

With every node connected and powered off, measure resistance between CAN High and CAN Low before adding termination. The official interpretation is: 0 ohms indicates a short, 60 ohms is correctly terminated, 120 ohms indicates one terminator, and infinite resistance indicates no terminators. Add termination only at the bus ends and account for CANTCU's built-in termination on CAN1 and CAN2.

Install the mandatory separate 8HP diagnostic OBD connector on CAN1 as shown in the official wiring diagram. Do not substitute the vehicle's existing OBD connector. This connection supports BMW DCAN diagnostics and transmission flashing.

## 6. Electrical Validation

Before first startup:

1. Check supply polarity, voltage, fuse values, grounds, and voltage drop under load.
2. Check for shorts between power, ground, CAN, and all adjacent connector pins.
3. Confirm CAN resistance with the network powered down.
4. Power the controller and confirm communication with CANTCU and the transmission.
5. Check the vehicle network for new bus faults or communication disruption.
6. Verify brake, selector, manual controls, and optional mode inputs in live data.
7. For an F-series GWS, disconnect each CAN pair and WUP in turn and verify that loss of selector communication is detected and cannot produce an unintended range request. For an E38 custom encoder, test every valid position, transition, open circuit, short to ground, conditioned-input short to supply, and conflicting-input combination.
8. Verify the Park/Neutral interlock before permitting engine cranking.
9. Verify reverse-light operation from confirmed transmission state.
10. Verify communication through the separate 8HP diagnostic OBD connector.
11. Switch ignition off and confirm that WUP falls immediately while transmission main power remains available for at least 60 seconds and then switches off.
12. Inspect the complete harness for sealing, support, heat clearance, and drivetrain movement.

Proceed to static commissioning only after loading and checking a conservative configuration as described in [CANTCU Programming and Parameter Tuning](CANTCU-Programming.md).

## Electrical Acceptance Checklist

- [ ] Hardware revision, serial number, and firmware recorded
- [ ] Harness pinout checked against current CANTCU documentation
- [ ] Supplies fused and polarity verified
- [ ] WUP controlled by CANTCU and delayed power-off verified
- [ ] Grounds and loaded voltage drops accepted
- [ ] Harness secured, sealed, and protected from heat and abrasion
- [ ] CAN resistance and signal integrity accepted
- [ ] CAN communication stable with no new bus faults
- [ ] Selector option, BMW part number, connector, CANTCU profile, and firmware support recorded
- [ ] Selector direction and indicated state agree
- [ ] Selector communication/input fault tests produce no unintended range request
- [ ] Brake signal and manual controls operate correctly
- [ ] Park/Neutral start interlock operates correctly
- [ ] Reverse lights operate correctly
- [ ] Separate CAN1 diagnostic OBD connector operates correctly

## Electrical and CAN Record

<!-- markdownlint-disable MD060 -->

| Circuit/signal | CANTCU pin | Vehicle connection | Notes |
| --- | --- | --- | --- |
| Controller ground | A8 |  |  |
| Controller supply | A1 |  | 10 A fused, or per combined-supply diagram |
| Timer permanent input |  | Battery distribution point | Separately fused for the timer and relay-coil circuit according to component and conductor ratings |
| Timer ignition trigger |  | Verified terminal-15 signal | Trigger only; must not carry timer supply, relay-coil current, or CANTCU/8HP load current |
| BMW relay contact 30 |  | Battery distribution point through dedicated 15 A fuse | Combined CANTCU/8HP feed per CANformance diagram |
| BMW relay contact 87 | A1 plus 8HP power input | Timed main-power output | Retained at least 60 seconds after WUP falls, then switched off |
| BMW relay coil |  | HELLA delayed output and ground | Record terminals 85/86 after confirming suppression-device polarity |
| Ignition state source |  |  | Defines CANTCU wake-up behavior |
| Transmission/shifter WUP | C4 |  | Ignition-on wake-up |
| +5 V sensor supply | C2 |  | Sensors only |
| Sensor ground | C7 |  |  |
| CAN High |  |  |  |
| CAN Low |  |  |  |
| Separate diagnostic OBD | CAN1 |  | Mandatory for 8HP diagnostics/flashing |
| Brake input |  |  |  |
| Reverse output |  |  |  |
| Park/Neutral output |  |  |  |
| Selector type/profile |  |  | E38 custom inputs or F-series 8HP GWS |
| Selector BMW part/connector |  |  |  |
| Selector +12 V/ground/WUP | C4 for WUP |  | F-series GWS only |
| Selector CAN1 H/L | CAN1 |  | F-series GWS only |
| Selector CAN2 H/L | CAN2 |  | F-series GWS only |
| E38 PRND input mapping/truth table | DIN/AIN-to-DIN |  | E38 custom option only |
| Upshift/downshift |  |  |  |

<!-- markdownlint-enable MD060 -->

## References

- [CANformance CANTCU Installation Manual](https://wiki.canformance.net/CANTCU/installmanual) - controlling reference
- [CANformance BMW 8HP second-generation F-Series integration](https://wiki.canformance.net/CANTCU/integrations/supportedtransmissions/bmw8hpfgen2) - applies if the donor is confirmed as this 8HP50 generation
- [CANformance CANTCU pinout](https://wiki.canformance.net/CANTCU/hardware/CANTCU_pinout)
- [CANformance supported ECUs and BMW E38 integration](https://wiki.canformance.net/CANTCU/integrations/supportedECUs)
- [CANformance supported shifters](https://wiki.canformance.net/CANTCU/integrations/supportedshifters)
- [CANformance BMW F-Series 8HP shifter](https://wiki.canformance.net/CANTCU/integrations/supportedshifters/Fxx-8HP)
- [CANformance input configuration](https://wiki.canformance.net/CANTCU/software/config/inputcfg)
- [TurboLamik supported CAN selectors](https://manual.turbolamik.eu/docs/general-info/supported-can-selectors/)
- [E38 M57/8HP70 TurboLamik selector installation](https://www.drive2.ru/l/689594727439276122/)
- [E38 M57/8HP70 TurboLamik installation discussion](https://www.drive2.ru/l/683394856248160840/)
- [E38 S62B50/8HP70 TurboLamik build, part 7](https://www.drive2.ru/l/655787493664229650/)
- [BMW E38 740d Steptronic shift parts](https://www.realoem.com/bmw/enUS/showparts?id=GE81-EUR-07-2001-E38-BMW-740d&diagId=25_0264)
- BMW E38 wiring diagrams
- ZF connector information for the identified 8HP50Z assembly
- Local vehicle modification and inspection regulations
