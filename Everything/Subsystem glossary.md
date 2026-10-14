*Part of [[Subsystem Stub]]*

---

A lookup page for every variable, method and weird word in the Collector and Indexer. Students `Ctrl/Cmd + F` for whatever confused them. Fill in the empty column. One or two sentences each, plain English, say *why* it exists, not just what it is.

All files are in `src/main/java/com/ck4911/` on the `autos` branch.

## Java and Dagger words

| Word | What it means |
|---|---|
| `import` / `import static` | |
| `private` / `public` | |
| `final` (variable) / `final class` | |
| `extends SubsystemBase` | |
| `implements CollectorIo` | |
| `interface` and `default` methods | |
| `@Override` | |
| `record` | |
| `@RecordBuilder` | |
| `() -> { ... }` (lambda) | |
| `this::intake` (method reference) | |
| `switch (mode) { case REAL -> ... }` | |
| `hashCode()` | |
| `@Inject` | |
| `@Singleton` | |
| `@Named("Bob")` | |
| `@Module` / `@Provides` | |
| `Provider<...>` | |
| `@Component` (`RobotComponent.java`) | |

## Units

| Thing | What it means |
|---|---|
| `Volts.of(...)`, `Amps.of(...)`, `Rotations.of(...)` | |
| `RotationsPerSecond` vs `RevolutionsPerSecond` (same thing) | |
| `.in(Radians)` | |
| `Angle`, `AngularVelocity`, `Voltage`, `Current`, `Temperature` | |
| Radians vs rotations | |

## Control words (link [[PID tuning]])

| Gain | What it does |
|---|---|
| P | |
| I | |
| D | |
| S | |
| G (and `Arm_Cosine`) | |
| V | |
| A | |
| Feedback vs feedforward | |
| Motion Magic (velocity, acceleration, jerk) | |
| `PidValues`, `FeedForwardValues`, `MotionMagicValues` (in `util/`) | |

## Library classes

### Commands (WPILib)
| Thing | What it does |
|---|---|
| `SubsystemBase` / `periodic()` | |
| `Command`, `Commands` | |
| `run`, `runOnce`, `startEnd` | |
| `Trigger` | |
| `DriverStation.isAutonomous()` | |
| `Timer` | |

### Logging and tuning (AdvantageKit + `util/`)
| Thing | What it does |
|---|---|
| `@AutoLog` / `...IoInputsAutoLogged` | |
| `Logger.processInputs(...)` | |
| `Logger.recordOutput(...)` | |
| `LoggedTunableNumber` / `tunableNumbers.create(...)` / `.get()` | |
| `LoggedTunableNumber.ifChanged(...)` | |
| Tuning mode (`@Named("TuningMode")` in `RobotModule.java`) | |
| `Alert` | |

### Hardware (CTRE Phoenix 6, link [[Add motors and sensors]])
| Thing | What it does |
|---|---|
| `TalonFX` | |
| `CANcoder` | |
| `CANBus` ("Bob" vs "rio") | |
| `TalonFXConfiguration` / `Slot0Configs` | |
| `getConfigurator().apply(...)` / `tryUntilOk` | |
| `StatusSignal` / `refreshAll` | |
| `setUpdateFrequencyForAll` / `optimizeBusUtilizationForAll` | |
| `setControl(...)` | |
| `VoltageOut`, `PositionDutyCycle`, `MotionMagicVelocityTorqueCurrentFOC` | |
| `Debouncer` | |

### SysId
| Thing | What it does |
|---|---|
| `SysIdRoutine` | |
| quasistatic vs dynamic | |
| `SignalLogger` | |

---

## Collector (`collector/Collector.java`)

Intro sentence to write: what the pivot and rollers are, what deploy / stow / agitate mean.

### Fields
| Variable | What it is |
|---|---|
| `collectorIo` | |
| `inputs` | |
| `constants` | |
| `pivotP` … `pivotA` | |
| `rollerP` … `rollerA` | |
| `stowPosition` / `deployPosition` | |
| `pivotVelocity`, `pivotAcceleration`, `pivotJerk` | |
| `rollerVelocity`, `rollerAcceleration`, `rollerJerk` | |
| `intakeSpeed` / `autoIntakeSpeed` | |
| `ballDetectedCurrent`, `debounceTime` | |
| `dumpVoltage` | |
| `stowTolerance` | |
| `pivotSysIdRoutine`, `rollerSysIdRoutine` | |

### Methods
| Method | What it does |
|---|---|
| `Collector(...)` (constructor) | |
| `periodic()` | |
| `updatePivotPid()` / `updatePivotFeedForward()` / `updatePivotMotionMagic()` | |
| `updateRollerPid()` / `updateRollerFeedForward()` / `updateRollerMotionMagic()` | |
| `setPivotAngle(angle)` | |
| `getPivotAngle()` | |
| `stow()` / `deploy()` | |
| `intake()` | |
| `isStowed()` | |
| `isStalled()` | |
| `collect()` | |
| `stopRollers()` | |
| `holdCurrentPosition()` | |
| `agitate(elapsed, delay, raise)` | |
| `intakeCommand()` | |
| `rollCommand()` | |
| `stopRollersCommand()` | |
| `deployNoRollersCommand()` | |
| `slowRaiseCommand(seconds)` | |
| `collectorDown()` / `collectorUp()` | |
| `stowCommand()` | |
| `agitateCommand()` | |
| `quickAgitateCommand(delay)` | |
| `stowWhenDone(command)` | |
| `oscillate()` | |
| `smartDumpCommand()` | |
| `runPivotSysId(trigger)` / `runRollerSysId(trigger)` | |

### `CollectorIoInputs` (in `CollectorIo.java`)
| Field | What it is |
|---|---|
| `pivotMotorConnected`, `rollerMotorConnected`, `pivotEncoderConnected` | |
| `pivotPositionRads` vs `pivotAbsolutePositionRads` | |
| `...VelocityRadsPerSec` | |
| `...AppliedVolts` | |
| `...SupplyCurrentAmps` vs `...TorqueCurrentAmps` | |
| `...TempCelsius` | |

### Constants (`CollectorConstants.java`, values in `CollectorModule.java`)
| Constant | Value | What it is |
|---|---|---|
| `pivotMotorId` / `rollerMotorId` / `pivotEncoderId` | 20 / 21 / 5 | |
| `pivotGearRatio` | 25 × 22 / 16 | |
| `minPivotPositionRads` / `maxPivotPositionRads` | -0.06 / 0.275 | |
| `pivotFeedBackValues` / `rollerFeedBackValues` | P = 1.5 / P = 16 | |
| `rollerFeedForwardValues` | S 0.397, V 0.127, A 0.0015 | |
| `intakeSpeed` / `autoIntakeSpeed` | 60 / 80 | |

---

## Indexer (`indexer/Indexer.java`)

Intro sentence to write: what the indexer and twindexer are, and why the twindexer speed changes with distance.

### Fields
| Variable | What it is |
|---|---|
| `inputs`, `indexerIo`, `constants` | |
| `indexerP` … `indexerA` | |
| `twindexerP` … `twindexerA` | |
| `indexSpeed` / `twindexSpeed` | |
| `indexerMotorDisconnected`, `twindexerMotorDisconnected` | |
| `indexerSysIdRoutine`, `twindexerSysIdRoutine` | |
| `twindexSpeedTable` | |
| `currentTargetTwindexSpeedRps` | |

### Methods
| Method | What it does |
|---|---|
| `Indexer(...)` (constructor) | |
| `periodic()` | |
| `setDynamicTwindexSpeed(distance)` | |
| `updateIndexerPid()` / `updateTwindexerPid()` / `updateIndexerFeedForward()` / `updateTwindexerFeedForward()` | |
| `runIndexer()` / `runIndexerInverted()` | |
| `runTwindexer()` / `runTwindexerInverted()` | |
| `stopIndexer()` / `stopTwindexer()` | |
| `feed(useDistance, distance)` | |
| `reverse()` | |
| `stop()` | |
| `indexcommand()` | |
| `indexAtDistanceCommand(distance)` | |
| `indexerCommandInverted()` / `twindexerCommandInverted()` | |
| `stopindexcommand()` | |
| `runIndexerSysId(trigger)` / `runTwindexerSysId(trigger)` | |

### `IndexerIoInputs` (in `IndexerIo.java`)
Same six values for `indexer...` and `twindexer...`: connected, velocity, applied volts, torque current, supply current, temp. Probably just link to the collector table.

### Constants (`IndexerConstants.java`, values in `IndexerModule.java`)
| Constant | Value | What it is |
|---|---|---|
| `indexerMotorId` / `twindexerMotorId` | 30 / 31 | |
| `indexSpeed` / `twindexSpeed` | 85 / 85 | |
| indexer gains | P 45, D 1, S 4.25, V 0.015 | |
| twindexer gains | P 20, S 3.125, V 0.0415 | |
| Motion Magic | velocity 100, acceleration 150 | |
| `providesTwindexerSpeedMap()` | 2 m→60, 3 m→60, 4 m→95, 5 m→95 | |

---

## Heads up: weird stuff in the code
> [!todo] Decide whether to explain these here or fix them in the code first
> Things students will trip over. All checked against `autos`:
> - Both `...IoSim` files are empty, so the collector and indexer do nothing in sim.
> - `minPivotPositionRads` / `maxPivotPositionRads` are used with `Rotations.of(...)`, so they're really rotations.
> - The comments in `CollectorConstants` say min = retracted, max = deployed, but the code uses max as stow and min as deploy.
> - `runPivotPosition` uses `PositionDutyCycle` and ignores its `feedforward` parameter, so the pivot Motion Magic tunables don't do anything.
> - `CollectorIoReal` sets `rollerPosition = pivotMotor.getPosition()` (reads the wrong motor).
> - `new Debouncer(0.5)` defaults to delaying the rising edge, so "disconnected" shows instantly and "connected" waits 0.5 s. AdvantageKit's examples use `DebounceType.kFalling`.
> - Not used anywhere yet: `ballDetectedCurrent`, `debounceTime`, `rollerCurrentLimitAmps`, `pivotEncoderOffsetRads`, `debounceTimeSeconds`, `absolutePivotPositionRads`, `runPivotCurrent` / `runRollersPercent` / `runRollersCurrent` / `setBrakeMode`, `setIndexerProfile` / `setTwindexerProfile`, `smartDumpCommand`, all SysId commands.
> - `indexcommand()` / `stopindexcommand()` are lowercase, everything else is camelCase.
> - The twindexer's Motion Magic jerk reads the indexer's value (harmless, both are 0).

---
← Previous: [[Write a basic command]] | Up: [[Subsystem Stub]]
