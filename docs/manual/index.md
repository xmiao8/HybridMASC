# HybridMASC user manual

## About this manual

This manual is for operators who run HybridMASC from its web interface: starting it up, homing and setting the film zero, calibrating, slicing, printing and shutting down. It covers the software as it stood on 4 November 2026 (web service 0.1.0-demo, firmware `fe3a1b1`). How each part is built and why it behaves as it does is in the [design and implementation notes](../design-and-implementation.md), which the printer also shows on its **Docs** tab.

Conventions used throughout:

- Tabs, buttons and fields are in **bold**, spelled as the screen shows them.
- Z heights are in mm above the film zero, unless a field says "below the top switch".
- Z speeds are in mm/min (as resin slicers give them), acceleration in mm/s², laser and galvo speeds in mm/s.
- Laser power is PWM duty in %, galvo position is in volts, and projector brightness is an LED level from 0 to 255. None of these is calibrated in physical units yet.

## The machine at a glance

HybridMASC is a bottom-up DLP resin printer with a laser added: each layer is cured by a projected image, and on layers that carry conductive features a 405 nm laser then writes silver into the cured resin. It sits in a fume hood; a laptop beside it runs the control service and serves the web page.

| Part | What it does | Where you control it |
| --- | --- | --- |
| Build plate on the Z stage | A lead-screw stage moves the plate up (+) and down, in 1.25 µm steps. An optical switch marks the top of travel. | Machine tab, **Z stage** card |
| DLP projector (TI LightCrafter 4500) | Projects each layer's mask up through the vat film: 1280 × 800 px, about 46.85 µm a pixel, a 60.0 × 37.5 mm field. Only the blue LED is used. | Machine tab, **Projector** card |
| 405 nm laser and two-axis galvo | Writes silver lines into the cured layer by reducing the AgTFA in the resin. | Machine tab, **Galvo** and **Laser** cards |
| Alignment camera (Arducam 8MP) | Looks down at the build area from the Z carriage. Used to align the laser to the projector and to measure the pixel size. | **Camera** and **Calibrate** tabs |
| Controller (Arduino Mega 2560) | Steps Z, sets the galvo voltages and switches the laser. Turns the laser off 0.5 s after the last laser command, so a stalled computer can't leave it on. | Status chips in the header |
| Host laptop | Runs the control service, drives the projector over HDMI and USB, and keeps the jobs and settings. | **System** tab |

Every printed layer goes through the same cycle, timed by the service:

1. **Wait before exposure.** The mask is already on the projector with the LED off; the resin and film settle.
2. **Expose.** The LED comes on at the job's LED level for the burn-in time (first layers) or the normal time.
3. **Laser.** On layers with laser lines, the laser draws each line at its own power and speed.
4. **Wait after exposure.** The next layer's mask goes up, LED off.
5. **Lift.** Two stages: slowly while the layer peels off the film, then fast.
6. **Wait after lift.** A pause asked for during the print happens here.
7. **Retract.** Two stages: fast, then slowly for the last part so resin can flow out from under the plate, ending one layer higher than before.

