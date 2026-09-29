# Autonomous-Line-Following-Hovercraft
A hovercraft built for an engineering robotics class. It lifts on a cardboard deck with a trash-bag skirt, follows a black line using two light sensors, and controls its propulsion fan and rudder with LEGO SPIKE motors. Built by a team of five.

![Top view](images/top-view.jpg)

## Demo
[Watch the best run](PASTE-YOUTUBE-LINK-HERE)

## Design Overview
- **Deck:** cardboard, 10 in x 20 in (0.129 m²), reinforced with a misprinted 3D-printed fan guard
- **Skirt:** black trash bag, taped to the deck and supported with cardboard strips and hot glue
- **Lift and propulsion:** two Delta PFR1212DHE-SP00 fans
- **Power:** three Tenergy 12V 2000 mAh NiMH packs wired in parallel, plus the SPIKE hub battery
- **Controller:** LEGO SPIKE hub with two reflected-light sensors on the front
- **Steering:** a motor-driven rudder behind the propulsion fan
- **Power switch:** positioned so the rudder motor presses it when it turns at the start of a run, powering on the hovercraft
- **Throttle:** a second motor turns the knob on a speed controller board
- **3D-printed parts:** fan guards, speed controller housing, and rudder
- **Measured weight:** 2.318 kg (predicted 2.364 kg from the parts list, within 2%)

| Side | Bottom |
|------|--------|
| ![Side view](images/side-view.jpg) | ![Bottom view](images/bottom-view.jpg) |

## Programming
Programmed with LEGO SPIKE's block-based editor. Four programs run at the same time:

![Code](code/hovercraft-code.png)

1. **Line following:** waits 5 seconds so the hovercraft can be set down. The rudder then turns 110° one way, which presses the power button and turns on the hovercraft, and turns 110° back to center. It then loops forever, reading the left and right light sensors and subtracting them to get an error. If the error is small, the rudder returns to center. Otherwise it steers proportionally (error x 0.05).
2. **Throttle control:** a motor turns the speed controller knob to set fan speed, then holds it for the run.
3. **Steering limiter:** watches the rudder motor position and pushes it back when it enters certain ranges, to stop overcorrecting.
4. **Start signal:** three beeps at the start of a run.

## Testing and Results
- **Hover test:** passed the 5-minute hover requirement.
- **Line following:** reliably reached zone 3, then zone 4 after tuning.
- **Sharp 90° turn:** the hovercraft still slid too far on the low-friction surface before recovering.

## What Went Wrong

### Speed Controller Failure
![Failed speed controller](images/speed-controller-failure.jpg)

During testing, the speed controller board failed. A component (it appears to be an electrolytic capacitor) ruptured and left burnt debris on the board.

**Cause:** We never confirmed it. Our best guess is a short circuit somewhere in the wiring. Other possible contributors:
- The fans draw a large current, which may have exceeded what the board was rated for
- Supply voltage or current above a component's rating
- A wiring fault while working in a cramped, taped-together build

**What we'd do differently:**
- Check the controller's voltage and current ratings against the fan's peak draw before wiring it in
- Add an inline fuse between the batteries and the controller
- Check the wiring for shorts with a multimeter before powering up
- Keep a spare controller on hand

### Other Problems
- **Skirt ballooning:** a fully enclosed skirt with small holes wouldn't hover consistently. Cutting a large opening and bridging it with cardboard strips fixed it.
- **Battery drain:** the fans pull a lot of current, so fan speed varied between runs. Going from two battery packs to three fixed it.
- **Oscillation:** the steering limiter made the craft wobble side to side, but the small corrections turned out to help it hold the line edge into turns.

## Lessons Learned
- A stiff, evenly supported skirt matters more than the fan.
- Test the lift system early, since it took hours to get a reliable hover.
- Size the battery for peak current, not just capacity.
- Protect the electronics with fuses and rating checks before something fails.

## Author
Michael White and teammates
