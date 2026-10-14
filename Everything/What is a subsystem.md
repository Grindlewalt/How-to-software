*Part of [[Subsystem Stub]]*

---

The big-picture page: what a subsystem is, why every one of ours has the same 6 files, and what happens every loop. No coding yet, just reading.

## Outline
- [ ] **What a subsystem is**
  - [ ] One mechanism on the robot = one subsystem class that owns its motors (collector = the arm that picks balls up, indexer = rollers that feed the shooter)
  - [ ] The big rule: only one command can use a subsystem at a time, so two things never fight over a motor
  - [ ] Teaching tip: point at the real mechanisms on the robot while explaining this
- [ ] **The 6 files** (open the `collector/` folder side by side while reading)
  - [ ] `Collector.java`: the "brain" (commands and logic, never touches a motor directly)
  - [ ] `CollectorIo.java`: the menu of what the brain can ask the hardware to do + the list of sensor values (`CollectorIoInputs`)
  - [ ] `CollectorIoReal.java`: talks to the real motors
  - [ ] `CollectorIoSim.java`: fake version for the sim (ours are empty, so the collector does nothing in sim)
  - [ ] `CollectorConstants.java`: a box of numbers (IDs, gear ratios, gains)
  - [ ] `CollectorModule.java`: fills in the numbers and picks Real vs Sim
  - [ ] Point out that `indexer/` has the exact same 6 files
- [ ] **Why split it up** (AdvantageKit IO layers)
  - [ ] The same brain code runs on the real robot and in the sim, only the IO file swaps
  - [ ] All sensor readings go through `updateInputs`, so everything gets logged and you can replay a match in AdvantageScope
  - [ ] Link back to how `providesCollectorIo` picks the IO (you already explain it in [[Choreo Marker Commands]])
- [ ] **How it all connects** (Dagger)
  - [ ] `robot/RobotComponent.java` lists every Module
  - [ ] `@Inject` on a constructor = Dagger builds it for you, you never write `new Collector(...)`
  - [ ] `ControllerBinding` hooks commands to buttons, `ChoreoAutoCommandHandler` hooks them to markers
- [ ] **What happens every 20 ms**
  - [ ] Order: read sensors → log them → run commands → commands tell the motors what to do
  - [ ] Show `periodic()` in `Collector.java` as the real example

## Pictures to make
- [ ] Diagram of how the files connect (Module → Constants + IoReal/IoSim → Collector → ControllerBinding / autos). A mermaid `flowchart` works in Obsidian.
- [ ] Diagram of one loop (mermaid `sequenceDiagram`)
- [ ] Screenshot of the `collector/` folder in IntelliJ

## Check yourself
- [ ] Name all 6 files and say what each does
- [ ] Explain why `Collector.java` never says `TalonFX`
- [ ] Explain what would happen if two commands tried to use the collector at once

---
Next: [[Create a SubsystemBase class]] | Up: [[Subsystem Stub]]
