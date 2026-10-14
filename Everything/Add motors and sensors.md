*Part of [[Subsystem Stub]]*

---

The `IoReal` file, the only file that actually talks to hardware. Continues the Roller from [[Create a SubsystemBase class]]. Our motors are CTRE TalonFX (Krakens) and our angle sensors are CANcoders, so this is all CTRE's Phoenix 6 library.

## Outline
- [ ] **Declaring the device**
  - [ ] `new TalonFX(constants.motorId(), canBus)`
  - [ ] The CAN ID has to match Phoenix Tuner X (link [[Phoenix Tuner X]])
  - [ ] `@Named("Bob") CANBus`: we have two buses, `rio` and our CANivore called "Bob". Mechanisms are on Bob. (In sim it quietly uses `rio`.)
  - [ ] CANcoders work the same way (`new CANcoder(id, canBus)`), example in `CollectorIoReal`
- [ ] **Configuring it** (`TalonFXConfiguration`)
  - [ ] Build it with `.withSomething(...)`, send it with `getConfigurator().apply(...)`
  - [ ] `Slot0Configs`: the PID + feedforward gains (link [[PID tuning]])
  - [ ] `CurrentLimitsConfigs`: we use 80 A stator so we don't cook motors or brown out
  - [ ] `MotorOutputConfigs`: brake vs coast, and `InvertedValue` (the fix when it spins backwards)
  - [ ] `MotionMagicConfigs`, `FeedbackConfigs`: mention, point at `CollectorIoReal` for a real example
  - [ ] `tryUntilOk(5, ...)` retries if the CAN bus was busy
- [ ] **Reading sensors** (status signals)
  - [ ] Grab each `StatusSignal` once in the constructor (`motor.getVelocity()` etc.)
  - [ ] Every loop: `BaseStatusSignal.refreshAll(...)`, then copy into `inputs` with `.getValue().in(RadiansPerSecond)`
  - [ ] `.isOK()` false = motor didn't answer = probably unplugged
  - [ ] `Debouncer` for the connected flag (heads up: see the glossary note about which direction ours delays)
  - [ ] `setUpdateFrequencyForAll(50, ...)` and `optimizeBusUtilizationForAll(...)`: keep the CAN bus from clogging
- [ ] **Telling the motor what to do** (control requests)
  - [ ] Make the request object once, then `motor.setControl(request.withVelocity(...))`
  - [ ] Table of the ones we use: `VoltageOut`, `VelocityVoltage`, `MotionMagicVelocityTorqueCurrentFOC` (indexer + collector rollers), `PositionDutyCycle` (collector pivot), `stopMotor()`
  - [ ] Teaching tip: status signal = motor talking to us, control request = us talking to the motor
- [ ] **The `@Override` methods**
  - [ ] This is where "the interface promises it" becomes "the motor does it"
- [ ] **Adding a second motor**
  - [ ] `IndexerIoReal.java` is literally one motor's worth of code, doubled

## Code to show
- [ ] Your full `RollerIoReal.java` (one TalonFX, `VelocityVoltage`)
- [ ] The pivot config in `CollectorIoReal.java` as the "advanced" example (gravity compensation, CANcoder feedback, gear ratio)

## Pictures to make
- [ ] Phoenix Tuner X showing a motor's CAN ID matching the code
- [ ] AdvantageScope plot of a motor's velocity and current while it spins (on the real robot)

## Check yourself
- [ ] Find the indexer motor's CAN ID in code and in Phoenix Tuner X, and they match
- [ ] Explain status signal vs control request
- [ ] Know where to flip the motor direction

---
← Previous: [[Create a SubsystemBase class]] | Next: [[Write a basic command]] | Up: [[Subsystem Stub]]
