*Part of [[Subsystem Stub]]*

---

Build a subsystem from scratch, file by file. Uses a pretend one-motor **Roller** subsystem (basically a stripped-down Indexer) so students aren't overwhelmed by the Collector's two motors.

## Outline
- [ ] **Before you start**
  - [ ] Make a practice branch off `autos` so you don't mess up comp code
  - [ ] Make the folder `src/main/java/com/ck4911/roller/`
  - [ ] Copy the copyright header from any other file
- [ ] **Step 1: `RollerConstants.java`**
  - [ ] What a `record` is (a class that only holds data, getters for free)
  - [ ] Fields: motor ID, speed, `PidValues`, `FeedForwardValues`
  - [ ] What `@RecordBuilder` does (lets you fill it in by name in the module)
  - [ ] Compare to `CollectorConstants.java`
- [ ] **Step 2: `RollerIo.java`**
  - [ ] The `RollerIoInputs` class: one field per sensor value, put the unit in the name (`Rads`, `Amps`, `Celsius`)
  - [ ] `@AutoLog` generates `RollerIoInputsAutoLogged` at build time (it's red in the IDE until you build once, that's normal)
  - [ ] `default` methods with empty `{}` = do nothing unless overridden
  - [ ] Compare to `IndexerIo.java` (the simpler one)
- [ ] **Step 3: `RollerIoSim.java`**
  - [ ] Empty class with an `@Inject` constructor, same as `IndexerIoSim`
- [ ] **Step 4: `RollerModule.java`**
  - [ ] `@Module` / `@Provides` = recipes for Dagger
  - [ ] `providesRollerConstants()`: fill in numbers with the builder
  - [ ] `providesRollerIo(...)`: the REAL / SIM / REPLAY switch (copy from `IndexerModule`)
  - [ ] Warning callout: CAN IDs must be unique, list the ones already used (see [[Subsystem Stub]])
- [ ] **Step 5: `Roller.java`**
  - [ ] `extends SubsystemBase` (registers with the scheduler, that's why `periodic()` runs)
  - [ ] `@Singleton` (only one roller exists)
  - [ ] Fields: `rollerIo`, `inputs`, the tunable numbers, an `Alert`
  - [ ] Constructor with `@Inject`: make the tunables with `tunableNumbers.create("Roller/P", ...)`
  - [ ] `periodic()`: always `updateInputs` then `Logger.processInputs` first, then `LoggedTunableNumber.ifChanged(...)`
  - [ ] Private helpers (`spin()`, `stop()`) vs public commands (covered on [[Write a basic command]])
  - [ ] Teaching tip: have them read `Indexer.java` top to bottom first, then write theirs
- [ ] **Step 6: wire it in** (the step everyone forgets)
  - [ ] Add `RollerModule.class` to the list in `robot/RobotComponent.java`
  - [ ] Ask for a `Roller` in `control/ControllerBinding.java`'s constructor. Dagger only builds things somebody asks for, so if nobody asks, `periodic()` never runs and there's **no error**

## Code to show
- [ ] Each of the 5 Roller files in full (write and build them yourself first so you know they compile)
- [ ] `CollectorModule.java` and `IndexerModule.java` for comparison
- [ ] The modules list in `RobotComponent.java`

## Pictures to make
- [ ] The finished `roller/` folder in IntelliJ
- [ ] The `Roller` table showing up in AdvantageScope with the sim running (values will all be 0 since the sim IO is empty)

## Check yourself
- [ ] It builds (`./gradlew build`)
- [ ] The `Roller` inputs show up in AdvantageScope in the sim
- [ ] Explain what happens if you forget Step 6

---
← Previous: [[What is a subsystem]] | Next: [[Add motors and sensors]] | Up: [[Subsystem Stub]]
