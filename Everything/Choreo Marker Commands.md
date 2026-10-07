
Choreo marker commands are the commands that run when they are activated through Choreo markers. Just a heads up, I recommend that you go through the training resources on the basics of Java here: Java Learning Resources before reading this as we talk about classes, objects and methods.

This will also be digging down into the code and showing the structure of how all of these commands work.

## Code break down

**What a bind does:**

```java
autoFactory.bind("EventName", aCommand);

// Our example:
autoFactory.bind("Intake", collector.intakeCommand());
```

This maps a string to a command. In the case of intake it maps `"Intake"` to the command:

```java
collector.intakeCommand()
```

Then inside of the Collector class we use a method with the return type command that in turn calls more void methods:

```java
public Command intakeCommand() {
  return run(
    () -> {
      deploy();
      intake();
    });
}
```

Here `run` is an inherited factory method that builds a `Command` from a lambda, and the `() -> {}` is the lambda holding the code to execute repeatedly.

### The Deploy method

```java
private void deploy() {
  setPivotAngle(Rotations.of(deployPosition.get()));
}
```

This method is a private method with the void return type (it means that nothing will be returned when the method is used). This uses the `setPivotAngle` method and its argument is `Rotations.of`, which is another method and the argument of that is the method `deployPosition.get`. Let's break down each of those methods.

So let's say that we run the method `deployPosition.get()`. `deployPosition` is an object, and calling `.get()` on it returns its current value. That is now the argument of `Rotations.of()`, so it looks something like `Rotations.of(.8)`, and Rotations is imported from WPILib to allow for smoother handling of the measurement of an angle.

### setPivotAngle

```java
private void setPivotAngle(Angle angle) {
  collectorIo.runPivotPosition(angle, Amps.of(0));
}
```

This is another private method with a void return type. What looks like an argument here is actually a parameter. A parameter is the variable in the method definition (`Angle angle`); an argument is the actual value passed in when the method is called (`Rotations.of(...)`). The parameter is a local variable scoped to this method, and when the method is used, like in our deploy method, it will then set the angle to be equal to whatever these methods return: `Rotations.of(deployPosition.get())`. Then it uses a method on the collectorIo object, which is an instance of a class that implements the CollectorIo interface (either CollectorIoReal or CollectorIoSim). The argument for the runPivotPosition that is being used is angle (the value that was passed into setPivotAngle). and the method call, Amps.of(0) has the amps be 0.

### default void runPivotPosition

```java
public default void runPivotPosition(Angle angle, Current feedforward) {}
```

Its body is empty (`{}`) because it is a `default` interface method meant to be overridden by a hardware IO implementation. In simpler terms that means that inside of our collectorioreal.java file, this same method name will be there *but* it will A) have a body B) at the top have an @Override, which tells the compiler this method is intentionally replacing the interface's version. Now you may be wondering, why do we have this extra method thats never really used? Another great question, and if we take a quick look over at all of our java files we will se a collectorioreal.java and a collectoriosim.java. The real file is for when we actually run it on the real robot, and the simulator is for when we run the code in the sim, which we will cover later. But now the last question you may have, how do we decide which method is actually used? We have the real runPivotPosition and the sim runPivotPosition, and that is the best question you have had so far. If we go to CollectorModule.java and look at line 44 you will see:

```java
public static CollectorIo providesCollectorIo(
Mode mode, Provider<CollectorIoReal> realProvider, Provider<CollectorIoSim> simProvider) {
return switch (mode) {
case REAL -> realProvider.get();
case SIM -> simProvider.get();
case REPLAY -> new CollectorIo() {};
default -> throw new IllegalArgumentException("Unexpected value: " + mode);
};
}
```
This basically is checking wether we are in the REAL or SIM mode, don't worry about REPLAY mode, we rarely use it. Based on what case it returns, it determines what instance the object will be of which class, deciding which method gets used in all of the code we just went through.

### Override runPivotPosition
```java
@Override
public void runPivotPosition(Angle angle, Current feedforward) {
pivotMotor.setControl(pivotRequest.withPosition(angle));
}
```
This is the method that actually moves the pivot motor. Its parameters, angle and feedforward, receive the arguments that setPivotAngle passed in: angle and Amps.of(0). angle is still the same value all the way back from the deploy method and then feedforward is the parameter that was the argument for runPivotPosition. The current/amps/feedforward is how much extra power we give the motor when putting the pivot forward, which in this case we do not need any extra power. 

**Breaking down the body**
`pivotMotor.setControl(...)` is a method call. pivotMotor is an instance from TalonFX. setControl is a method also from CTRE (which is a parent of Phoenix/Talon) setControl is a way of sending a control request to a motor controller. In this case the argument of setControl is another method call `pivotRequest.withPosition(angle)`. pivotRequest is a field that holds the PositionDutyCycle object. "withPosition is a method of the PositionDutyCycle class, which (like TalonFX) comes from the CTRE Phoenix 6 library. It tells the motor what position it should go to, in this case angle. 

### The Full Path
TODO: insert the full path