# What is PhotonVision

Part of [[PhotonVision]]

The robot needs to know where it is on the field for multiple critical things, like auto align/aim, autonomous routines, and more. Figuring that out is called **odometry**: "using sensors on the robot to create an estimate of the pose of the robot on the field".

## Ways of estimating the robot's position
There are a few ways of finding your position on the field, but it boils down to 2 main ways:
- **Dead reckoning:** just using your wheel encoders and gyro to guess where you are. This slowly drifts, so the error keeps building up.
- **Pose estimation:** dead reckoning *plus* something like PhotonVision that periodically corrects your position, so the error doesn't keep building up.

## How PhotonVision corrects drift
PhotonVision uses cameras on the robot to take pictures of the field, then runs an algorithm on each picture to look for **AprilTags**. AprilTags look similar to QR codes and work in a similar way. For each tag it finds, PhotonVision:

1. **Identifies the tag.** Each tag has a number (which numbers exist depends on that year's field).
2. **Measures how big it looks.** It counts how many pixels the tag takes up. The camera is calibrated so the math works: if a tag 1 ft away takes up 100 pixels, then 2 ft away it takes up 50 pixels, and it can work out the distance for any size in between (like 75 pixels).
3. **Measures the distortion.** If the camera is looking at the tag at an angle, the tag looks skewed, and that tells it the angle.
4. **Publishes the result to NetworkTables**, something like "We are 5 feet away from AprilTag 13 at an angle of 30 degrees".

From there, the robot has a list of where every AprilTag is on the field, so it looks up where AprilTag 13 is, does the math to work out where *we* must be, and updates the dead reckoned position. That gets rid of any drift that built up (say, over the last few seconds), which keeps the position accurate throughout the whole match.

## Where this runs: the co-processor
All of that image processing is too much work for the roboRIO to do on top of running the robot. So PhotonVision runs on a separate small computer on the robot called a **co-processor**.

A **co-processor** is a second computer that takes on one specific job so the main controller doesn't have to. Ours does vision: the cameras plug into it, it runs PhotonVision on every frame, and it sends only the small results (like "tag 13, 5 feet away") to the robot over the network. The roboRIO never has to look at a picture.

We use **Orange Pis** as our co-processors. On the robot, they plug into the radio (the AUX ports from [[Configure the radio]]).

## Next step
The next step in this lesson is setting up the co-processor itself: [[Connect and configure]].

---
Next: [[Connect and configure]] | Up: [[PhotonVision]]
