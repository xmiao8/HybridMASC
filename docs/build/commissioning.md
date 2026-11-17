# First power-up

This page takes an assembled, wired machine to the point where the [user manual](../manual/index.md) takes over. Do it with the vat off, the cover off and the laser supply switched off until the step that needs it.

!!! note "Source code"
    The firmware and the control service aren't in this repository yet. The steps below say what each needs, so they can be followed once the code is published.

## 1. Flash the controller

1. Keep the laser supply **off**. The laser's control input floats while the Mega resets.
2. Build the firmware sketch (`firmware/HybridMASC/`) for the Arduino Mega 2560. The prototype uses arduino-cli with the `arduino:avr` core and the TMC2208Stepper library, version 0.2.5.
3. Upload it over USB.
4. Open the serial port at 500000 baud and send `PING`. The board answers with a line of JSON containing `"dev":"zmasc"`.

Opening the serial port normally resets the Mega, which loses its homing. The control service avoids this by opening the port with hang-up-on-close turned off; on the host, run `stty -F /dev/ttyACM0 -hupcl` after each flash, replug or reboot.

## 2. Check the Z axis from the serial port

With the vat off and the build plate clear of everything:

1. Send `DRIVER?`. The reply should show that the TMC2208 answers on its UART and reports 16 microsteps. If it doesn't answer, check the two UART wires before moving anything.
2. Send `ENDSTOP?` with the carriage away from the top: it should read not triggered. Block the sensor by hand: it should read triggered. If it is the other way round, the polarity setting is wrong for your sensor.
3. Send `ENABLE on=1`, then a 1 mm relative move upward with `MZ` (the command table is in the [design notes](../design-and-implementation.md)). The plate should move **up** 1 mm. If it moves down, swap one motor coil. If it moves 2 mm, the driver isn't taking its settings over the UART.
4. Send `HOME`. The carriage rises to the endstop, backs off, creeps back and parks 2 mm below it.

## 3. Set up the host

The service is a Python web application (FastAPI) that runs as a systemd service and serves the interface on port 80. The host needs:

- Linux with no desktop session holding the projector's output, since the service drives the HDMI output directly.
- A udev rule giving the service account access to the projector's USB control interface, and permission to open the Mega's serial port.
- Optionally, a polkit rule letting the service restart or shut down the computer from the System tab.
- Console blanking disabled, and the service set to switch the projector's LED off on exit, because the text console reappears on the projector whenever the service releases the output.

The interface has no login. Restrict the port to the networks that should reach it with the host's firewall.

## 4. First start

Follow the manual's [start-up order](../manual/startup.md): machine supplies first, then the host, then the laser supply only when needed. Open the page and check that the Z stage, Galvo, Laser and Projector chips in the header are green.

## 5. Projector

1. On the **Machine** tab, show the focus test image and switch the LED on at a low level. The projector powers up with its LED on; the service switches it off about 40 s after boot.
2. Lay a tissue over the funnel where the film will be. Focus the projector's lens on it until the Siemens stars are sharp at the centre and at all four corners.
3. Show the grid image and check the corner marker to see whether the image is mirrored as seen from above. Note the answer for the slicer's mirror settings.

On this projector the LED current scale is reversed from the manufacturer's documentation; the interface hides this and shows 255 as brightest. See the manual's [Projector](../manual/projector.md) page.

## 6. Laser beam path

Eyewear on, laser power limit at its lowest useful setting, beam block in hand.

1. Put the galvo inside its allowed range from the **Machine** tab. Arming is refused while it is outside, and it sits at 0 V after every reset.
2. Arm the laser and fire with press-and-hold. The beam goes off when you let go.
3. Adjust mirror 1 until the beam lands on the centre of mirror 2, then mirror 2 until it enters the centre of the scanner's input.
4. With a tissue over the funnel, look for the spot. If the module's lens is adjustable, focus it until the spot on the tissue is as small as it gets.
5. Jog the galvo across its range and check that the spot crosses the whole projected field without clipping. The prototype's spot dims near one corner of the field, as if the beam is partly cut off there; if you see this, re-centre the beam on the scanner's input.

## 7. Calibrate

These are the manual's procedures, done here for the first time. See [Calibration](../manual/calibration.md).

1. **Measure projection.** With a printed 10 mm scale bar on the tissue, measure the projected pixel size and accept it. The prototype measures about 46 to 47 µm a pixel, a field of about 60 × 37 mm.
2. **Align the laser to the projector.** Run the alignment. A good run on the prototype fits to a few tens of micrometres; hundreds means stray reflections or an over-bright spot, usually cured by lower laser power or a higher PWM frequency.
3. **Trace the edge** (Demo tab) to see the laser follow the outline of the projected field.

Repeat both calibrations after fitting the vat with its film, since the film may sit at a slightly different height from the tissue, and after moving the projector, a mirror, the scanner or the laser.

## 8. Fit the vat and set the film zero

1. Fit the vat with its film. Leave it empty.
2. Home Z, then jog the build plate down slowly until it just touches the film, and press **Set film zero**. Until this is set, nothing in software stops the plate at the vat. See [Z stage and film zero](../manual/z-stage.md).
3. Refit the cover.

## 9. First print

Print the exposure ladder (Slicer tab, calibration prints) to find the exposure for your resin at your LED level, then a simple shape. The manual's [Preparing a job](../manual/slicing.md) and [Printing](../manual/printing.md) pages take it from here.
