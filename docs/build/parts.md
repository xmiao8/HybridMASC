# Parts list

A cost estimate, then three tables: parts to buy, parts to print or machine, and fasteners and consumables. Quantities in brackets come with the donor Form 2 or with another part. A part marked **to confirm** is on the machine, but its exact model or size isn't recorded yet (see [Open items](open-items.md)). Quantities are for one machine.

Where a part was bought from a known listing, the Notes column links to it. Listings change, so check the specification against the table before ordering.

## Cost estimate

Approximate prices in US dollars, checked in November 2026 against distributor and marketplace listings. Where no listing was checked the price is marked as an estimate. Shipping, tax and tools aren't included, and nothing here is a quote.

| Group | Estimate (USD) |
|---|---|
| Purchased parts (tables below) | 1,884–3,197 |
| Printed parts (PETG-CF and PET-CF filament) | 30–60 |
| Seal plates, machined from the drawings | 30–150 |
| Fasteners, wire and connectors | 20–40 |
| Release film | 18–30 |
| Laser safety eyewear and a beam block | 40–150 |
| **Total** | **about 2,000–3,600** |

The projector is most of the cost. The total assumes a new DLP LightCrafter 4500 (about $1,300 from TI, more from distributors); a projector you already have brings it down a long way. Most of the rest is the donor Form 2, the galvo kit and the laptop, all of which vary a lot second-hand. A lab that already has a laptop and a spare Form 2 can build the rest for roughly $1,700–2,800.

## Purchased parts

### Chassis and motion

| # | Part | Qty | Specification | Price (USD) | Notes |
|---|---|---|---|---|---|
| 1 | Formlabs Form 2 (donor printer) | 1 | Chassis, Z tower, carriage, orange cover, and items 2 to 4 and 9 | 150–400 | A unit with a failed laser or mainboard is enough; only the frame, the Z axis and the fold mirrors are reused |
| 2 | Z stepper motor | (1) | 1.8° (200 steps/rev), driven at 600 mA RMS | — | From the donor Form 2; nothing to buy |
| 3 | Lead screw | (1) | 4 mm lead, direct drive | — | From the donor Form 2; nothing to buy. The firmware assumes a 4 mm lead (800 microsteps/mm) |
| 4 | Optical slot sensor (endstop) | (1) | Output HIGH when blocked, read with the controller's pull-up | — | From the donor Form 2; nothing to buy |

### Light sources and optics

| # | Part | Qty | Specification | Price (USD) | Notes |
|---|---|---|---|---|---|
| 5 | DLP projector | 1 | Any DLP projector with an HDMI input and a wavelength that cures your resin. The prototype uses a TI DLP LightCrafter 4500 (DLPC350 controller, 912 × 1140 DMD) on its blue LED channel | Varies; 1,300–1,700 for the LightCrafter 4500 | Use what you have. The control service switches and dims the LED through the LightCrafter's USB interface; with another projector, layer timing falls back to showing a black image, which lets some light through (see the note below this table) |
| 6 | Laser module | 1 | 405 nm laser engraver module, 500 mW, with focusing lens and driver board | 25–55 | [Amazon listing](https://a.co/d/09Kt7r56). At 500 mW, treat it as a Class 4 laser |
| 7 | Laser driver | (1) | Constant-current driver board with a TTL/PWM input | Included (with item 6) | Comes with the laser module; nothing to buy. Runs from the 12 V laser supply (item 17). Modulation bandwidth **to confirm** |
| 8 | Two-axis galvanometer scanner with its driver board | 1 set | Analog position inputs, one per axis | 85–250 | [Amazon listing](https://a.co/d/0a6Q2i9N). A laser-show (ILDA) scanner kit; only the mirrors, motors and analog driver are used, not the kit's show controller. Scan speed, scan angle and input range **to confirm** |
| 9 | Fold mirror | (2) | | — | From the donor Form 2; nothing to buy |
| 10 | Alignment camera | 1 | Arducam 8 MP USB (UVC), manual focus | 35–75 | Used for calibration only |

**Projector choice.** Any DLP projector that takes HDMI and emits at a wavelength your resin cures at will project the layers. The LightCrafter 4500 has two advantages the software relies on: its LED can be switched and dimmed over USB, which works as a shutter, and its native output is small enough for a fine pixel size. With a projector the service can't control, an exposure ends by showing black, and the light a DLP still lets through during a black frame keeps reaching the resin. Recalibrate the pixel size and the laser alignment for whichever projector you use.

### Electronics

| # | Part | Qty | Specification | Price (USD) | Notes |
|---|---|---|---|---|---|
| 11 | Controller | 1 | Arduino Mega 2560 R3 | 40–52 | Powered from the host's USB |
| 12 | Control board | 1 | Custom two-layer circuit board that plugs onto the Mega ("MASC 3.0 v1.0", about 102 × 81 mm) | 15–50 (pcb fabrication) | Carries items 13 to 15 and the connectors; design files not published yet |
| 13 | Stepper driver | 1 | TMC2208 V3.0 stepper driver module with heatsink, used in UART mode | 6–15 | [Amazon listing](https://a.co/d/09XOhLya). Socketed on the control board, with the UART wired both ways |
| 14 | Galvo DAC | 2 | Analog Devices AD5761R, 16-bit, ±10 V output | 15–30 (both) | One per axis; uses its internal reference |
| 15 | Buzzer, voltage regulators, connectors | 1 set | As on the control board | 10–30 (estimate) | Listed in the board's own bill of materials (not published yet) |
| 16 | Power supply | 1 | Mean Well RT-65C: +5 V at 5 A, +15 V at 2.2 A, −15 V at 0.5 A, 65.5 W, 88–264 V AC input | 25–60 | +15 V feeds the Z driver; ±15 V feeds the galvo driver |
| 17 | Laser power supply | 1 | 12 V DC, 2 A | 8–15 (estimate) | Any 12 V, 2 A adapter. Powers the laser module and its driver (items 6 and 7) only |
| 18 | Projector power supply | 1 | As supplied with the projector | Included (with item 5) | |

### Host and cables

| # | Part | Qty | Specification | Price (USD) | Notes |
|---|---|---|---|---|---|
| 19 | Host laptop | 1 | Linux laptop with one HDMI port and at least two USB ports | 150–400 (used; estimate) | Runs the control service and drives the projector. The Mega and the projector's LED control take one USB port each; the alignment camera needs a third, so use a USB hub if the laptop has only two. The prototype uses a 4-thread laptop with 6 GB RAM running Ubuntu; no desktop session is needed |
| 20 | HDMI cable | 1 | Host to projector | 5–10 (estimate) | |
| 21 | USB cable, A to B | 1 | Host to Mega | 5–10 (estimate) | Also powers the Mega |
| 22 | USB cable to the projector's USB port | 1 | Host to projector (LED control) | 5–10 (estimate) | |
| 23 | USB cable for the camera | 1 | Long enough to follow the Z carriage over its full travel | 5–15 (estimate) | |
| 24 | USB hub | (1) | Powered USB 2.0 or better | 0–20 (optional) | Only if the laptop has fewer than three USB ports |

## Printed and machined parts

The CAD files will be added to the repository under `hardware/`. File names below are the ones in the project's CAD folder. Sizes are bounding boxes.

### Vat

| Part | File | Qty | Size (mm) | How it's made | Notes |
|---|---|---|---|---|---|
| Light funnel and vat base | `Vat_P1` | 1 | 200 × 145 × 68 | 3D printed | Screws to the deck; its funnel passes through the deck opening. An alternative, `Vat_Alt`, is 5 mm taller |
| Vat frame | `Vat_P2` | 1 | 80 × 103 × 23 | 3D printed in PET-CF | Holds the resin; the film closes its bottom |
| Seal plate A | `SealA` | 1 | 92.7 × 64.7 × 3.2 | Machined from 1/8 in (3.2 mm) stock | 18 countersunk M3 clearance holes round the window; drawing `SealA - Sheet1.pdf` |
| Seal plate B | `SealB` | 1 | 92.7 × 64.7 × 3.2 | Machined from 1/8 in (3.2 mm) stock | 18 tapped M3 holes matching plate A; drawing `SealB - Sheet1.pdf` |
| Vat lid | `Vat Lid` | 1 | | 3D printed | Covers the vat between prints |

The CAD folder also holds older vat revisions (`Vat`, `Vat Short`, `Vat_85`, `Vat_90`, `Vat_Alt_Bottom`, `Round Vat`); the machine uses `Vat_P1` and `Vat_P2`.

### Z stage

| Part | File | Qty | Size (mm) | How it's made | Notes |
|---|---|---|---|---|---|
| Build plate with arm | `Build Plate` | 1 | 149 × 58 × 30 | 3D printed | Replaces the Form 2 platform arm. `Build Plate Thin` is a variant |
| Camera bracket | `Camera` | 1 | 39 × 58 × 30 | 3D printed | Holds the alignment camera on the carriage arm, looking down |
| Endstop mount | `sensor` | 1 | | 3D printed | Holds the slot sensor at the top of the Z tower |

### Optics and laser

| Part | File | Qty | Size (mm) | How it's made | Notes |
|---|---|---|---|---|---|
| Projector stand | `DLP Stand` | 1 | | 3D printed | Holds the LightCrafter in the base, lens up |
| Galvo stand | `Galvo Stand` | 1 | 118 × 76 × 45 | 3D printed | Holds the scanner block under the funnel |
| Mirror stand | `Mirror Stand` | 1 | 91 × 92 × 70 | 3D printed | Carries the two fold mirrors from the Form 2 |
| Laser bracket | `Top Laser`, `Laser_Assem` | 1 | 84 × 58 × 30; 104 × 88 × 36 | 3D printed | Holds the laser module on the right-hand wall, in line with the entry hole |
| Laser adapter | `Laser Adapter` | 1 | | 3D printed | Fits the laser module to its bracket |

### Electronics

| Part | File | Qty | Size (mm) | How it's made | Notes |
|---|---|---|---|---|---|
| Controller stand | `Microcontroller Stand` | 1 | 100 × 76 × 5 | 3D printed | Plate for the Mega and control board in the front bay |
| Driver board brackets | | 2 | | Sheet or printed plate with standoffs | For the laser driver and the galvo driver on the right-hand wall; no CAD yet |

## Fasteners and consumables

| Part | Qty | Notes |
|---|---|---|
| M3 × 6 mm countersunk screws | 18 | Clamp the film between the seal plates |
| M3 screws, mixed lengths, with nuts or heat-set inserts | As needed | Printed parts, brackets, standoffs |
| 20 mm screws for the funnel plate | 4 | Through the funnel plate's corners into the deck |
| M3 standoffs | 8 | Laser driver and galvo driver boards |
| FEP release film | 1 sheet, at least 100 × 70 mm | 0.127 mm (0.005 in). A consumable: the laser marks it |
| Hook-up wire, crimp connectors, ferrules | | Motor, endstop, galvo signal, laser TTL and power wiring |
| Filament for the printed parts | About 1 kg | PETG-CF for most parts; PET-CF for the vat frame, which touches resin |
| Tissue (Kimwipe) and a printed 10 mm scale bar | | Stand in for the film during the first calibrations |

## Safety equipment

| Part | Notes |
|---|---|
| Laser safety eyewear for 405 nm | Rated for a 0.5 W Class 4 laser at 405 nm (commonly OD 4 or higher); confirm the rating with your laser safety officer. One pair for everyone in the room |
| Beam block | A matte, non-flammable plate to stop the beam during mirror alignment |
| Nitrile gloves, eye protection, fume hood | For resin handling; see the manual's [Safety](../manual/safety.md) page |
