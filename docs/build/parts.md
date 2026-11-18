# Parts list

Three tables: parts to buy, parts to print or machine, and fasteners and consumables. A part marked **to confirm** is on the machine, but its exact model or size isn't recorded yet (see [Open items](open-items.md)). Quantities are for one machine.

Where a part was bought from a known listing, the Notes column links to it. Listings change, so check the specification against the table before ordering. Prices aren't listed yet.

## Purchased parts

### Chassis and motion

| # | Part | Qty | Specification | Notes |
|---|---|---|---|---|
| 1 | Formlabs Form 2 (donor printer) | 1 | Chassis, Z tower with lead screw and carriage, orange cover | A unit with a failed laser or mainboard is enough; only the frame and Z axis are reused |
| 2 | Z stepper motor | 1 | 1.8° (200 steps/rev), driven at 600 mA RMS | The motor on the Form 2's Z tower; model **to confirm** |
| 3 | Lead screw | 1 | TR8x4 (4 mm lead), direct drive | Part of the Z tower; lead **to confirm** against the firmware's setting |
| 4 | Optical slot sensor (endstop) | 1 | Output HIGH when blocked, read with the controller's pull-up | Mounted at the top of travel; model **to confirm** |

### Light sources and optics

| # | Part | Qty | Specification | Notes |
|---|---|---|---|---|
| 5 | DLP projector | 1 | TI DLP LightCrafter 4500 (DLPC350 controller, 912 × 1140 DMD), blue LED channel | HDMI input at 1280 × 800; USB for LED control. LED wavelength **to confirm** |
| 6 | Laser module | 1 | 405 nm laser engraver module, nominally 500 mW, with focusing lens | [Amazon listing](https://a.co/d/09Kt7r56). Laser class and measured power **to confirm** |
| 7 | Laser driver | 1 | Constant-current driver with a TTL modulation input | Whether it comes with the module (item 6) or is separate, its supply voltage and its modulation bandwidth are **to confirm** |
| 8 | Two-axis galvanometer scanner with its driver board | 1 set | Analog position inputs, one per axis | [Amazon listing](https://a.co/d/0a6Q2i9N). A laser-show (ILDA) scanner kit; only the mirrors, motors and analog driver are used, not the kit's show controller. Scan speed, scan angle and input range **to confirm** |
| 9 | Scan lens | 1 | Barrel labelled "89.6 mm" | Sits above the scanner, under the funnel; model **to confirm** |
| 10 | Fold mirror | 2 | About 22 × 22 × 3 mm, first-surface | Coating and supplier **to confirm** |
| 11 | Alignment camera | 1 | Arducam 8 MP USB (UVC), manual focus | Used for calibration only |

### Electronics

| # | Part | Qty | Specification | Notes |
|---|---|---|---|---|
| 12 | Controller | 1 | Arduino Mega 2560 R3 | Powered from the host's USB |
| 13 | Control board | 1 | Custom two-layer circuit board that plugs onto the Mega ("MASC 3.0 v1.0", about 102 × 81 mm) | Carries items 14 to 16 and the connectors; design files not published yet |
| 14 | Stepper driver | 1 | TMC2208 V3.0 stepper driver module with heatsink, used in UART mode | [Amazon listing](https://a.co/d/09XOhLya). Socketed on the control board, with the UART wired both ways |
| 15 | Galvo DAC | 2 | Analog Devices AD5761R, 16-bit, ±10 V output | One per axis; needs an external reference (**to confirm** how it is provided) |
| 16 | Buzzer, voltage regulators, connectors | 1 set | As on the control board | Listed in the board's own bill of materials (not published yet) |
| 17 | Power supply | 1 | Mean Well RT-65C: +5 V at 5 A, +15 V at 2.2 A, −15 V at 0.5 A, 65.5 W, 88–264 V AC input | Which rail feeds the Z driver, the galvo driver and the laser driver is **to confirm** |
| 18 | Second power supply | 1 | **To confirm** | The assembly model shows a second, smaller supply on the right-hand side for the galvo and laser. Whether the machine has one, and its model, is **to confirm** |
| 19 | Projector power supply | 1 | As supplied with the LightCrafter 4500 | |

### Host and cables

| # | Part | Qty | Specification | Notes |
|---|---|---|---|---|
| 20 | Host computer | 1 | Laptop or small PC with HDMI out and three USB ports, running Linux | The prototype uses a 4-thread laptop with 6 GB RAM and Ubuntu; no desktop session is needed |
| 21 | HDMI cable | 1 | Host to projector | |
| 22 | USB cable, A to B | 1 | Host to Mega | Also powers the Mega |
| 23 | USB cable to the projector's USB port | 1 | Host to projector (LED control) | |
| 24 | USB cable for the camera | 1 | Long enough to follow the Z carriage over its full travel | |

## Printed and machined parts

The CAD files will be added to the repository under `hardware/`. File names below are the ones in the project's CAD folder. Sizes are bounding boxes.

### Vat

| Part | File | Qty | Size (mm) | How it's made | Notes |
|---|---|---|---|---|---|
| Light funnel and vat base | `Vat_P1` | 1 | 200 × 145 × 68 | 3D printed | Screws to the deck; its funnel passes through the deck opening. An alternative, `Vat_Alt`, is 5 mm taller |
| Vat frame | `Vat_P2` | 1 | 80 × 103 × 23 | 3D printed | Holds the resin; the film closes its bottom. Use a resin-resistant material |
| Seal plate A | `SealA` | 1 | 92.7 × 64.7 × 3.2 | Machined from 1/8 in (3.2 mm) stock | 18 countersunk M3 clearance holes round the window; drawing `SealA - Sheet1.pdf` |
| Seal plate B | `SealB` | 1 | 92.7 × 64.7 × 3.2 | Machined from 1/8 in (3.2 mm) stock | 18 tapped M3 holes matching plate A; drawing `SealB - Sheet1.pdf` |
| Vat lid | `Vat Lid` | 1 | | 3D printed | Covers the vat between prints |

Which vat revision is on the machine now is **to confirm**: the CAD folder also holds `Vat`, `Vat Short`, `Vat_85`, `Vat_90`, `Vat_Alt_Bottom` and `Round Vat`.

### Z stage

| Part | File | Qty | Size (mm) | How it's made | Notes |
|---|---|---|---|---|---|
| Build plate with arm | `Build Plate` | 1 | 149 × 58 × 30 | 3D printed on the prototype; material **to confirm** | Replaces the Form 2 platform arm. `Build Plate Thin` is a variant |
| Camera bracket | `Camera` | 1 | 39 × 58 × 30 | 3D printed | Holds the alignment camera on the carriage arm, looking down |
| Endstop mount | `sensor` | 1 | | 3D printed | Holds the slot sensor at the top of the Z tower |

### Optics and laser

| Part | File | Qty | Size (mm) | How it's made | Notes |
|---|---|---|---|---|---|
| Projector stand | `DLP Stand` | 1 | | 3D printed | Holds the LightCrafter in the base, lens up |
| Galvo stand | `Galvo Stand` | 1 | 118 × 76 × 45 | 3D printed | Holds the scanner block under the scan lens |
| Mirror stand | `Mirror Stand` | 1 | 91 × 92 × 70 | 3D printed | Carries the two fold mirrors |
| Laser bracket | `Top Laser`, `Laser_Assem` | 1 | 84 × 58 × 30; 104 × 88 × 36 | 3D printed | Holds the laser module on the right-hand wall, in line with the entry hole |
| Laser adapter | `Laser Adapter` | 1 | | 3D printed | Fits the laser module to its bracket; whether it is still in use is **to confirm** |

### Electronics

| Part | File | Qty | Size (mm) | How it's made | Notes |
|---|---|---|---|---|---|
| Controller stand | `Microcontroller Stand` | 1 | 100 × 76 × 5 | 3D printed | Plate for the Mega and control board in the front bay |
| Driver board brackets | | 2 | | Sheet or printed plate with standoffs | For the laser driver and the galvo driver on the right-hand wall; no CAD yet |
| Base tray | | 1 | About 360 × 385 × 17 | **To confirm** | Grid tray the chassis stands on, in place of the Form 2's feet; no CAD yet |

## Fasteners and consumables

| Part | Qty | Notes |
|---|---|---|
| M3 countersunk screws | 18 | Clamp the film between the seal plates. Length **to confirm** |
| M3 screws, mixed lengths, with nuts or heat-set inserts | As needed | Printed parts, brackets, standoffs |
| Screws for the funnel plate | 4 | Through the funnel plate's corners into the deck. Size **to confirm** |
| M3 standoffs | 8 | Laser driver and galvo driver boards |
| Release film | 1 sheet, at least 100 × 70 mm | FEP or PFA, 0.127 mm (0.005 in). Which of the two **to confirm**. A consumable: the laser marks it |
| Hook-up wire, crimp connectors, ferrules | | Motor, endstop, galvo signal, laser TTL and power wiring |
| Filament for the printed parts | | Material used on the prototype **to confirm** |
| Tissue (Kimwipe) and a printed 10 mm scale bar | | Stand in for the film during the first calibrations |

## Safety equipment

| Part | Notes |
|---|---|
| Laser safety eyewear for 405 nm | The optical density needed depends on the laser's class and power, both **to confirm**. One pair for everyone in the room |
| Beam block | A matte, non-flammable plate to stop the beam during mirror alignment |
| Nitrile gloves, eye protection, fume hood | For resin handling; see the manual's [Safety](../manual/safety.md) page |
