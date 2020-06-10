---
description: 'Pick a program, any program...'
---

# Introducing the OpMode

OpModes are essential to programming in FTC. It is the entry point of your programs—think `public static void main`. It is where your programs access all external resources, like robot hardware and telemetry. Short for “Operation Mode”, the OpMode is the true foundation upon which you program a FTC robot.

## Introduction

A TV can have multiple channels. A smartphone can have multiple apps. A computer can have multiple programs. A codebase for FTC can have multiple OpModes. An OpMode is a particular procedure that is executed by a FTC Robot Controller phone. You might create OpModes to test electronics, run autonomously for the Autonomous Period, run using remote control for the TeleOp Period, or to experiment with unfamiliar software.

{% hint style="info" %}
FIRST provides numerous example OpModes in the FtcRobotController app. They are accessible through both Android Studio and the [Skystone GitHub repository](https://github.com/FIRST-Tech-Challenge/SkyStone/tree/master/FtcRobotController/src/main/java/org/firstinspires/ftc/robotcontroller/external/samples). Their content covers numerous topics of FTC programming, including how to use motors, many types of sensors, telemetry, and image recognition. Throughout your experience as a programmer for ARC, these examples are excellent references for how certain tasks are done. They also serve as a reminder of the format that OpModes should follow.
{% endhint %}

## OpMode Lifecycle

### Normal Flow

Each OpMode you create can be found as a menu option on the Driver Station app. Above the circular button, two dropdown options are available on both sides of the OpMode selection menu, denoting TeleOp and Autonomous respectively. Each dropdown menu contains the names of all the declared OpModes in its category. Once you select the desired OpMode and press _INIT_, an object belonging to its class is instantiated, and either `runOpMode` or `init` is executed.

When setting up the robot on the field, one member of the drive team selects the desired Autonomous OpMode and presses _INIT_. **We recommend that your Autonomous OpModes use** [**telemetry**](telemetry-and-debugging.md) **to inform the drive team when it is fully initialized and whether any errors have occurred**; the drive team may not touch the Driver Station screen nor enter the field after signalling to the referee that it is ready. Before autonomous begins, the OpMode will stay initialized. Once autonomous begins, the drive coach presses Play \(▶\), and the OpMode continues to execute. If the current OpMode belongs to the Autonomous category, an automatic 30-second timer can stop the OpMode once the Autonomous period ends; this timer is shown to the right of the circular button.

Between Autonomous and TeleOp, the drive coach switches from the Autonomous OpMode to the TeleOp OpMode and initializes it while the drivers pick up their controllers. When the TeleOp countdown ends, the drive coach presses Play \(▶\), and the OpMode continues to execute.

Once the TeleOp period ends, the drive coach presses Stop \(◼\), and the OpMode is asked to stop. The low-level mechanism for this differs by whether the OpMode is linear; refer to [OpMode vs LinearOpMode](opmode-vs-linearopmode.md) for more details.

{% hint style="info" %}
Teams have done clever things with the time period after initialization but before Autonomous begins. For example, during Rover Ruckus World Championships, ARC Thunder implemented a mechanism that sends the perceived type of the middle sampling mineral to the drive team using telemetry. This allowed the drive team to eliminate potential forms of visual interference for the vision system before indicating readiness to compete.

Note, however, that since you are not allowed to touch the Driver Station's screen after indicating that you are ready and before the Autonomous period begins, you should make your telemetry messages succinct enough that viewers do not need to scroll.
{% endhint %}

### Exceptions to the Flow

If your OpMode happens to throw an uncaught exception, one of the following may occur:

* _Emergency Stop_: The OpMode will abort, and a brief summary of the uncaught exception will be shown in telemetry. To resume operation, you are required to restart the robot through the Driver Station. Doing so is illegal during Autonomous but legal during TeleOp.
* _Crashing app_: The Robot Controller app will crash, and Android will show the message _"Unfortunately, FTC Robot Controller has stopped."_ There is no known way to recover from this during competition.

By the nature of the FTC Control System, the Robot Controller and the Driver Station may occasionally and spontaneously disconnect. When this happens, the OpMode will attempt to stop, and the Robot Controller app will attempt to regain communication with the Driver Station. When \(and if\) this connection is restored, the drive team may restart the OpMode from the Driver Station.

{% hint style="info" %}
FTC has become notorious for its disconnection problems. During [Relic Recovery World Championship DaVinci F-2](https://youtu.be/5WCCiSv4uSE), for example, 9971 LANBros disconnected during the match and caused its alliance to lose Worlds. More recently, during [Rover Ruckus Maryland Tech Invitational \(MTI\) SF2-3](https://youtu.be/xjClFpUv4UM), 14270 Quantum Robotics disconnected during the match and caused its alliance to be eliminated. So don't be so frustrated when you experience a disconnect from time to time—it happens to the best teams out there as well.
{% endhint %}

## OpMode Definition

Refer to the [official examples](https://github.com/FIRST-Tech-Challenge/SkyStone/blob/master/FtcRobotController/src/main/java/org/firstinspires/ftc/robotcontroller/external/samples/BasicOpMode_Iterative.java) for a demonstration. To define an OpMode in Java, simply follow the following steps:

1. Make a new class for the OpMode, and let the class extend either `OpMode` or `LinearOpMode`. _\(See_ [_OpMode vs LinearOpMode_](opmode-vs-linearopmode.md) _for an explanation of these options\)_ 
2. Annotate the class with either `@Autonomous` or `@TeleOp`. This will determine where your new OpMode will be found on the Driver Station interface. Select the option that is appropriate for your OpMode’s intended model of operation. 
3. Give the annotation parameters `name` and `group`. The `name` should uniquely identify the OpMode in a list of OpMode names. The value of the `group` parameter allows you to further organize OpModes; in the Driver Station interface, OpModes are first divided into two lists, one for OpModes marked with `@Autonomous` and one for those marked with `@TeleOp`. Then, each of these lists are also sorted alphabetically by `group`, and the OpModes within each `group` are sorted alphabetically by `name`. Thus, there are many options when it comes to organizing your OpModes. Always use a distinctive and descriptive `name` such that all of your team's drivers can easily distinguish the proper OpMode to run at any time without the assistance of programmers. By ARC convention, the value of `group` should be one of the following: 
   1. **“Competition”:** to denote that the current OpMode should be used during an actual competition
   2. **“Experimental”:** to denote that the current OpMode is used to experiment with untested or otherwise unfamiliar code
   3. **“Troubleshoot”:** to denote that the current OpMode is used to verify the operation of particular features, such as hardware devices.
   4. **"Other":** for OpModes whose purpose is not covered by any of the options above. 
4. Declare the required abstract methods. For a `LinearOpMode`, the required method is `public void runOpMode()`; for an iterative `OpMode`, the required methods are `public void init()` and `public void loop()`. See [OpMode vs LinearOpMode](opmode-vs-linearopmode.md) for an explanation of these methods. 
5. Fill the method bodies with desired logic.

For a `LinearOpMode`, the empty definition should look like this:

{% code title="MyOpMode.java" %}
```java
@Autonomous(name="Demo Auto", group="Experimental")
// Or @TeleOp
public class MyOpMode extends LinearOpMode {
    @Override
    public void runOpMode() {
        // Your code here
    }
}
```
{% endcode %}

For an `OpMode`, the empty definition should look like this:

{% code title="MyOpMode.java" %}
```java
@Autonomous(name="Demo Auto", group="Experimental")
// Or @TeleOp
public class MyOpMode extends OpMode {
    @Override
    public void init() {
        // Code to initialize
    }

    @Override
    public void loop() {
        // Code to iterate
    }
}
```
{% endcode %}

{% hint style="warning" %}
We encourage you not to copy & paste from this guide. Typing the code out helps you memorize this structure and eliminate any dependence on this guide when creating new OpModes. Many competition venues do not allow access to the Internet in the pits, which means that you cannot always rely on this guide.
{% endhint %}

In the [next section](opmode-vs-linearopmode.md), you will discover the differences between these two paradigms of programming OpModes.

## Check your Understanding

1. What is an OpMode?
2. Where can you select which OpMode to run?
3. True or False: You do not need to create a new class in order to make a new OpMode.

