# Configuring the robot physics

Configuring robot physics is very important for making autos. If you have the incorrect physics and dimensions, the auto will not work as intended. In general we will probably create a filled out version that has been tested that you can just copy onto your computer's Choreo instance.

## How to do it
1. **Open the main menu** — In Choreo, in the top left click the 3 lines, or "main menu".
    ![[Pasted image 20260613110140.png]]
2. **Open document settings** — Click the document settings option. It should pull up a screen that looks like this:
    ![[Pasted image 20260613110254.png]]

## What each option means
- **Mass:** How much the robot weighs — this includes bumpers and battery. We have a scale that we put the robot onto to measure its mass. It is important to specifically have this one be accurate.
- **MOI (Moment of inertia):** The other one where it is **extremely** important we get it correct. I made a whole dedicated page for it here: [[Calculating MOI]].
- **Bumper front:** Measure from the edge of the bumper to the center of the robot. This applies for all of the bumper sides, and the back.
- **Wheel radius:** Another one where you'll want to use the CAD to measure it, but if the CAD doesn't have the same grip tape/tread that we do on the actual robot, then measure the wheel.
- **Wheel COF:** Something you generally do not get yourself. This is published by the brand that made the wheel.
- **Motor rev/Wheel rev:** This will change year by year, but the manufacturers of the swerve module will publish them. In 2026 we used the MK5 swerve modules, which had different gearings: L1, L2 and L3. You can usually just search it up and it will say something like 6.37:1, so you can simply type 6.37.
- **Motor max speed:** Another thing you can just look up online. For Kraken X60's it is 6000 RPM.
- **Motor max torque:** Also look this up. For a Kraken X60 it is 7.09 N\*m, just type it as 7.09 N\*m.

---
← Previous: [[Creating a project and saving it]] | Next: [[Building and naming paths]] | Up: [[Choreo]]
