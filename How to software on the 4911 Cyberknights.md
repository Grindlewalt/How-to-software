Welcome to the software team! This page is your roadmap. Below is everything a member needs to know to contribute to FRC software development. Work through each item, check it off when you can do it on your own (not just watch someone else do it), and follow the links for step-by-step guides.

---

## What you need to know to be on the software team

### Robot basics
- [ ] **Power the robot on/off** — replace and test a battery, handle batteries safely, and know what a healthy voltage looks like → [[Robot Power and Batteries]]
- [ ] **Use the FRC Driver Station** — enable, disable, recover from an E-Stop, connect controllers, and run autonomous routines → [[FRC Driver Station]]
- [ ] **Configure and troubleshoot the radio** → [[Robot Radio]]

### Autonomous (Choreo)
- [ ] **Build an auto in Choreo** that → [[Choreo]]
	- [ ] Moves the robot along the X or Y axis
	- [ ] Rotates the robot
	- [ ] Uses the max-velocity constraint
	- [ ] Uses the keep-in-lane constraint
	- [ ] Use a subsystem command with a Marker  

### CTRE / Phoenix Tuner X
- [ ] **Use Phoenix Tuner X**, including → [[Phoenix Tuner X]]
	- [ ] Tuning PID and applying the values in code
	- [ ] Generating swerve drivetrain code
	- [ ] Updating device firmware

### Vision (PhotonVision)
- [ ] **Fully set up PhotonVision** → [[PhotonVision]]
	- [ ] Connect and configure cameras (name them, set the camera type)
	- [ ] Add cameras and their transforms into code
	- [ ] Calibrate cameras

### Code
- [ ] **Stub out a basic subsystem** → [[Subsystem Stub]]
- [ ] **Run the simulator on your own laptop** → [[Simulator]]

---

## Index of How-To's
- [[Robot Power and Batteries]]
	- [[Replace and test a battery]]
	- [[Safe battery handling]]
	- [[Reading battery voltage]]
- [[FRC Driver Station]]
	- [[Enable and disable the robot]]
	- [[Recover from an E-stop]]
	- [[Connect controllers]]
	- [[Run an autonomous routine]]
- [[Robot Radio]]
	- [[Configure the radio]]
- [[Choreo]]
	- [[Installing Choreo]]
	- [[Creating a project and saving it]]
	- [[Configuring the robot physics]]
		- [[Calculating MOI]]
	- [[Building and naming paths]]
	- [[Adding the auto to the auto picker and code]]
	- [[Waypoints]]
	- [[Constraints]]
		- [[Stop and Delay in Choreo]]
	- [[Markers]]
		- [[Choreo Marker Commands]]
- [[Phoenix Tuner X]]
	- [[PID tuning]]
	- [[Generate swerve drivetrain code]]
	- [[Update devices]]
- [[PhotonVision]]
	- [[Everything/Connect and configure]]
	- [[Add cameras and transforms into code]]
	- [[Calibrate cameras]]
- [[Subsystem Stub]]
	- [[Create a SubsystemBase class]]
	- [[Add motors and sensors]]
	- [[Write a basic command]]
- [[Simulator]]
