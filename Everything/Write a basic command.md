*Part of [[Subsystem Stub]]*

---

What a command is, how we build them, and how to hook one up to a button or an auto.

## Outline
- [ ] **What a command is**
  - [ ] "Something the robot does for a while"
  - [ ] The 4 parts: `initialize`, `execute`, `isFinished`, `end` (we almost never write these by hand)
  - [ ] Requirements: starting a command that needs the collector cancels whatever was using it
- [ ] **Factories from `SubsystemBase`** (these require `this` automatically)
  - [ ] `run`, `runOnce`, `startEnd`, `runEnd`, with when each one ends
  - [ ] Real examples: `intakeCommand()` (`run`), `stopRollersCommand()` (`runOnce`)
  - [ ] Lambdas `() -> { }` and method references `this::spin` (you already explain lambdas in [[Choreo Marker Commands]], so link it)
  - [ ] Warning callout: `run(...)` alone never stops the motor when it's cancelled
- [ ] **Factories from `Commands`**
  - [ ] `sequence`, `parallel`, `deadline`, `repeatingSequence`, `waitSeconds`, `waitUntil`, `either`, `print`
  - [ ] Gotcha: `Commands.run(..., this)` needs the subsystem as the last argument or it won't be required
- [ ] **Decorators**
  - [ ] `.withTimeout`, `.until`, `.andThen`, `.finallyDo`, `.repeatedly`, `.withName` (always name them, it makes AdvantageScope readable)
  - [ ] Walk through `agitateCommand()` in `Collector.java` line by line as the "putting it together" example
- [ ] **Hooking it to a button** (`control/ControllerBinding.java`, `setupControls()`)
  - [ ] `onTrue`, `whileTrue`, `onFalse`, `toggleOnTrue`
  - [ ] The `teleop` trigger and `.and(...)`
  - [ ] Read `setupControls()` first so you pick a button nobody uses
  - [ ] Note: in teleop the collector, indexer and shooter are all run by one big `mechanismCommand()` that calls their plain `void` methods (`collector.collect()`, `indexer.feed(...)`). Explain why, so students aren't confused that those don't look like normal commands.
- [ ] **Default commands**
  - [ ] `setDefaultCommand(...)`, the drivetrain's joystick drive is the example
- [ ] **Hooking it to an auto**
  - [ ] `autoFactory.bind("Intake", collector.intakeCommand())`, link [[Markers]] and [[Choreo Marker Commands]]

## Code to show
- [ ] `spinCommand()` / `stopCommand()` for the Roller
- [ ] `agitateCommand()` and `smartDumpCommand()` from `Collector.java` (good "read this and explain it" exercises)

## Pictures to make
- [ ] GIF of a command showing up in AdvantageScope's `CommandsAll/` while a button is held

## Check yourself
- [ ] Explain why `run(...)` alone doesn't stop the motor when you let go
- [ ] Read `smartDumpCommand()` and explain it step by step
- [ ] Your Roller spins while you hold a button in teleop and stops when you let go

---
← Previous: [[Add motors and sensors]] | Next: [[Subsystem glossary]] | Up: [[Subsystem Stub]]
