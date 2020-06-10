# Servos

Servos are rotating motors that can rotate their output axle within a semicircular range. For more specific information, ask a member of the build team or visit [ServoCity's introduction to Servos](https://www.servocity.com/what-is-a-servo). A physical servo is represented by an instance of the [`Servo`](https://ftctechnh.github.io/ftc_app/doc/javadoc/com/qualcomm/robotcore/hardware/Servo.html) class in the FTC SDK.

{% embed url="https://first-tech-challenge.github.io/SkyStone/doc/javadoc/com/qualcomm/robotcore/hardware/Servo.html" %}

## Servo Position

Most standard servos are only capable of moving within a semicircular range, or from $$0^\circ$$ to $$180^\circ$$. The **position** of a servo is represented by a decimal in the FTC SDK, where $$0$$ represents $$0^\circ$$ and $$1$$ represents the largest angle possible, which is typically $$180^\circ$$. The scale is linear, so $$0.5$$ represents $$90^\circ$$, and so forth. Note that the club owns servos that can rotate $$360^\circ$$; for these servos, a position value of $$1$$ represents $$360^\circ$$ instead.

To have a servo move to a specific angle, call `Servo.setPosition` with the desired position value $$x$$, where $$0\leq x\leq 1$$. To retrieve the last value that was passed to `setPosition`, call `Servo.getPosition`. Note that this method does not reflect the servo's actual position at the instant of calling it. This means that the program cannot know for certain that the servo has reached the desired position value, so to compensate for the servo's rotation, we typically wait for a certain amount of time with `Thread.sleep` before moving onto another action.

## Servo Direction

Like the `DcMotor`, we can set the direction of a servo with `Servo.setDirection`. Typically, the effect of setting the direction to _Reverse_ is that any position value $$x$$ that is passed in causes the servo to move to the position $$1-x$$, meaning that the angle corresponding to a position value of $$0$$ in the _Forward_ direction corresponds to a position value of $$1$$ in the _Reverse_ direction.

## Servo Scale Range

There are many situations where a servo that is capable of rotating 180 degrees has a smaller range during operation. The FTC SDK includes a method named `Servo.scaleRange`, which allows you to restrict a servo's operating range to a subset of its capable range. Using `scaleRange` also means that any position value that is passed to `setPosition` is scaled within the given range. For example, if you call `servo.scaleRange(0.3, 0.6)`, subsequently calling `servo.setPosition(1)` will cause the servo to rotate to a position value of $$0.6$$, and calling `servo.setPosition(0)` will cause the servo to rotate to a position value of $$0.3$$.

## Examples

The following annotated examples demonstrate how to interact with the `Servo` interface according to the expected behaviors above. Feel free to refer to FTC's [official samples](https://github.com/FIRST-Tech-Challenge/SkyStone/tree/master/FtcRobotController/src/main/java/org/firstinspires/ftc/robotcontroller/external/samples) for more guidance.

```java
public class Demo {
  private Servo servo;

  // Setting servo position
  public void setPosition() throws InterruptedException {
    // Let the servo rotate to the angle corresponding to a position value of 0.6, or 108 degrees
    servo.setPosition(0.6);
    // Immediately, getPosition will return 0.6, regardless of whether the servo has actually reached that position
    assert servo.getPosition() == 0.6;

    // We can call Thread.sleep(...) to wait for the servo to reach the given position before moving on
    Thread.sleep(500);
  }

  // Setting servo direction
  public void setDirection() {
    // Reverse the servo's range such that a position value x in the forward direction now corresponds ot 1-x in the reverse
    servo.setDirection(Direction.REVERSE);
    // Let the servo rotate to a position value of 0.2 (or 36 degrees) in the reverse direction
    servo.setPosition(0.2);

    // Set the servo's direction to FORWARD again
    servo.setDirection(Direction.FORWARD);
    // Let the servo rotate to a position value of 0.8 (or 180-36 degrees) in the forward direction
    servo.setPosition(0.8);
    // In the real world, this should not cause the servo to rotate to another angle compared to the previous setPosition(0.2) call
  }

  // Using Servo.scaleRange
  public void scaleRange() {
    // Scale position values 0-1 to a subrange of the servo's capable range from 0.2 to 0.6
    servo.scaleRange(0.2, 0.6);
    
    // Let the servo rotate to a position value of 0, equivalent to 0.2 without the scaleRange call
    servo.setPosition(0);

    // Let the servo rotate to a position value of 0.8, equivalent to 0.52 without the scaleRange call
    servo.setPosition(0.8);
  }
}
```

## Check your Understanding

1. Why do we use servos?
2. What is the range of motion of a servo?
3. How many possible directions does a servo have?