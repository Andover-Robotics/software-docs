---
summary: >-
  Something to remember in every loop condition, or else your OpMode crashes at
  the end of Autonomous.
---

# Stopping LinearOpModes

> _You must always be able to stop Autonomous from running. This is a safety issue, if your robot starts to damage the field, another robot, or a person in the pits. It’s also one of the things that is tested during Field Inspections. -Philbot, FTC Forums_

As a programmer, it is your responsibility to ensure that the robot is always under control. This is not just a matter of rules—it’s a matter of ethics. The 737 MAX incidents demonstrate how badly things can go when this basic principle is violated. The club has had a rich history of neglecting the following procedures, leading to penalties on the field and broken robot parts. To prevent this from happening to your robot, read on.

## Interrupting a LinearOpMode

{% embed url="https://docs.oracle.com/javase/tutorial/essential/concurrency/interrupt.html" %}

A `LinearOpMode` executes like any other computer program—the statements in `runOpMode` are executed one after another, like in `public static void main`. When the Stop (◼) button is pressed, the Robot Controller SDK sends an interrupt to the thread that runs `runOpMode`, signaling it to stop. If the thread is running a while loop whose condition does not check if the OpMode is stopped, it can take a long time for the thread to respond to the interrupt and stop itself. The Robot Controller SDK has a mechanism for this—if the thread does not stop within a few seconds, the app forcefully aborts the thread and issues an “Emergency Stop” with the message `LinearOpMode stuck in stop()`, requiring you to restart the robot before starting another OpMode.

## The Solution

One of the functions made available in `LinearOpMode` is [`isStopRequested`](http://ftctechnh.github.io/ftc_app/doc/javadoc/com/qualcomm/robotcore/eventloop/opmode/LinearOpMode.html#isStopRequested--), which returns true whenever the OpMode is requested to stop (either by a timer or by pressing the Stop button). This means that you can check it in every loop condition that the OpMode might execute in the course of its lifetime. This ensures that whenever the OpMode is asked to stop, your code can quickly escape the current state and finish its execution. Consider the following example:

```java
// Unresponsive when aborted!
public void runOpMode() {
  liftMotor.setMode(RunMode.RUN_TO_POSITION);
  liftMotor.setTargetPosition(5100);
  liftMotor.setPower(0.6);
  while (liftMotor.isBusy()) {
    telemetry.addData("liftMotor position", liftMotor.getCurrentPosition());
    telemetry.update();
  }
}
```

On Line 5, the `while` loop's condition does not include whether the OpMode has stopped. As a result, when this program is stopped prematurely (perhaps to prevent damage to the lift), it will not respond, and an Emergency Stop will be issued.

To fix this program, change the fifth line to `while (liftMotor.isBusy() && !isStopRequested())`. This additional check ensures that when the OpMode is requested to stop, the flow of execution will immediately exit the loop and return from the method.

