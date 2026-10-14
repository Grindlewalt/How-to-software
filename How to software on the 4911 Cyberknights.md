Welcome to the software team! This page is your roadmap. Below is everything a member needs to know to contribute to FRC software development. Work through each item, check it off when you can do it on your own (not just watch someone else do it), and follow the links for step-by-step guides.

---

## What you need to know to be on the software team
It is strongly recommended to first do [[Setting up your IDE]] as almost all lessons require for you to have an IDE configured, if you are comfortable with another IDE, then you can use that but all steps are written for InteliJ.
### Code
- [ ] Apply for GitHub education and get InteliJ ultimate installed → [[Setting up your IDE]]
- [ ] **Run the simulator on your own laptop** → [[Simulator]]
	- [ ] Have all software installed and understand basic uses of that software
	- [ ] Run the simulateJava gradle task and open the sim GUI
	- [ ] Bind your keyboard or a controller to Joystick 0 and drive the robot in Teleoperated
	- [ ] Connect AdvantageScope to the sim and show the robot's Pose2d on the 2D and 3D field
	- [ ] Add the Auto Chooser to Elastic, pick an auto, and watch it run in the sim
- [ ] **Stub out a basic subsystem** → [[Subsystem Stub]]
	- [ ] Name the 6 files in a subsystem folder and say what each one does
	- [ ] Explain what happens every 20 ms loop (read sensors → log → run commands → set motors)
	- [ ] Build a one-motor subsystem from scratch and wire it into `RobotComponent` and `ControllerBinding`
	- [ ] Write a command for it and bind it to a button
	- [ ] Read any method in `Collector.java` or `Indexer.java` and explain what it does
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
	- [ ] Calibrate cameras
	- [ ] Add cameras and their transforms into code


---

## Index of How-To's
- [[Setting up your IDE]]
	- [[Installing Git]]
- [[Simulator]]
	- [[Prerequisites]]
	- [[Launching and configuration of the simulator]]
	- [[Basic uses of AdvantageScope]]
	- [[Using elastic and selecting an autonomous routine]]
	- [[Troubleshooting the sim]]
- [[Subsystem Stub]]
	- [[What is a subsystem]]
	- [[Create a SubsystemBase class]]
	- [[Add motors and sensors]]
	- [[Write a basic command]]
	- [[Subsystem glossary]]
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
	- [[What is PhotonVision]]
	- [[Connect and configure]]
	- [[Calibrate cameras]]
	- [[Add cameras and transforms into code]]
