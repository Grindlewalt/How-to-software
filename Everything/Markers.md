Markers are the last part of Choreo we will go over. At some point you may have wondered how the other parts of the robot will be used aside from just driving, and that is a great question. Markers are the answer.

1. Inside of Choreo, find a point where you may want a subsystem to do something. In my auto, I'm going to be using the collector right when I'm outside of the trench, which will be waypoint 2
2. Once you have the waypoint that you want to the robot to activate its subsystem, go to ChoreoAutoCommandHandler.java (com > ck4911 > auto), and scroll down to the `bindEventMarkers()` method. Find the `autoFactory.bind` lines and read the names for each event:
   ```java
// ---- Collector ----
autoFactory.bind("Intake", collector.intakeCommand()); // deploy + run rollers
autoFactory.bind("StopCollect", collector.stopRollersCommand()); // rollers off, stay deployed
autoFactory.bind("Stow", collector.stowCommand()); // raise, rollers off

// ---- Shooter ----
// Home the hood against its hard stop (use at t=0 so the hood has a known zero).
autoFactory.bind("Down", shooter.performHoodHoming());
   ```
   There are no shooting markers anymore. The pre-spin, the shot and the collector jitter all happen automatically at every **split** waypoint (the robot stops there and shoots), so you don't need a marker for them. Any old shoot/index markers left in a path are just ignored.

   > [!warning]
   > Commands bound here must **not** require the drivetrain, or they will cancel the trajectory that is following the path.
3. You can read that there are names like "Intake", "Stow", etc...  Note that each is case sensitive. If you are curious about what each command does, you can command/windows + click on the command. (in the Intake bind, I'd click the intakeCommand() and it will take you to where you need to see what the method does.)
4. Here I'm going to click on the marker, then click on the waypoint, then set the string to be "Intake" and you can leave the 3rd field set to none
   ![[ScreenRecording2026-06-16at3.49.59PM-ezgif.com-video-to-gif-converter.gif]]
5. Make sure to rebuild it for the marker to take effect, now when the robot drives, that command is ran. Here is a tutorial on how to create your own command and also a quick explainer on what is actually happening inside of the code.
   
   ### Resources:
   [[Choreo Marker Commands]]

---
← Previous: [[Constraints]] | Up: [[Choreo]]
