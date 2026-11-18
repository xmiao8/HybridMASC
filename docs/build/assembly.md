# Assembly

The order below works from the chassis outward: strip and cut the Form 2, fit the Z stage parts, build the vat, then the optics inside the base, the laser on the side wall and the electronics. Wiring has its [own page](wiring.md).

Positions are given facing the front of the printer: the Z tower is at the back, and "right" is your right.

!!! note "Photos"
    Assembly photos will be added. Until then, the rendered model in the project's `Model` folder (to be published with the CAD) shows where each part sits, including a cutaway of the base.

## 1. Prepare the chassis

1. **Strip the Form 2.** Remove the cover, the resin tank and wiper, the build platform, the display, the mainboard, and the laser and galvo block from inside the base. Keep the frame, the Z tower with its motor, lead screw and carriage, and the cover.
2. **Remove the stock platform arm** from the Z carriage, back to the carriage itself. The new build plate arm bolts on in its place.
3. **Flatten the top deck.** Remove the tank tray and wiper mechanism so the deck is a flat surface.
4. **Cut the deck opening** for the light funnel, centred on the build area. The funnel is about 150 × 115 mm where it passes through the deck; cut to the printed part, not to this number.
5. **Clear the optics bay.** The inside of the base, below the deck, must be empty over the footprint of the projector, the galvo stand and the mirror stand.
6. **Open the front bay** for the RT-65C power supply (left) and the controller (right).
7. **Drill the laser entry hole** in the right-hand wall, about 12 mm in diameter, in line with fold mirror 1. Mark it from the mirror stand once that is in place (step 4.3), not from a measurement.
8. **Fit the base tray** under the chassis in place of the stock feet.

## 2. Z stage

1. **Fit the endstop.** Mount the Form 2's own optical slot sensor in its printed mount at the top of the Z tower, so that the carriage blocks the slot at the top of travel. The firmware homes upward and expects the sensor's output HIGH when blocked.
2. **Fit the build plate arm** to the carriage. The plate hangs from a post at the end of the arm, centred over the deck opening.
3. **Fit the camera bracket** to the arm, with the camera looking straight down at the build area, beside the plate's post. Route its USB cable so it follows the carriage over the full travel without snagging.
4. **Check the travel by hand** with the motor unpowered: the carriage should run from the endstop to the frame's hard stop, about 205 mm below it, without the arm or the camera touching anything.

Whether the build plate needs levelling to the film, and how, is **to confirm**.

## 3. Vat

1. **Print the funnel base and the vat frame.** Check that the funnel's inner walls are matte and dark: both light sources pass through it, and the laser's reflections off bright walls confuse the alignment camera.
2. **Cut the release film** a little larger than the seal plates.
3. **Clamp the film.** Lay the film between seal plate A (countersunk holes) and seal plate B (tapped holes) and fit the 18 M3 countersunk screws. Tighten them a little at a time, working across the plate, so the film ends up flat and evenly tensioned with no wrinkles.
4. **Fit the clamped film to the vat frame.** The seal plates have six larger holes for this; the screws they take are **to confirm**. The film is now the vat's floor.
5. **Seat the funnel base on the deck,** funnel down through the opening, and fix it with its four corner screws.
6. **Place the vat on the funnel base.** How it locates and locks is **to confirm**.

The film is a consumable. Slow laser passes mark it, and the Sequencer tab tracks which areas have been used (see the manual's [Sequencer](../manual/sequencer.md) page).

## 4. Optics in the base

The projector and the scanner sit side by side under the funnel, both pointing up at the same film. Neither lens can be directly under the centre of the build field, so each sits to one side of it and reaches the field at a slight angle. The calibration maps one onto the other, keystone included.

1. **Projector.** Fix the LightCrafter 4500 to its stand with the lens pointing up, and place it so the lens is under the funnel. Leave access to its HDMI, USB and power connectors, and to the focus ring.
2. **Galvo scanner and scan lens.** Fix the scanner block to the galvo stand with the scan lens above it, under the funnel beside the projector lens. Leave the scanner's input aperture facing fold mirror 2.
3. **Fold mirrors.** Fit the two mirrors to the mirror stand at the back right of the bay. Mirror 1 sits level with the laser's entry hole and turns the incoming beam straight down. Mirror 2 sits below it, level with the scanner's input, and turns the beam forward into the scanner.
4. **Mark and drill the entry hole** (step 1.7) if you haven't yet, in line with mirror 1.

Leave fine positioning until [first power-up](commissioning.md): the projector is focused and the mirrors are aligned with the machine running.

## 5. Laser

1. **Fit the laser bracket** to the outside of the right-hand wall, so the module's lens points through the entry hole at mirror 1.
2. **Fit the laser module** to the bracket. Don't connect its supply yet.
3. **Fit the laser driver** on standoffs on the right-hand wall, forward of the laser, and the **galvo driver board** forward of that.
4. **Fit the second power supply,** if your build has one (see the [parts list](parts.md#electronics)), low on the right-hand side.

The beam path from the module to the wall is open on the prototype. A printed shroud over this gap is worth adding.

## 6. Electronics

1. **RT-65C power supply:** front bay, left.
2. **Controller:** fit the Mega to the controller stand in the front bay, right, and plug the control board onto it. Fit the TMC2208 with its heatsink into its socket.
3. **Leave the USB port reachable.** The Mega is powered and controlled over USB from the host.

Then go on to [Wiring](wiring.md).

## 7. Cover

Refit the Form 2 cover; on the prototype it sits turned 180° from its stock orientation. Leave it off until [first power-up](commissioning.md) is finished.
