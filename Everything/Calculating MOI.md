# Calculating MOI

Calculating MOI is quite complex, but don't get overwhelmed. I will probably make a video on how to do it, as it's a good introduction to system identification and similar topics to PID tuning (you will need to know how to do PID tuning).

A few good resources that I strongly recommend you read up on are from the WPILib docs (a very helpful resource — when you have a question, you can probably find the answer somewhere in there):
- https://docs.wpilib.org/en/stable/docs/software/advanced-controls/system-identification/introduction.html
- https://docs.wpilib.org/en/stable/docs/software/advanced-controls/introduction/introduction-to-feedforward.html#the-permanent-magnet-dc-motor-feedforward-equation

Both of these are short reads and will help you a lot through this document.

## The equation we will be using
$$I = \text{mass} * \frac{\text{trackwidth}}{2} * \frac{kA_\text{angular}}{kA_\text{linear}}$$

Let's break down each part of this equation:
- **Mass:** The weight of the robot.
- **Trackwidth:** The distance from the center of the left wheel to the right one. Always use CAD for this, as measuring will be less accurate.
- **kA angular:** How many volts are required to feed the motor to make the robot's spin _accelerate_ at a certain rate — basically volts per unit of angular acceleration. The harder you want the spin to speed up, the more volts this term adds. It will look something like this for the final answer: V/(rad/s²).
- **kA linear:** The same as kA angular, just for driving forward in a straight line instead of spinning. It's how many volts are required to make the robot _accelerate_ (speed up) at a certain rate when driving straight. It will look something like this for the final answer: V/(m/s²).

Getting mass and trackwidth is pretty simple, it's the kA angular and linear that are a tad more difficult to get.

> [!todo] Finish this when you have the actual robot

---
Up: [[Configuring the robot physics]]
