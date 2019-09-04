# Accessing Gamepads

> **Relay driver inputs to robot hardware as quickly as possible**

To perform this TeleOp OpMode duty, your code needs to be able to read inputs from the driver's handheld controllers in real time. This is accomplished by accessing the fields of two instances of `Gamepad` in the `TeleOp` class: `gamepad1` and `gamepad2`. These fields correspond to the _User 1_ and _User 2_ registrations on the Driver Station; see FTC's [wiki page](https://github.com/FIRST-Tech-Challenge/SkyStone/wiki/Creating-and-Running-an-Op-Mode-%28Android-Studio%29#running-your-op-mode-with-a-gamepad-connected) on how these registrations work.

{% embed url="https://ftctechnh.github.io/ftc\_app/doc/javadoc/com/qualcomm/robotcore/hardware/Gamepad.html" caption="JavaDocs for the Gamepad class" %}

![Control columns of a F310 Gamepad \(from Modern Robotics\)](../.gitbook/assets/image%20%286%29.png)

Notice how each control column on a standard Gamepad is reflected with a field in `Gamepad`. The values for these fields are updated in real time as your OpMode executes, so accessing them at any time will yield the most up-to-date data from the controller itself. For example, the following expression is `true` whenever the "X" button of Gamepad 1 is pressed:

```java
gamepad1.x
```

## Relaying Inputs in an iterative OpMode

Recall that in an iterative OpMode, the `loop()` method is executed repeatedly when the OpMode is running. Given that the values in `gamepad1` and `gamepad2` are constantly updated, we can conveniently relay the state of input columns to output devices. Consider the following example of a simple tank-drive control scheme implementation:

{% code-tabs %}
{% code-tabs-item title="Tank Drive Implementation" %}
```java
public void loop() {
  leftMotor.setPower(-gamepad1.left_stick_y);
  rightMotor.setPower(-gamepad1.right_stick_y);
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

In this example, we simply pass the values of the fields of `gamepad1` to the two drivetrain motors repeatedly. Whenever a driver pushes the left stick forward, `leftMotor` receives a positive power value; whenever a driver pushes the right stick forward, `rightMotor` receives a positive power value.

{% hint style="warning" %}
Notice how the $$y$$ axes of the gamepad sticks are inverted: pushing the stick forward will cause the corresponding field to have a negative value. We typically need to negate the field in code whenever we wish to access these control axes.
{% endhint %}

## Examples from FTC and the Club

Examine the following examples from both _FIRST_ and the club's previous programs. Try to understand each control scheme and imagine explaining it to a potential driver—the control scheme of your robot is something **you** will need to negotiate!

* \_\_[_Basic Iterative OpMode example_](https://github.com/FIRST-Tech-Challenge/SkyStone/blob/master/FtcRobotController/src/main/java/org/firstinspires/ftc/robotcontroller/external/samples/BasicOpMode_Iterative.java#L113), from FIRST
* \_\_[_ARC Thunder's TeleOp for Rover Ruckus_](https://github.com/ARC-Thunder/Rover-Ruckus/blob/master/TeamCode/src/main/java/org/firstinspires/ftc/teamcode/MainTeleOp.java#L64)\_\_
* \_\_[_ARC Hailstorm's TeleOp for Relic Recovery_](https://github.com/AHSHailstorm/ARC-Hailstorm2017-2018/blob/master/TeamCode/src/main/java/org/firstinspires/ftc/teamcode/HailstormBasicTeleOp2017_2018.java#L50)\_\_
* \_\_[_ARC Thunder's TeleOp for Velocity Vortex_](https://github.com/Andover-Robotics/ARC-Thunder-2016-2017/blob/master/ThunderBasicTeleOp2016_2017.java#L75)\_\_

