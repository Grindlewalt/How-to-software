*Part of [[Simulator]]*

---

How to launch the simulator GUI and set up your keyboard or controller. Make sure you have everything in [[Prerequisites]] first.

## Setting up the Gradle task in IntelliJ

1. In IntelliJ, look at the top bar. To the right of the elephant icon is a box that says "Current File". Click it.

   ![[Pasted image 20261005195515.png|500]]

2. A drop down will appear. Choose **Edit Configurations...**
3. A panel will open. It may look different from mine, since sometimes there is already a default Gradle task. Click the **+** button in the top left.

   ![[Pasted image 20261005200116.png|500]]

4. In the drop down that opens, click **Gradle** (the one with the little elephant).

   ![[Pasted image 20261005200446.png|450]]

5. Leave everything alone (unless you want to experiment!), with two exceptions:
   - **Name:** call it whatever you want, as long as you can tell it runs the simulator.
   - **Run:** type (or copy and paste) `simulateJava`.
   Then click **OK**.
6. The dialog closes and the box at the top (where "Current File" was) now shows either your name or `YEAR-NAME [simulateJava]`. Mine for 2026-Rebuilt is `2026-Rebuilt [simulateJava]`.

## Launching it
1. Make sure your new configuration is selected in that box. If it isn't, click the drop down and select it.
2. Click the green triangle right next to the drop down.

   ![[Pasted image 20261005201558.png|500]]

3. This builds the code, then launches the Sim GUI. You will occasionally see errors in the output, but they shouldn't stop the sim from running. Some runtime warnings are harmless (like PhotonVision/camera spam or "joystick not found"), but a red **build failure** is not, so if it never launches see [[Troubleshooting the sim]].

## Configuring the sim
There isn't a ton to configure aside from your keyboard or controller. **By default, nothing is bound**, so the robot won't respond to any input until you do this.

### Setting up the keyboard
With Keyboard 0 the controls are **WASD** to drive (W/S forward and back, A/D strafe) and **E / R** to turn, plus the normal controls for whatever the controller has been configured to do. You can change the keys under **DS → Keyboard 0 Settings**.

1. Find the **System Joysticks** panel. It is usually in the middle left. If it isn't there, go to **DS** in the top menu and make sure **System Joysticks** is checked at the bottom.

   ![[Pasted image 20261005203907.png|450]]

2. Drag **Keyboard 0** onto **Joystick 0**. A real controller shows up in the same panel (the name varies, it is usually above the keyboard and sometimes in yellow), and you drag it the same way.

   ![[ScreenRecording2026-10-05at8.42.54PM-ezgif.com-video-to-gif-converter.gif|450]]

If you have multiple keyboards or controllers, you can make the driver Joystick 0 and the operator Joystick 1.

### Robot state
In the top right there is a **Robot State** window with a couple of options. These are the 4 you need to know:
- **Disconnected:** No Driver Station is attached, so the robot is never enabled and nothing is sent back to the driver station. **This is where the sim starts**, and joystick/keyboard input does nothing in this state.
- **Disabled:** The simulated robot is connected, but no motors will move and a few other processes are inhibited for safety.
- **Autonomous:** Runs whatever autonomous routine you have selected in Elastic (we will get there). Make sure the alliance color you have selected in the sim matches the alliance of the auto you're running (the station number doesn't matter).

  ![[Pasted image 20261005210932.png|350]]

- **Teleoperated:** Use this mode to simulate driving. WASD or joystick control will work now.

---
← Previous: [[Prerequisites]] | Next: [[Basic uses of AdvantageScope]] | Up: [[Simulator]]
