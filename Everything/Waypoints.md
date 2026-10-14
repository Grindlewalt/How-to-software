In this section we will go over the Pose waypoint, Translation waypoint and the Empty way point. We will go over their uses and their constraintss that can be applied.

### Setting initial position and moving forward
In the top left point on the field section of Choreo, you will see a rectangle with a dot in the middle and a triangle on the outside, click on that.
![[Pasted image 20260613184414.png]]

Now with that clicked, go down to the field and click on the blue alliances start line, the initial robot position will appear.
![[Pasted image 20260613184532.png]]

Now click again a bit further in the blue territory, this will place down a second Pose waypoint.
![[Pasted image 20260613184746.png]]
A few things to note in the diagram above, inside of the red circle there is a option that says "waypoints", currently there are 2 waypoints, any of the three waypoint options in the top (Pose waypoint, Translation waypoint and Empty waypoint), those waypoints will appear under the "WAYPOINTS" menu. The other thing to note is that now that I have more then one way point, a new button in the bottom right corner of the screen has appeared. I have circled it in green. When you click on it, it will build the trajectory, and if you have already built it, will update the one inside of the code, you will have to rebuild and redeploy the code for the changes to take effect.

After clicking it, a "play button" will appear that allows you to see what the built auto will do. This is a good time to watch for all 4 corners of the robot to ensure that clipping wont happen. So, congratulations, you've made your first auto! We could deploy this now and run it and the robot would move, though this auto isn't to helpful yet, so lets  learn some concepts real quick!
### Waypoint ordering:
So, lets take my auto "GrantsAutos" and add a third Pose waypoint, and rebuild it.
![[ScreenRecording2026-06-13at10.00.29PM-ezgif.com-video-to-gif-converter.gif]]

As we can see it goes to 1, then 2 and finally 3, but if i rearrange them, it goes in that order, this is a more exaggerated example here:
![[ScreenRecording2026-06-13at10.08.16PM-ezgif.com-video-to-gif-converter.gif]] 
So, you can rearrange the order in which pose waypoints are to change the order the robot will drive to each, try that out now with a 3 waypoint auto.

### Pose waypoints 
Pose waypoints are going to be one of the most used tools in Choreo, and they are very simple to use.
Pose waypoints track both rotation and location. Here is a good exercise to try and learn the concept of it, make sure to delete the 3 waypoints you already placed down.
1. Place the Translation pose down on the starting line
2. Rotate it 180 degrees (if it says rads, just delete the rads part and replace it with "deg")
   ![[Pasted image 20260613222132.png|448]]
3. Next right in front of it, place down another Translation waypoint, don't rotate it this time
4. Finally add another one on the other side of the field, this can be a random rotation, whatever you want.
5. build it and watch the robot spin around (usually not over 180 degrees so it wont be a helicopter.)

**Using Max angular velocity constraint**
Quick Disclaimer: They way I am using a Max angular velocity constraint isn't really that practical. If you are ever encounter this issue in real life, just use a Pose translation so that you are explicit in the rotation you want the robot to go, however, Choreo is built to be very optimized from a physics standpoint so even if you are explicit about the rotation of the robot, the robot may still have some angular momentum that Choreo is trying to account for, rotating the robot, which is the use case that I am describing here. So yes, there are some flaws in this demo, it was just the one I decided to use because to understand Max angular velocity, you only have to understand the Pose waypoint, though I'll probaly introduce Translation waypoints before. Thats all! read on!

The max angular velocity constraints determines how fast the robot can rotate. You will pick 2 or more waypoints where you want this constraint to take place. You will get an error if constraints conflict with a Translation waypoint (ex: you set a max angular velocity between point 1 and 2 to be 0 deg/s but there is a 180 degree difference between 1 and 2, it is impossible to not rotate and have a rotation requirement at the same time!) so it is best practice to have the 2 Pose waypoints to either A) have the same rotation or B) have it be a Pose -> Translation -> Pose and then have an angular constraint between Translation -> pose. Here are the 2 examples and then I'll tell you how to apply a max angular constraint:

**Option one:** Don't rotate it (sometimes can be hard especially when moving quickly)
![[ScreenRecording2026-06-13at10.48.01PM-ezgif.com-video-to-gif-converter.gif]]

**Option 2:** use max angular velocity constraint
![[ScreenRecording2026-06-13at10.52.58PM-ezgif.com-video-to-gif-converter.gif]]
Notice how it is a Pose -> translation (Which has not rotation value) and then Pose again, with my final rotation included. With the Max angular velocity constraint, the robot does not start rotating while still under the trench (the little gap that the robot drove through), which would lead to clipping, and in real life, a collision.

Before we get into Max angular velocity constraint, I want to briefly go over the Translation waypoint, as it will be a prereq to understanding the Max angular velocity constraint.

### Translation waypoint and Max angular velocity constraint
The translation way acts very similar to the Pose waypoint except that it does not affect rotation. You cannot start a path with a Translation waypoint, only a Pose waypoint can be used so that the robot knows its rotation.
![[Pasted image 20260614095643.png]]

Now if i start it properly with a Pose waypoint, notice how it doesn't rotate at all durning the routine:
![[ScreenRecording2026-06-14at9.58.50AM-ezgif.com-video-to-gif-converter.gif]]

If we however add in another Pose waypoint, the robot will begin rotating again, even if we didn't initially want that. Now yes, we could use a Pose waypoint, and if you are ever actually caught in this situation, you should use a Pose waypoint, but in this case, I want a simple example to show what the max angular velocity can do.
![[ScreenRecording2026-06-14at10.01.07AM-ezgif.com-video-to-gif-converter.gif]]
But if we add the Max angular velocity constraint to waypoints 1-5, we get this:
![[Screen Recording 2026-06-14 at 10.14.07 AM.gif]]

If you also have a reason for a slow turn, you can simply increase it from 0 rads/s, but most of the time I use it for making sure the robot does not rotate at all, though there will be a use case where you'll not want the robot to rotate.

---
← Previous: [[Adding the auto to the auto picker and code]] | Next: [[Constraints]] | Up: [[Choreo]]
