# Safety

!!! danger "Read before the first session"
    Keep the **STOP** button in view whenever the machine is doing something. It works from every page, with one tap and no confirmation.

- **STOP** is the red button at the top right of every page. One tap, no confirmation: it stops Z at once, aborts homing, switches the laser and the projector LED off, and ends any print, preview, sequence or calibration run. To brake Z gently instead, use **Halt** on the Machine tab.
- **Laser.** The 405 nm diode laser is steered by galvo mirrors anywhere in the 60 × 37.5 mm field, and its reflections off the vat walls are bright. Wear 405 nm laser safety eyewear whenever the laser supply is on. Switch the laser supply off before the controller is reset or reflashed: its control input floats for a second or two.
- **Projector light.** The projector's blue LED cures resin and is bright; don't look into the projection lens. It switches its LED on by itself at power-up. The service turns it off about 40 s after boot, and again whenever the projector turns it back on.
- **Resin.** The MASC resin contains silver trifluoroacetate (AgTFA). Handle it in the fume hood, with nitrile gloves and eye protection, and follow its safety data sheet for spills and waste.
- **Moving plate.** Keep hands out of the build area while Z moves. Until a film zero is set there is no lower software limit: **Lower** or **Move to height** can drive the plate down to the frame's hard stop, through the vat. Set the film zero before putting resin in the vat.
- **Top of travel.** Normal Z moves don't watch the top switch. If the stage has lost steps, a move upward can run the carriage into the top of the frame. Re-home after anything that may have cost steps (a crash, a stall, a motor power cut).
- **No login.** Anyone who can open the page on the lab network or the Tailscale network can operate the machine, and the **Control:** label in the header locks nothing. The **System** tab shows how many browsers are connected; agree with others in the lab who is in charge before you start.
- **E-stop and Sash interlock.** The Safety card on the Print tab lists both, but the design notes describe no E-stop or sash switch wired to the controller. Treat them as not wired until this is confirmed (see [Open items](open-items.md)).
