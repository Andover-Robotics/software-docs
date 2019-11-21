---
description: 'Troubleshooting is inevitable, so here are some tools.'
---

# Telemetry and Debugging

## Telemetry

In FTC, there are many situations in which you need to [confirm the value of a variable](https://github.com/ARC-Thunder/ftc_app/blob/fb933aa2e67ef65de2014ab9ac86163ee5bc9b01/TeamCode/src/main/java/org/firstinspires/ftc/teamcode/ThunderNavigation.java#L88), confirm the execution of a conditional branch, or simply inform the drive team about the state of the robot's program. The FTC control system has built-in support for **telemetry**, which effectively delivers any arbitrary message from the Robot Controller code to the Driver Station's screen. It is practically analogous to the print statement in a traditional computer program.

The `OpMode` class contains a [public field](http://ftctechnh.github.io/ftc_app/doc/javadoc/com/qualcomm/robotcore/eventloop/opmode/OpMode.html#telemetry) named `telemetry`, which is where all telemetry actions are performed. Feel free to refer to the JavaDoc documentation for the `Telemetry` interface for more details.

{% embed url="https://first-tech-challenge.github.io/SkyStone/doc/javadoc/org/firstinspires/ftc/robotcore/external/Telemetry.html" caption="Official JavaDocs for Telemetry" %}

Telemetry works slightly differently compared to straightforward print statements. In telemetry, we build the driver station display line-by-line and then perform a bulk transmission to the Driver Station for this display to be shown. This mechanism takes into account the limited communication bandwidth between the Driver Station and the Robot Controller; to minimize disruption to the control system's other duties, there is a minimum time interval of 250 milliseconds between each bulk transmission of telemetry data. This is why the telemetry data shown on the Driver Station screen does not update very quickly. This mechanism will also affect how we write code for telemetry.

### Writing Simple Data

In its simplest form, composing telemetry messages involves adding lines to the display by making calls to `Telemetry.addData` and then sending the display to the Driver Station by calling `Telemetry.update`. The following demonstrates this technique using [some autonomous code from Relic Recovery](https://github.com/ARC-Thunder/ftc_app/blob/fb933aa2e67ef65de2014ab9ac86163ee5bc9b01/TeamCode/src/main/java/org/firstinspires/ftc/teamcode/AutonomousMethodMaster.java#L433-L438) by 5273.

{% code title="AutonomousMethodMaster.java" %}
```java
// Adds telemetry of the drive motors
telemetry.addData("motorFL Pos", LPos);
telemetry.addData("motorFR Pos", RPos);

// Updates the telemetry
telemetry.update();
```
{% endcode %}

If `LPos` and `RPos` are both zero, executing this will cause the Driver Station to display the following information: 

**motorFL Pos : 0  
motorFR Pos : 0**

By default, calling `telemetry.update()` will automatically clear the currently added data after it has been sent. Therefore, if you call `telemetry.update()` twice in a row, the Driver Station will probably not show any data. You can override this behavior by using [`Telemetry.setAutoClear`](http://ftctechnh.github.io/ftc_app/doc/javadoc/org/firstinspires/ftc/robotcore/external/Telemetry.html#setAutoClear-boolean-).

Moreover, whereas calling `telemetry.update()` is necessary in a LinearOpMode, it is not necessary in an iterative OpMode. `telemetry.update()` is automatically called after each iteration of the `loop()` method.

If you would like to send formatted data using the [`String.format` technique](https://docs.oracle.com/javase/8/docs/api/java/lang/String.html#format-java.lang.String-java.lang.Object...-), `addData` can optionally accept more arguments and pass them to `String.format` with the second argument being the format string. For instance, if `x` is equal to 3.141, calling `telemetry.addData("Info", "Value of x is %.2f", x)` would result in "**Info : Value of x is 3.14"** on the Driver Station screen.

Simply using `addData` in this manner is sufficient for most situations, but there are other options that may be more suitable for certain use cases.

### Multiple Items per Line

If you would like multiple items to be shown in one line on the Driver Station, you can use the technique demonstrated below:

{% code title="From Telemetry JavaDoc" %}
```java
telemetry.addLine()
     .addData("count", currentCount)
     .addData("elapsedTime", "%.3f", seconds);
telemetry.addLine()
     .addData("voltage", "%.1f", getCurrentVoltage())
     .addData("orientation", "%s", getOrientation());
telemetry.update();
```
{% endcode %}

### Managing Existing Items

The `Telemetry.addData` method returns an object of the type [`Telemetry.Item`](http://ftctechnh.github.io/ftc_app/doc/javadoc/org/firstinspires/ftc/robotcore/external/Telemetry.Item.html), which represents a single item on the Driver Station display. If you store the return value of `addData` somewhere, you can reuse it later to make edits to the data, add more items to the display, or remove it from the display using the [`Telemetry.removeItem`](http://ftctechnh.github.io/ftc_app/doc/javadoc/org/firstinspires/ftc/robotcore/external/Telemetry.html#removeItem-org.firstinspires.ftc.robotcore.external.Telemetry.Item-) function.

### Logging

The [`Telemetry.log()`](http://ftctechnh.github.io/ftc_app/doc/javadoc/org/firstinspires/ftc/robotcore/external/Telemetry.html#log--) method returns an instance of [`Telemetry.Log`](http://ftctechnh.github.io/ftc_app/doc/javadoc/org/firstinspires/ftc/robotcore/external/Telemetry.Log.html), an interface that supports message-based logging. Log messages are displayed under all other types of data on the Driver Station.

## Debugging

Sometimes the Robot Controller app crashes without any useful information shown on the screen. Sometimes your code behaves erratically, and you would like to confirm a theory of a possible error using the value of a variable. In both situations, the most effective way to troubleshoot is to **debug** the program's execution. Since the Robot Controller app is debuggable, you can use the **Debug button** \(pictured below\) during upload to tell Android Studio to attach its debugger to the app.

![Debugging Button \(from Android Developers\)](../.gitbook/assets/image%20%2816%29.png)

The debugger in Android Studio supports the following features:

* View system logs with Logcat
* View the cause and the stack trace of a fatal exception
* Step through code, set breakpoints, and view the values of variables
* Evaluate code expressions at runtime

For a more comprehensive reference, visit [Android's debugging documentation](https://developer.android.com/studio/debug) and [IntelliJ IDEA's debugging documentation](https://www.jetbrains.com/help/idea/debugging-code.html). Remember that Android Studio is based on IntelliJ IDEA.





