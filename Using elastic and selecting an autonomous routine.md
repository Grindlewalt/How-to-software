# Using Elastic and selecting an autonomous routine

Part of [[Simulator]]

Elastic is another tool that works with NetworkTables. It is used as a dashboard to display things like battery, match time, and the speed or current draw of a mechanism, and it is also how we select autos.

In this lesson we will use Elastic to select which autonomous routine to run in the simulation, then run it. Selecting an auto this way carries over to the real robot, since (as of the 2026 season) we use Elastic in competition.

## Configuring Elastic to select autos
1. **Make sure the simulator is running.** If it isn't, follow [[Launching and configuration of the simulator]] to start it (run your `simulateJava` Gradle task in IntelliJ). Elastic can only show data from a running robot or sim.
2. Open Elastic. It is an intuitive interface, and you will be greeted by an empty grid.

   ![[Pasted image 20261006161240.png|450]]

3. Check the bottom left corner. A green **Network Tables: Connected (127.0.0.1)** means you have successfully connected to NetworkTables (`127.0.0.1` is your own computer, where the sim is running). If it doesn't say that, the sim probably isn't running.
4. Look at the top left corner. There are 2 tabs: **Teleoperated** and **Autonomous**. For now we will not worry about Teleoperated. It works exactly like the Autonomous tab, but it is shown during the teleop part of the match instead. For example, you may not care about the auto chooser during teleop, but you would want the battery voltage or a shooter-ready indicator up there.
5. Click over to the **Autonomous** tab, then right click anywhere in the grid. Two options appear: **Add Widget** and **Clear Layout**. Click **Add Widget**.
6. This opens a familiar looking window of all the public NetworkTables topics (a topic is similar to a genre of entries).

   ![[Pasted image 20261006161555.png|450]]

7. Click **SmartDashboard**, and you will see a topic called **Auto Chooser**. You don't have to expand it. Drag and drop it into the grid anywhere (you may have to resize it).
8. The chooser lists the available autonomous routines. The number varies a lot, even between branches of the same repo.

   ![[Pasted image 20261006162114.png|450]]

Here is the full walkthrough:

![[ScreenRecording2026-10-06at4.17.58PM-ezgif.com-video-to-gif-converter.gif|450]]

## Enabling in the simulator and watching the autonomous
As you may remember from [[Basic uses of AdvantageScope]], there are 2 different ways to view the robot's position on the field, the 2D and 3D map. Either works equally well and they serve different purposes.

1. Make sure these 3 things are still running: the simulator, AdvantageScope and Elastic.
2. In Elastic, double check you have an auto selected. Some autos are for tuning only and may not run inside the simulator. If you don't have an auto, make your own! The step by step documentation for Choreo (the software we use to make autonomous routines) is here: [[Choreo]].
3. Go to AdvantageScope, make sure everything is connected, and make sure the Pose2d of the robot is showing on whichever map you want.
4. In the Sim GUI, click **Autonomous** in Robot State. If you're unsure how, review [[Launching and configuration of the simulator]].
5. The routine starts instantly. Either have AdvantageScope already in view, be quick to click over, or use the replay feature in the top middle, where you can drag the playback cursor back to the beginning of the auto.

Full walkthrough:

![[Screen Recording 2026-10-06 at 5.10.19 PM.gif|500]]

---
← Previous: [[Basic uses of AdvantageScope]] | Up: [[Simulator]]
