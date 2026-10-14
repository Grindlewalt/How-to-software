# Run an autonomous routine

Running an autonomous routine is basically just enabling the robot in Autonomous mode, so a lot of this overlaps with [[Enable and disable the robot]]. The big difference is that the robot runs its own pre-coded path instead of listening to the controllers, so being in the right spot matters a lot more.

## How to do it
1. **Pick the auto** — Pick the auto you want from the auto chooser (the dropdown on the dashboard, we use Elastic as of 2026, but it should be the same for most choosers). Make sure it's the right one for how the field is set up and where the robot is starting. Autos are pre-coded paths, so if you run the wrong one, or the robot isn't where that path expects it to start, it will happily drive off and do the wrong thing, and yes I have done that with the small little 35 pound software chassis and it ran into the driver station, knocking the whole thing down and breaking the big enabled alarm on the driver station (if you are reading this in the future I hope I fixed it :).

    > [!todo] Find the auto chooser's name in Network Tables
    > if you're reading this, it means I didn't do this todo lol, js lmk so I can fix it

2. **Set the start position** — Put the robot in its correct starting position on the field. Line it up the same way it was when the auto was made (this is usually a specific spot against the wall or on a tape mark). Make sure that PhotonVision also knows where it is on the field. You can confirm this by opening the PhotonVision GUI on photonvision.local. There you can see if the cameras are seeing an AprilTag, thus getting position data. You can also check under AdvantageScope and see if the robot is in the same position as it is in real life.
3. **Set the mode to Autonomous** — Make sure the right most box above the Enable/Disable buttons is set to "Autonomous" (this is the box that is normally in "TeleOperated" for driving). If it's still on TeleOperated, clicking enable will just hand control to the drivers instead of running the auto.
4. **Clear the field, then enable** — Same safety stuff as enabling normally, check that any controllers aren't sitting face down on the table, make sure the field is clear, and make sure everyone knows the robot is about to move. When running autos, really, really make sure no one is on or in the general vicinity of the field bc 135 pounds of aluminum moving really fast would be considered "sub optimal" for most ankles, shins and knees. The robot will move on its own and people don't expect that, so it's worth saying the "enable" loudly. When you're ready, yell "Enabling" and click the green "Enable" button (how many times can you say enable in 2 sentences?). You'll know it's running when the RSL (Robot Signal Light, aka the orange light) begins blinking and the robot starts moving on its own. The second you click enable it will start moving, which can be a little surprising the first time.

The auto will run for the length of the autonomous period and then stop (in a real match it switches over to teleop automatically). If you need to stop it early, just click the red "Disable" button and the robot will cut power and stop wherever it is. When running a new auto for the first time, do this thing called "riding the E-Stop" where basically the entire time you are really watching the robot and have your hand right over the E-Stop. Stuff can seem like it's going really well and then it will just randomly on the way back run into a wall, literally, and it's not the end of the world if it happens, but still not great as it can damage the stuff it hits.

## Troubleshooting
**Nothing happens when you enable:** Same checks as [[Enable and disable the robot]], make sure the robot is connected (battery icon green and updating, "Communication" status light green) and that it's not in E-Stop. If it's connected and you still get nothing, make sure the mode box is actually on "Autonomous" and not "TeleOperated".

**It enables but the robot doesn't move:** Double check that you actually selected an auto in the chooser. If no auto is selected (or an empty/"do nothing" one is), the robot will sit there doing nothing, which looks exactly like it's broken but isn't.

**It runs the wrong path or drives somewhere weird:** This is almost always either the wrong auto selected in the chooser, non updated vision, or the robot starting in the wrong spot. Reset the robot to its correct starting position, double check the PhotonVision GUI and that it's seeing tags / check AdvantageScope, and double check the chooser before trying again. There has been one weird bug where it consistently, no matter the orientation or location of the robot, would go backwards. If this happens, just let the standing software lead sort it out because it was a simple solution, but a complex journey to get to the solution. Happy auto making!!! This is my favorite part of software.

---
← Previous: [[Connect controllers]] | Up: [[FRC Driver Station]]
