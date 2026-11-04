# Projector

The image and the light are switched separately: pick a test image, set the LED level, then switch the LED on, or run a timed exposure. The controls are on the **Projector** card of the Machine tab.

- **LED level** sets the brightness from 0 to 255: 255 is the brightest, and 0–16 give no light. Type a level or step it with **−5** / **+5**. It is not calibrated in mW/cm², but it repeats on this machine, so an exposure time is only meaningful together with the level it was found at.
- **Test images**: **Black**; **White** (the whole field); **Grid** (a 16 × 10 grid with a centre square and a corner marker that shows mirroring); **Focus** (Siemens stars at the centre and corners, plus 2–8 px bar groups); **Clear** (no image).
- **LED on** / **LED off** work as the shutter. A black image still lets some light past the mirrors, so only LED off is truly dark. An LED switched on by hand goes off by itself after 5 minutes.
- **Expose for** *n* **s** → **Expose** switches the LED on with the image that is showing for 0.1–300 s, then off, timed by the service; the event log records how long it was actually on. It refuses while the image is black. While it runs, everything else that would change the machine is refused except **LED off** (which ends it early) and **STOP**.

The service also switches the LED off when the projector connects, when a job starts, on STOP, and whenever the service stops. When the service stops, the laptop's text console appears on the projector; that is normal.

Typical uses: check focus with the Focus image and the camera; check mirroring with the Grid; cure a single test patch in resin with **Expose**. To find exposure times for a new resin, print the [Exposure ladder](slicing.md#step-1-slicing).
