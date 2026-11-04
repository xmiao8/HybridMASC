# The web interface

Open the printer's address in any browser on the lab network or the lab's Tailscale network; ask whoever runs the machine for it. The host's firewall turns away every other network. A window of at least 1000 × 700 keeps the header and tabs fixed while pages scroll beneath them.

![Header and tabs](img/ui-header.jpg)

The header is the machine's status line, the same on every tab:

- **Device chips** (Z stage, Galvo, Laser, Projector): a green dot means that part is connected and answering.
- **State badge**: IDLE, or what the machine is doing (printing, homing, a run in progress).
- **Laser badge**: "laser safe" while disarmed; it changes when the laser is armed or firing.
- **live**: the page is receiving updates (ten a second). If it drops, the values on the page are stale; reload.
- **STOP**: always one tap, see [Safety](safety.md).

The tabs are grouped by use:

| Group | Tab | Use it to |
| --- | --- | --- |
| Printing | **Print** | Watch a print: layer, phase, time left, layer preview, Z, LED and laser readouts, events. Start **Clean vat**. |
| Printing | **Slicer** | Turn a part into a job: step 1 **Slicing** (masks), step 2 **Processing** (laser lines, export). |
| Printing | **Jobs** | Start, preview, download, delete or upload saved jobs. |
| Hands-on | **Machine** | Move Z, the galvo, the laser and the projector by hand. |
| Hands-on | **Sequencer** | Build and run short machine programs from steps. |
| Setup and checks | **Calibrate** | Align the laser to the projector; measure the projected pixel size. |
| Setup and checks | **Camera** | Live view, zoom, snapshot and camera settings. |
| Setup and checks | **Demo** | Trace the edge of the projected field with the laser. |
| Right-hand tabs | **Logs** | The full event log. |
| Right-hand tabs | **Docs** | The design and implementation notes, with a **Download .md** button. |
| Right-hand tabs | **Settings** | Machine settings (Z speed, film zero, pixel size) and the peel profile. |
| Right-hand tabs | **System** | Light or dark theme, service status, restart the service or the computer, network and host details. |

A few rules hold everywhere:

- Hand controls on the Machine tab are disabled while a job runs.
- While a timed exposure runs, other commands that would change the machine are refused; STOP always works.
- Values that aren't calibrated yet are shown in machine units: galvo in volts, laser power as PWM %, projector LED as a 0–255 level.
