# Troubleshooting

Most problems show up first in the header chips, the Z status line or the event list; check the **Logs** tab for the service's own explanation before changing anything.

| Symptom | Likely cause | What to do |
| --- | --- | --- |
| A device chip isn't green | That part is unplugged, unpowered or not answering | Check its cable and supply. The service reconnects by itself; if not, **Restart service**. |
| The **live** badge is gone, or values stop changing | The page lost its connection to the service | Reload the page. If it persists, **Restart service** on the System tab. |
| Jog buttons refused; Z says "Not homed: press Home Z" | Z hasn't been homed since the controller started | Press **Home Z**. |
| **Home Z** won't start | The top switch already reads triggered: the carriage is in the switch, or the sensor is unplugged | Check the sensor cable. If the carriage is at the switch, it has to be moved down before homing. |
| Homing stops with a reason | A homing phase ran past its distance limit | Look for an obstruction or a loose sensor, then home again. |
| The plate ends up higher or lower than the readout, or ran into the top | The motor lost steps (too fast, too much acceleration, or a heavy peel) | Home again. Lower the move speed or acceleration, or soften the peel. |
| Z moves are twice the distance asked | The motor driver lost its settings in a motor-power cut (seen with older firmware) | Shut down and restart the laptop so the controller restarts, and report it. |
| The galvo doesn't move and the laser shows no light, though the page shows commands | The galvo electronics were powered after the controller started | Check the machine supplies are on, shut down the laptop, and start it again. |
| **Arm laser** refused | The galvo is outside its allowed range (0 V after a controller restart) | Press **Centre** on the Galvo card. |
| **Expose** refused | The image showing is black | Choose **White**, **Grid** or **Focus** first. |
| The projector shows lines of text | The service isn't running (stopped or restarting) | Wait a few seconds, or **Restart service**. |
| The projector LED comes on by itself at power-up | Normal start-up behaviour of the projector | The service switches it off once it can reach the projector (about 40 s after boot), and within a second whenever it comes back on. |
| **Start print** refused | One of the [pre-print checks](printing.md#before-you-start) failed | Read the message: home Z, set the film zero, check the projector, or re-slice a job that has no LED level. |
| The part pushes the film down at each layer; first layers too thick | No settling time before exposure | Set **Wait before exposure** to at least 1 s. Check for lost steps. |
| Laser lines or the edge trace miss their place | The alignment is out of date | Run the [alignment](calibration.md#align-the-laser-to-the-projector) again. |
| Camera picture blurred or badly exposed | Focus on Auto, or the settings were changed | Set focus to Manual; check exposure; **Reset camera to its defaults** if needed. |
