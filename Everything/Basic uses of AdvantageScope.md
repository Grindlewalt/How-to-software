

Part of [[Simulator]]

AdvantageScope is an easier way to view NetworkTables, which is everything the robot publishes: its position, motor positions, speeds and so much more. It lets us view all of that in a more graphic-based way. The most common thing you will use it for is viewing the robot's Pose2d (where the robot is relative to the field). Selecting the autonomous routine we want to run is done in Elastic, not here (see [[Using elastic and selecting an autonomous routine]]).

## Connecting AdvantageScope to the simulator
The sim launches a local server on your computer, and NetworkTables are viewed over a network connection. In this case the sim (the "robot") is on your computer, and the software viewing the published NetworkTables is also on your computer.

1. Launch AdvantageScope (it doesn't matter which tab you're on) and go to **File → Connect to Simulator**. Make sure **Default: NetworkTables 4** is selected. The shortcut `Cmd+Shift+4` (Mac) / `Win+Shift+4` (Windows) also works.

   ![[Pasted image 20261005212108.png|450]]

2. If nothing happens, or it just says "Searching", make sure **Default** is selected and the sim is still running (it can crash).
3. Once you're connected, try clicking the other 2 default tabs. They include a 2D and a 3D field.

## Viewing the robot on the field
While the exact path might change, you can find the Pose2d under **AdvantageKit → RealOutputs → Odometry → Pose2d**. Or type `AdvantageKit/RealOutputs/Odometry/` in the search bar.

Drag and drop the whole option into **Poses** (the center option). Then:
- In the **2D view**, a box with an arrow shows up representing the robot (the arrow points forward).
- In the **3D view**, you get a 3D model of that season's kit bot.

![[ScreenRecording2026-10-05at9.24.13PM-ezgif.com-video-to-gif-converter.gif|450]]

---
← Previous: [[Launching and configuration of the simulator]] | Next: [[Using elastic and selecting an autonomous routine]] | Up: [[Simulator]]
