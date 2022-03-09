# Accessing Gamepads

## Reading the Gamepad

To perform in TeleOp, your code needs to be able to read inputs from the driver's handheld controllers in real time. This is accomplished by accessing the fields of two instances of  the`Gamepad class` in the `TeleOp` class: `gamepad1` and `gamepad2`. Both of these fields will have been initialized by the FTC Robot Controller app while the program is initializing, so you do not have to worry about their initialization and may program under the assumption that they are non-null instances of the `Gamepad` class.&#x20;

How do you know which controller is `gamepad1` and which is `gamepad2`? These fields correspond to the _User 1_ and _User 2_ registrations on the Driver Station, which may be set up by the drivers on the FTC Driver Station app before the program is initialized; see FTC's [wiki page](https://github.com/FIRST-Tech-Challenge/SkyStone/wiki/Creating-and-Running-an-Op-Mode-\(Android-Studio\)#running-your-op-mode-with-a-gamepad-connected) on how these registrations work.

{% embed url="https://ftctechnh.github.io/ftc_app/doc/javadoc/com/qualcomm/robotcore/hardware/Gamepad.html" %}
JavaDocs for the Gamepad class
{% endembed %}

![Control columns of a F310 Gamepad (from Modern Robotics)](<../.gitbook/assets/image (17).png>)

Notice how each control column on a standard Gamepad is reflected with a field in `Gamepad`. The values for these fields are updated in real time as your OpMode executes, so accessing them at any time will yield the most up-to-date data from the controller itself. For example, the following expression is `true` whenever the "X" button of Gamepad 1 is pressed:

```java
gamepad1.x
```

Different inputs on controllers will correspond to different data types. Knowing which field of the `Gamepad` class will result in which data type is essential to a functioning TeleOp.

The controllers' buttons-X, A, B, Y, Back, and Stop-are **booleans**. Thus, `gamepad1.x`, `gamepad1.a`, `gamepad1.b`, `gamepad1.y`, `gamepad1.back`,  and`gamepad1.start`, respectively, will be `true` if the button is pressed and `false` otherwise.

The left and right bumpers, too, are **booleans**. Thus, `gamepad1.left_bumper` and `gamepad1.right_bumper`  will be `true` if the bumper is pressed and `false` otherwise.&#x20;

The x and y axes values of each joystick is a **double, ranging between -1 and 1.** The **center** of an axis is at the value **0**. The x and y values of the left and right sticks may be read from the following fields: `gamepad1.left_stick_x`, `gamepad1.left_stick_y`, `gamepad1.right_stick_x`, and`gamepad1.right_stick_y`. If the joysticks were in the positions shown in the image above, all four of these expressions would evaluate to 0.&#x20;

The values of the left and right triggers, too, are **doubles, ranging between 0 and 1.** `gamepad1.left_trigger` and `gamepad1.right_trigger` would give 0 if the triggers were unpressed, 1 if they were pressed fully to the ground, and a decimal value in between the two if the trigger were not fully pressed.

Finally, the D-pad buttons give **boolean** values. `gamepad1.dpad_up`, `gamepad1.dpad_right`, `gamepad1.dpad_down`, and `gamepad1.dpad_left` will each give true if the corresponding region of the dpad is pressed and false otherwise.

## Relaying Inputs in an iterative OpMode

Recall that in an iterative OpMode, the `loop()` method is executed repeatedly when the OpMode is running. Given that the values in `gamepad1` and `gamepad2` are constantly updated, we can conveniently relay the state of input columns to output devices. Consider the following example of a simple tank-drive control scheme implementation:

{% code title="Tank Drive Implementation" %}
```java
public void loop() {
  leftMotor.setPower(-gamepad1.left_stick_y);
  rightMotor.setPower(-gamepad1.right_stick_y);
}
```
{% endcode %}

In this example, we simply pass the values of the fields of `gamepad1` to the two drivetrain motors repeatedly. Whenever a driver pushes the left stick forward, `leftMotor` receives a positive power value; whenever a driver pushes the right stick forward, `rightMotor` receives a positive power value.

{% hint style="warning" %}
Notice how the $$y$$ axes of the gamepad sticks are inverted: pushing the stick forward will cause the corresponding field to have a negative value. We typically need to negate the field in code whenever we wish to access these control axes.
{% endhint %}

## Examples from FTC and the Club

Examine the following examples from both _FIRST_ and the club's previous programs. Try to understand each control scheme and imagine explaining it to a potential driver—the control scheme of your robot is something **you** will need to negotiate!

* __[_Basic Iterative OpMode example_](https://github.com/FIRST-Tech-Challenge/SkyStone/blob/master/FtcRobotController/src/main/java/org/firstinspires/ftc/robotcontroller/external/samples/BasicOpMode\_Iterative.java#L113), from FIRST
* __[_ARC Thunder's TeleOp for Rover Ruckus_](https://github.com/ARC-Thunder/Rover-Ruckus/blob/master/TeamCode/src/main/java/org/firstinspires/ftc/teamcode/MainTeleOp.java#L64)__
* __[_ARC Hailstorm's TeleOp for Relic Recovery_](https://github.com/AHSHailstorm/ARC-Hailstorm2017-2018/blob/master/TeamCode/src/main/java/org/firstinspires/ftc/teamcode/HailstormBasicTeleOp2017\_2018.java#L50)__
* __[_ARC Thunder's TeleOp for Velocity Vortex_](https://github.com/Andover-Robotics/ARC-Thunder-2016-2017/blob/master/ThunderBasicTeleOp2016\_2017.java#L75)__
