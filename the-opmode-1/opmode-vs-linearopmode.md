---
description: The OpMode that is not linear is iterative.
---

# OpMode vs LinearOpMode

As you have discovered in the previous section, you have a choice between extending from `OpMode` and extending from `LinearOpMode` in each new OpMode that you intend to create. These options represent two different paradigms of execution flow. Whereas `OpMode` is inherently iterative, `LinearOpMode` is inherently sequential. There is no distinct advantage in either option over the other—the choice depends on how you wish to model your program.

{% hint style="info" %}
It is a wildly popular belief that `OpMode` corresponds with TeleOp and `LinearOpMode` corresponds with Autonomous. While this is the most popular method of association, it is by no means enforced. Some of the best teams in the world break this association by having their autonomous OpMode be [nonlinear](https://bitbucket.org/PeterTheEarthling/version-4.3/src/master/ftc_app-master/TeamCode/src/main/java/HelperClasses/Auto.java).
{% endhint %}

## The LinearOpMode

When you first learned to code, you were probably told that a program is like a to-do list for the computer to follow step-by-step. Indeed, the `public static void main` method is executed in this manner. The `LinearOpMode` follows this pattern—much like the `main` method, the `runOpMode` method is called whenever the current OpMode is initialized from the Driver Station by pressing the _INIT_ button. Therefore, you can treat `runOpMode` as the entry point of your program. The typical structure for the body of `runOpMode` is as follows:

1. **Initialize** all references to hardware
2. **Wait for the Play \(▶\) button to be pressed on the Driver Station** by calling `waitForStart()`
3. **Run** the operations of the current OpMode

The club has [plenty](https://github.com/ARC-Thunder/Rover-Ruckus/blob/81609d6b0197b887c1569a39b6fbbfb1eea1bf55/TeamCode/src/main/java/com/andoverrobotics/core/examples/TankDriveAutonomousExample.java#L15) [of](https://github.com/ARC-Thunder/teamcode/blob/3829a4eb1866220c5239d494ea30e5067c8a73ee/VuforiaAutonomous.java#L60) [examples](https://github.com/ARC-Lightning/Rover_Ruckus-2018-2019/blob/master/TeamCode/src/main/java/org/firstinspires/ftc/teamcode/autonomous/AutoOpMode.java#L38) from historic code that use this `LinearOpMode` paradigm.

{% hint style="info" %}
We can theoretically stop any OpMode at any time by pressing the Stop \(◼\) button, but how is it able to stop a blocking operation in a `LinearOpMode`immediately? If your code only waits for a motor to reach a specific position, it would not care whether the OpMode has stopped, and the Robot Controller app would have to forcefully abort your OpMode, causing an Emergency Stop and requiring the robot to be restarted. This issue is addressed in [Stopping LinearOpModes](stopping-linearopmodes.md).
{% endhint %}

## The \(Iterative\) OpMode

Unlike the `LinearOpMode`, the \(iterative\) `OpMode` executes a specific method named `loop` repeatedly when the OpMode is running. When declaring an `OpMode`, you may override the following methods, shown in the order of execution in a typical OpMode lifecycle:

| Function Signature | When It's Executed | Required? |
| :--- | :--- | :--- |
| `public abstract void init()` | Executed **once** immediately after a user presses _INIT_ on the Driver Station | Yes |
| `public void init_loop()` | Executed **repeatedly** after a user presses _INIT_ but before a user presses Play \(▶\) on the Driver Station | No |
| `public void start()` | Executed **once** immediately after a user presses Play \(▶\) on the Driver Station | No |
| `public abstract void loop()` | Executed **repeatedly** after a user presses Play \(▶\) but before a user presses Stop \(◼\) on the Driver Station | Yes |
| `public void stop()` | Executed **once** immediately after a user presses Stop \(◼\) on the Driver Station | No |

If it makes more sense to you, you can imagine an `OpMode` as a `LinearOpMode` with the following definition of `runOpMode()`:

{% code-tabs %}
{% code-tabs-item title="Executing an iterative OpMode" %}
```java
public void runOpMode() {
  init();
  
  while (!isStarted())
    init_loop();
    
  start();
  
  while (!isStopRequested())
    loop();
    
  stop();
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

For conventional TeleOp, we initialize our references to hardware devices in the `init()` method, and we send the received gamepad values to the output devices in the `loop()` method. FIRST's [example](https://github.com/FIRST-Tech-Challenge/SkyStone/blob/master/FtcRobotController/src/main/java/org/firstinspires/ftc/robotcontroller/external/samples/BasicOpMode_Iterative.java) is an excellent reference for this paradigm.

