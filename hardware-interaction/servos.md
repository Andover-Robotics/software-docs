Servos are rotating motors that can turn parts within a semicircular range. For more specific information, ask a member of the build team or visit [ServoCity's introduction to Servos](https://www.servocity.com/what-is-a-servo). A physical servo is represented by an instance of the [`Servo`](https://ftctechnh.github.io/ftc_app/doc/javadoc/com/qualcomm/robotcore/hardware/Servo.html) class in the FTC SDK.

# Servo Position

Most standard servos are only capable of moving within a semicircular range, or from $0^\circ$ to $180^\circ$. The **position** of a servo is represented by a decimal in the FTC SDK, where $0$ represents $0^\circ$ and $1$ represents the largest angle possible, which is typically $180^\circ$. The scale is linear, so $0.5$ represents $90^\circ$, and so forth. Note that the club owns servos that can rotate $360^\circ$; for these servos, a position value of $1$ represents $360^\circ$ instead.

To have a servo move to a specific angle, call `Servo.setPosition` with the desired position value $x$, where $0\leq x\leq 1$. To retrieve the last value that was passed to `setPosition`, call `Servo.getPosition`. Note that this method does not reflect the servo's actual position at the instant of calling it. This means that the program cannot know for certain that the servo has reached the desired position value, so to compensate for the servo's rotation, we typically wait for a certain amount of time with `Thread.sleep` before moving onto another action.

# Servo Direction

Like the `DcMotor`, we can set the direction of a servo with `Servo.setDirection`. Typically, the effect of setting the direction to _Reverse_ is that any position value $x$ that is passed in causes the servo to move to the position $1-x$, meaning that the angle corresponding to a position value of $0$ in the _Forward_ direction corresponds to a position value of $1$ in the _Reverse_ direction.

# Servo Scale Range

There are many situations where a servo that is capable of rotating 180 degrees has a smaller range during operation. The FTC SDK includes a method named `Servo.scaleRange`, which allows you to restrict a servo's operating range to a subset of its capable range. Using `scaleRange` also means that any position value that is passed to `setPosition` is scaled within the given range. For example, if you call `servo.scaleRange(0.3, 0.6)`, subsequently calling `servo.setPosition(1)` will cause the servo to rotate to a position value of $0.6$, and calling `servo.setPosition(0)` will cause the servo to rotate to a position value of $0.3$.
