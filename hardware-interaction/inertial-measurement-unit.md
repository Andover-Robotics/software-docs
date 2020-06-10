# Inertial Measurement Unit

The **Inertial Measurement Unit** of a REV Expansion Hub is an electronic device that measures the following physical attributes:

* Absolute Orientation
* Angular Velocity
* Linear Acceleration
* Magnetic Field Strength
* Gravity
* Temperature

{% hint style="warning" %}
Although the IMU is capable of measuring linear acceleration, it is not optimal for measuring displacement due to inaccuracies. Consider a scenario where a robot stays at rest. The measured linear acceleration is supposed to be 0, but it may fluctuate around 0 due to signal noise, causing minor changes in velocity that in turn causes the calculated displacement to deviate from the resting position at a steady rate. When the robot accelerates, inaccuracies like these add up over time, reducing the usefulness of the displacement measurements. **Do not rely on linear acceleration measurements from the IMU for displacement feedback.**
{% endhint %}

**The IMU is [useful](https://github.com/OpenFTC/OpenRC-Turbo/blob/324ed36fa4c1adb305c026f52b746acd4692e88a/Hardware/src/main/java/com/qualcomm/hardware/bosch/BNO055IMU.java#L71) for rotation feedback**, so you can use its angular orientation measurements to help your robot execute perfect turns during autonomous. You can also use the IMU to enable field-centric movement control during TeleOp, which may reduce driver cognitive workload for certain applications and improve scoring performance.

## Dimensions

The following video from FIRST demonstrates how each rotational axis (heading, roll, and pitch) corresponds to the physical dimensions of the REV Expansion Hub.

{% embed url="https://youtu.be/eN7fQnQ8zeg" %}

## Usage

### Initialization

The IMU behaves slightly differently compared to other sensors—you need to explicitly initialize it in addition to retrieving the object from `hardwareMap` before reading measurements. Check out this [function definition](https://github.com/Andover-Robotics/4410-Skystone/blob/master/TeamCode/src/main/java/org/firstinspires/ftc/teamcode/Bot.java#L101) from ARC Lightning 2019-2020, where we call `imu.initialize(parameters)` to prepare it for normal operation. For reference, here is a more comprehensive example of how to initialize your IMU. Ideally, you should do it when getting all hardware devices from `hardwareMap`.

```java
// Retrieve the IMU object from the hardware map
// Hint: you usually do not need to add this entry into your hardware configuration. It should already be there.
BNO055IMU imu = hardwareMap.get(BNO055IMU.class, "imu");
// `imu` is a variable in this example, but it is most likely a field in your code. Omit the type (`BNO055IMU`) in order to assign to the field.

// Make a new parameters object to store your preferences
BNO055IMU.Parameters params = new BNO055IMU.Parameters();

// Set the unit of all angles retrieved from the IMU.
// !: If you want to integrate with Road Runner, use RADIANS instead of DEGREES
params.angleUnit = BNO055IMU.AngleUnit.DEGREES;

// Initialize the IMU with your parameters
imu.initialize(params);
```

<!-- Author's note: Since the official JavaDocs indicated that manual calibration is not necessary for proper operation, I chose to omit it from this guide. The only perceivable benefit of manual calibration is a reduction in time spent initializing. Additionally, having to save a separate calibration file for each hub introduces excessive complexity. -->

### Reading Angles

Before beginning to read angles from the IMU, you need to determine the rotational axis to which the robot's heading corresponds. According to the video above, the robot's heading corresponds to the Z-axis if the hub is mounted with the words "EXPANSION HUB" facing up, and it corresponds to the X-axis if the hub is mounted with the words facing horizontally.

To read angular orientation measurements from the IMU, we use the `getAngularOrientation` method. It is possible to call this method with no parameters, but to make your code less ambiguous, we recommend supplying the three parameters.

1. The first parameter should be `AxesReference.INTRINSIC`, as found in the official usage example.
2. The second parameter depends on the rotational axis to be read. If you intend to read the Z-axis, use `AxesOrder.ZYX`. If you intend to read the X-axis, use `AxesOrder.XYZ`.
3. The third parameter depends on how you intend to use the retrieved values. If you will use trigonometric functions with them, it is a good idea to use `AngleUnit.RADIANS`. Otherwise, it might be more intuitive to use `AngleUnit.DEGREES`.

Once you have retrieved the angular orientation data in an `Orientation` object, you can access the heading of the robot with the `firstAngle` field. The range of values for this field is $$[-180, 180]$$ for degrees and $$[-\pi, \pi]$$ for radians. The initial orientation of the hub will take on a value of 0, and the positive direction corresponds to counter-clockwise rotation. Examine the video above for more intuition.

```java
// Obtain the orientation from the hub. The first angle shall be the X-axis reading. The unit of the first angle value should be degrees.
Orientation orient = imu.getOrientation(AxesReference.INTRINSIC, AxesOrder.XYZ, AngleUnit.DEGREES);

// `angle` is the heading of the robot in degrees
double angle = orient.firstAngle;
```

{% hint style="warning" %}
Since the angle output is constrained to $$[-180, 180]$$ or $$[-\pi, \pi]$$, the reading will wrap around the possible range when crossing an extremum. For example, if you were to keep track of the angle reading when the robot performs a full clockwise rotation, the reading would reach -180 degrees and immediately jump to 180 degrees. It is very possible that the robot might cross this heading when executing autonomous turns, so it is important to take the wraparound into consideration when programming.
{% endhint %}

{% hint style="info" %}
Q: Why do we have to use `firstAngle` to refer to the heading? If we need to access the Z-axis, couldn't we have `AxesOrder.XYZ` and use `thirdAngle`?

A: We have chosen `firstAngle` as our convention because of Road Runner. Road Runner Quickstart's FTC integration classes implement the `getExternalHeading` method by accessing the `firstAngle` of the input `Orientation`. It is a good idea to share the `BNO055IMU` instance used by Road Runner To minimize ambiguity and hide the implementation details of `Orientation`, you are free to wrap the access logic in your own class.
{% endhint %}

For a complete reference of the `BNO055IMU` class, check out the following source file from OpenFTC. Since the class is technically not part of the official `org.firstinspires` packages, you cannot find it in the official JavaDocs. Instead, you can read the inline JavaDoc source located in its extracted source file below:

{% embed url="https://github.com/OpenFTC/OpenRC-Turbo/blob/324ed36fa4c1adb305c026f52b746acd4692e88a/Hardware/src/main/java/com/qualcomm/hardware/bosch/BNO055IMU.java" %}

## Check Your Understanding

1. What IMU measurement is the most useful in FTC? How could you use this measurement to improve performance?
2. If you are currently working on a robot, which axis (X, Y, or Z) of the Expansion Hub corresponds to the robot's heading?
3. Given an initialized `BNO055IMU` instance assigned to a field named `imu`, retrieve the X-axis angular orientation reading in degrees and normalize it to the range $$[0, 360]$$.