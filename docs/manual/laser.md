# Laser and galvo

By hand, the laser fires only while it is armed, the galvo is inside its allowed range, and someone holds **Hold to fire**. The **Galvo** and **Laser** cards on the Machine tab hold all the hand controls.

!!! danger "Eye safety"
    Wear 405 nm laser safety eyewear whenever the laser supply is on. Reflections off the vat walls can be brighter than the spot itself.

### Galvo

Galvo positions are in volts, because the scan optics aren't calibrated in mm yet. The field view shows the allowed range as a rectangle, and a dot where the galvo was last sent (nothing can read the mirrors back).

- Jog with **▲ +Y**, **◀ −X**, **+X ▶**, **▼ −Y** in steps of **0.01 V**, **0.1 V** or **1 V**.
- **Centre** moves to the middle of the allowed range.
- **Move to** takes typed x and y volts; a click on the field view moves there too.
- **Allowed range** limits every target. It is now X 0.39–7.01 V, Y −0.03–3.9 V, which covers the whole projected field. Change it with **Save range**, or from a [projection measurement](calibration.md#measure-the-projection-pixel-size).

A controller restart puts both axes at 0 V, which is outside the range, and arming is refused until the galvo is moved back inside. Use **Centre**.

### Firing the laser by hand

1. Put on 405 nm eyewear and switch the laser supply on.
2. Move the galvo inside the allowed range.
3. Set **Power** in % (**−1** / **+1**). Start at 1 %: that is what the alignment uses. **Power limit** caps what can be set; change it with **Set limit**.
4. Press **Arm laser**. It turns into **Disarm laser**, and the status line reads "armed · hold the button to fire".
5. Press and hold **Hold to fire**. The beam stays on while the button is held, and the status line reads FIRING with the power; a power change applies while it is on.
6. Release to switch the beam off, and press **Disarm laser** when done.

The beam also goes off 1 s after the browser stops sending hold requests (a dropped connection), on disarm, on STOP and when the service stops. The controller itself cuts it 0.5 s after the last laser command, so a frozen laptop can't leave it on. If the controller ever reports the laser on when the service didn't fire it, the service switches it off and logs an error.

Power is PWM duty at about 490 Hz, not calibrated in mW. At partial power, fast lines can come out dashed: at 120 mm/s the beam moves 0.24 mm in one PWM period.
