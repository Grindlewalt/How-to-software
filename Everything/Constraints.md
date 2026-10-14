During this lesson I strongly encourgae you open Choreo and build autos with constraints so you can get a hands on idea of how Constraints work. Constraints are critical to making a good auto and are a core part of Choreo (Like waypoints and markers) and you will need a strong understanding of them as without constraints, the robot just flies around.



TODO: make a video for this one (if you are reading this, it means i havent made the video yet)

### Brief overview of each:
* **Stop point:** A point where the robot comes to a complete halt before immediately starting up again. There's no delay - it just momentarily stops.
* **Max velocity:** The maximum speed the robot can move, measured in meters per second (m/s).
* **Max acceleration:** Not to be confused with max velocity. This is how quickly the robot can change its speed, measured in meters per second squared (m/s²).
* **Max angular velocity:** This is the maximum the robot will spin around (measured in rad/s)
* **Point at:** We will skip this for now as you will rarely use it and it is a rather finicky feature.
* **Keep in circle:** This is a constraint that requires all parts of a robot to stay in a circle, if that is not possible (ex: the circle is too far away from a waypoint, the circle is too far, some other random reason) it will throw an error, and you will have to change stuff around till it works.
* **Keep in rectangle:** The same as the circle, but its a rectangle (Hence the name, keep in **rectangle**)
* **Keep in lane:** The Keep in lane constraint creates an actual lane that the robot must stay inside of, so when you create a path an Choreo optimizes and accounts for momentum, it creates lines that may go a bit outside of the actual line, so the keep in lane makes sure that the robot follows the line you made, to a certain tolerance.
* **Keep out circle:** This works as the name implies, it is a circle that the robot must keep out of, again, if the keep out is too close (as in for the robot to go to the point, it also must go into the circle, that can't work.) it will throw an error

### How to apply constraints
Applying the constraints can be a bit confusing at first, but once you understand its very simple too use. After this, we will go into how to use each constraint and also some use cases (the examples won't always be perfect/over simplified where there are better solutions, but it is for learning/education.)

1. Make a simple path, remember the rules: The first waypoint has to be a Pose waypoint, Pose waypoints affect Translation (where it is on the X and Y) and translation only affects the Translation. Have the path be more then 3 waypoints, then build it. this will be mine (note that I used translation waypoints as not to interfere with any explicit rotation):
   ![[Pasted image 20260614214534.png|376]]
2. Every constraint except the Stop point is applied the exact same way: pick the constraint in the toolbar at the top, then click the first and last waypoint you want it to cover. The [[#Max Velocity]] section walks through it step by step, so if this is your first time, start there. The Stop point is slightly different, and it's covered in its own section right below.

### Stop points
The Stop point constraint will bring the linear velocity to 0, once its speed is zero, it will start accelerating again.

**Application**
1. The Stop point constraint is the very first constraint
   ![[Pasted image 20260614233233.png]]
2. The stop point will only apply to one waypoint unlike all other constraints which must apply too two or more waypoints.
   ![[Screen Recording 2026-06-14 at 11.35.03 PM.gif]]
3. As you can see, the point that I added a stop point too stopped fully and then started accelerating again, there is no delay on it, if you need the robot to stop for say 200 ms, you have to use an event marker then inside of the .traj file, add a delay manually. The [[Stop and Delay in Choreo]] page will help you with this.

### Max Velocity
The maximum speed the robot can move, measured in meters per second (m/s). This is the one I'd learn first, since every other constraint (except the Stop point) gets applied the same way.

1. Use the simple path you built in [[#How to apply constraints]] (more than 3 waypoints, starting with a Pose waypoint, already built).
2. Click the Max velocity button in the toolbar at the top:
   ![[Pasted image 20260614222938.png|472]]
3. Now click the waypoints you want this constraint to cover. Let's say I want the robot to go no faster than 1.8 m/s between waypoints 2 and 3. With Max velocity selected in the toolbar, I click waypoint 2, then waypoint 3. A dotted yellow line should show up between them. If it doesn't, make sure the tool is actually selected (it's highlighted in yellow when it is).
   ![[Screen Recording 2026-06-14 at 10.40.31 PM.gif]]
4. Set the constraint's speed to 1.8 m/s, then rebuild the path.
5. Hit play and watch: the robot slows down between waypoints 2 and 3, then speeds back up once it's past the constraint. You'll use this one a lot, any time the robot needs to slow down to do something, like going through a tight spot or collecting.

### Max acceleration
Max acceleration not to be confused with max velocity. This is how quickly the robot can change its speed, measured in meters per second squared (m/s²).
1. Find a spot in your routine where you may not want the robot to accelerate too much. This could be a situation where you are trying to compound sub system movement with driving, like an elevator, and don't want to shoot forward too fast, loosing balance. This will commonly happen after a Stop point for a collection from a source or a ground collect. In this example, I'm going to leave my Stop point on waypoint number 2 and then add a max acceleration on point 2-3. This will be the same exact process as Max velocity, so in this GIF I won't add the process of applying the the constraint.
   ![[Screen Recording 2026-06-14 at 11.52.14 PM.gif]]
2. As you can see from points 2-3 it does accelerate/get faster gradually, but once it gets past point 3, it accelerates much faster, as there is no constraint on it.

### Max angular velocity
This is the maximum the robot will spin around (measured in rad/s)

1. I'll be changing my auto to have a bit more spin momentum to it, and I'll have a before and after of what the Max angular velocity does to the routine.
   ![[Adobe Express - Screen Recording 2026-06-15 at 1.40.53 PM.gif]]
2. This is going to be the first auto that I use in our example that is going to be on the more advanced side with multiple different constraints and waypoints. The collector is on the front of the robot, and is supposed to collect the yellow balls in the middle of the field. Pose waypoints 6-7 both face in a way that should allow for collection of balls, but there are points where the robot is rotated over 90 degrees, and you would need a lot of pose waypoints to make sure that the robot faces in the right direction. So what we can do is use a Max angular velocity constraint to ensure the robot does not rotate too much. With the max angular velocity for 4-5 and 6-7 applied, we can see the affect (Note that it is best practice to set max angular velocity to .01 rads/s, it is close enough to 0 that the tolerance of the robot being able to rotate that precisely will not be affected, if you set it to 0 rads/s Choreo will run into some bug (Rounding error maybe?) where it thinks the robot has to rotate a very tiny amount, throwing an error)
   ![[ScreenRecording2026-06-15at1.57.05PM-ezgif.com-video-to-gif-converter.gif]]
3. As we can see, while the robot is collecting, it is always faced forward in the correct way.

### Keep in circle/rectangle
The keep and circle rectangle are the same thing, but with different shapes. This constraint will ensure that during whatever waypoints you select, all 4 corners of the robots bumper will stay inside of said shape
1. Find 2 points that may overlap/clip a field element, even if you don't have it set to where there may be a collision, sometimes momentum accounting can lead to some overshoot and collision. For my example I chose waypoint 3-4, and used the keep in rectangle.   ![[ScreenRecording2026-06-15at4.37.47PM-ezgif.com-video-to-gif-converter.gif]]
2. As you can see, between point 3-4 the 4 corners of the robot never went outside of the box. In general you will find that the rectangle tool is a bit more useful then the circle tool, but there are some use cases for the circle.

### Keep in lane
This is and Max velocity are the 2 constraints I use most. The Keep in lane constraint creates an actual lane that the robot must stay inside of, so when you create a path an Choreo optimizes and accounts for momentum, it creates lines that may go a bit outside of the actual line, so the keep in lane makes sure that the robot follows the line you made, to a certain tolerance.
1. For this one I will be creating an auto where you need the bot to go strait, but Choreo defaults to creating a rounded line.
   ![[Pasted image 20260615164844.png]]
2. As you can see, the robot goes out of the field boundaries, quick side note: you will see that by default, Choreo adds a Keep in rectangle constraint that is the entire field, when it is checked and rebuilt, the robot will not leave the field, I recommend having this, but I disabled it for this example.
3. I will now add the Keep in lane constraint between waypoint 9 and 10:
   ![[Screen Recording 2026-06-15 at 1.57.05 PM 1.gif]]
4. No more clipping! Again, extremely helpful. 

### Keep out circles 
The keep out circle works very similarly to the keep in circle, except instead of all parts of the robot staying inside of the keep in circle, no parts of the robot go into the keep put circle. There, for some reason, is no keep out rectangle. The process for this is the same as all of the other circles and rectangles, if you have questions you can just ask me.


### Your task
Your task, now that you have finished reading all of this and following along in your own Choreo instance is to make an auto that uses all of the constraints (except for point at). You have to have it not clip though any field elements, and have it have an actual goal. You can pick any game season to try this out with. If you need ideas for what the auto should look like, just look up "FRC 254 clean robotics video" and it will be a match of a specific team from auto to end of teleop. 

---
← Previous: [[Waypoints]] | Next: [[Markers]] | Up: [[Choreo]]
