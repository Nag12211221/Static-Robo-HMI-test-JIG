# Static-Robo-HMI-test-JIG

This repository documents a starting plan for building a static robotic HMI test jig similar to the supplied reference fixture: a rigid aluminum-frame test station with modular connector panels, routed harnessing, alignment hardware, and an electrical control/test system.

## 1. Define the Goal

- Decide exactly what the jig must validate before designing the hardware.
- Typical test coverage:
  - HMI push buttons and switches
  - Panel connectors
  - Continuity between connector pins
  - Short-circuit detection
  - 24 VDC and low-voltage power rails
  - Current draw
  - Sensor inputs
  - Signal routing
  - Communication lines
  - LED, buzzer, or output response
  - Full functional HMI operation
- Create a device/interface list:
  - HMI unit under test
  - Power input connector
  - Communication connector
  - Button/switch connector
  - Sensor connector
  - Output connector
  - Ground/chassis connection
  - Programming/debug connector, if required
- Create a connector pinout table for every connector before wiring.

Example pinout table:

| Connector | Pin | Signal | Voltage/Current | Test Method | Pass/Fail Condition |
| --- | --- | --- | --- | --- | --- |
| J1 Power | 1 | +24 VDC | 24 VDC / rated load | Measure voltage | 23-25 VDC |
| J1 Power | 2 | 0 VDC | Return | Continuity check | < 1 ohm to 0 V bus |
| J2 IO | 1 | Button input 1 | 24 VDC input | Toggle input | Controller detects state change |
| J2 IO | 2 | LED output 1 | 24 VDC output | Command output | LED/output turns on |

## 2. Study the Reference Design

- Treat the fixture as a modular electrical test jig, not only a mechanical frame.
- Key design features visible in the reference image:
  - Aluminum extrusion base and upper frame
  - Multiple removable vertical connector/test panels
  - Repeated connector groups arranged in columns
  - Top-mounted cable harness routed across the fixture
  - White cable clamps holding harness bundles
  - Side support posts for rigidity
  - Front alignment blocks and locking hardware
  - Rear or side cable exit path
  - Repeated fasteners for easy service access
- Use modularity as a core design rule:
  - One test panel per HMI section or connector group
  - Replaceable connector plates
  - Labeled harnesses
  - Service loops for maintenance

## 3. Electrical Design

- Build the electrical design from the connector pinout tables.
- Make a complete I/O list with:
  - Connector name
  - Pin number
  - Signal name
  - Signal type
  - Voltage/current rating
  - Test method
  - Pass/fail limit
  - Controller input/output channel
  - Wire color
  - Terminal block number
- Decide the automation level:
  - Manual: operator uses switches, meter readings, and visual inspection.
  - Semi-automatic: operator loads the HMI and starts a controller-driven test.
  - Fully automatic: controller sequences tests, records results, and reports pass/fail.
- Recommended controller choices:
  - PLC for industrial reliability and 24 VDC I/O.
  - Arduino or ESP32 for low-cost proof-of-concept testing.
  - Raspberry Pi or industrial PC for logging, UI, and network reporting.
  - DAQ module for accurate analog voltage/current measurement.
- Add electrical protection:
  - Main fuse or breaker
  - Branch fuses for each connector group
  - Current-limited power supply
  - Emergency stop circuit
  - Relay isolation for switched loads
  - Flyback protection for coils
  - Overvoltage protection
  - Reverse polarity protection
  - Proper chassis grounding
  - Shield termination for communication or analog wiring
- Keep wiring separated:
  - AC mains wiring
  - 24 VDC power wiring
  - Low-level analog signals
  - Digital I/O
  - Communication cables
  - Shield/earth wiring

## 4. Mechanical Frame Design

- Use aluminum T-slot extrusion for the main frame.
- Suggested frame sections:
  - Base frame mounted to the workbench
  - Upper horizontal support rail
  - Left and right vertical support posts
  - Front alignment rail
  - Rear cable support rail
- Use removable test panels:
  - Aluminum plate for industrial durability
  - Acrylic or Delrin for lightweight prototypes
  - Individual plates for each connector group
  - Captive screws or dowel alignment for repeatability
- Add alignment and holding features:
  - Dowel pins
  - Guide rails
  - Hard stops
  - Clamp blocks
  - Toggle clamps or pneumatic clamps if high repeatability is required
  - Locating nests for the HMI housing
- Design for maintenance:
  - Leave access to fasteners
  - Allow panel removal without cutting wires
  - Add cable service loops
  - Use replaceable wear parts where connectors are frequently mated

## 5. Connectors and Test Points

- Use the same connector family as the real HMI/product harness whenever possible.
- Use panel-mount connectors for repeatable connections.
- Use pogo pins or spring-loaded probes for temporary contact points.
- Use keyed connectors to prevent wrong orientation.
- Use connector labels on both the front panel and wiring side.
- Separate connector groups by function:
  - Power
  - Digital inputs
  - Digital outputs
  - Sensors
  - Communication
  - Spare/future expansion
- For each connector group, document:
  - Part number
  - Mating connector
  - Pin count
  - Wire gauge
  - Current rating
  - Expected mating cycle life
  - Replacement procedure

## 6. Wiring Harness

- Route the harness across the top or rear of the fixture like the reference design.
- Use cable clamps or cable duct to keep wiring fixed and repeatable.
- Label both ends of every wire.
- Use ferrules on stranded wires going into terminal blocks.
- Use proper crimp tools for connector terminals.
- Add strain relief near every panel connector.
- Bundle wires by function:
  - Power bundle
  - I/O bundle
  - Communication bundle
  - Sensor/analog bundle
- Leave service loops so panels can be removed for repair.
- Avoid sharp bends and pinch points.
- Keep high-current wiring away from sensitive analog or communication signals.

## 7. Control/Test Box

- Mount the control hardware in a dedicated enclosure or DIN-rail box.
- Include:
  - Main power inlet
  - Main disconnect or power switch
  - Emergency stop
  - 24 VDC power supply
  - Controller, PLC, DAQ, or microcontroller
  - Relay or I/O modules
  - Terminal blocks
  - Fuses or breakers
  - Status indicators
  - USB, Ethernet, or serial connection for logs
  - Grounding bar
- Separate AC mains from low-voltage DC wiring.
- Use finger-safe terminals for higher-voltage sections.
- Provide a wiring diagram inside the enclosure or in the documentation package.

## 8. Test Procedure

- Start with basic electrical safety checks:
  - Visual inspection
  - Connector presence check
  - Continuity check
  - Short-circuit check
  - Ground continuity check
- Add power checks:
  - Verify input voltage
  - Verify output power rails
  - Measure current draw
  - Check fuse status
- Add functional checks:
  - Press each HMI button and verify the expected input state.
  - Command each LED/output and verify the expected response.
  - Read each sensor input and compare against expected limits.
  - Run communication checks if the HMI uses serial, CAN, Ethernet, or another bus.
  - Verify display or screen response if applicable.
- Define clear pass/fail limits for every test.
- Record:
  - Serial number
  - Operator
  - Date/time
  - Test result
  - Failed step, if any
  - Measurement values

## 9. Documentation Package

- Keep these documents with the jig:
  - Mechanical layout drawing
  - Panel drawings
  - Electrical schematic
  - Wiring diagram
  - Connector pinout tables
  - I/O list
  - Bill of materials
  - Assembly procedure
  - Test procedure
  - Maintenance procedure
  - Calibration/check procedure
  - Revision history
- Update documentation whenever connectors, wiring, software, or test limits change.

## 10. Prototype First

- Build one small section before building the complete jig.
- Recommended prototype scope:
  - One connector group
  - One removable panel
  - One power input
  - One controller input group
  - One controller output group
  - One simple pass/fail test
- Validate:
  - Connector fit
  - Mechanical alignment
  - Cable routing
  - Electrical continuity
  - Contact reliability
  - Operator access
  - Ease of service
- Improve the design before scaling to the full fixture.

## 11. Starter Bill of Materials

| Category | Suggested Items |
| --- | --- |
| Frame | Aluminum T-slot extrusion, corner brackets, T-nuts, base plates |
| Panels | Aluminum plates, acrylic/Delrin plates, captive screws, dowel pins |
| Connectors | Panel-mount connectors, mating plugs, pogo pins, test sockets |
| Wiring | Hookup wire, shielded cable, ferrules, crimp terminals, cable labels |
| Harness Support | Cable duct, cable clamps, strain reliefs, cable ties, service-loop clips |
| Electrical Protection | Fuses, breakers, current limiters, surge protection, grounding bar |
| Control | PLC, DAQ, microcontroller, Raspberry Pi, industrial PC, relay modules |
| Power | 24 VDC power supply, main switch, E-stop, terminal blocks |
| Operator Interface | Start button, reset button, pass/fail indicators, buzzer, display |
| Mechanical Holding | Guide rails, hard stops, toggle clamps, alignment blocks |
| Tools | Crimp tool, wire stripper, multimeter, insulation tester, torque tools |

## 12. Recommended First Steps

- Create a connector and pinout spreadsheet.
- Decide which tests are required and which are optional.
- Sketch the fixture layout using the reference design as a guide.
- Select the controller platform.
- Select connector families and panel-mount versions.
- Design one removable test panel.
- Build one prototype connector group.
- Wire the prototype to the controller.
- Validate continuity, shorts, power, and one functional test.
- Update the design based on prototype results.
- Scale the modular panel layout to the full jig.

## 13. Safety Notes

- Have the final electrical design reviewed by a qualified electrical engineer or technician.
- Follow local electrical codes and workplace safety rules.
- Do not expose operators to live terminals.
- Use fusing and current limits on all externally accessible power.
- Verify emergency stop behavior before normal use.
- Clearly label voltage levels, moving parts, pinch points, and service access areas.
