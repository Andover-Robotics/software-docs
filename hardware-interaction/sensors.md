# Sensors

A **sensor** is an electronic device that takes input from the outside environment, whether that's color, temperature, or some other factor, and collects the information so we can use it to make decisions in our program.

## The Color Sensor

One common sensor is a color sensor. Color sensors can be useful in a variety of challenges where the robot needs to differentiate differently colored objects.

Here are some important tips you'll need to know in order to use a color sensor:

### Initializing the Sensor

Just like any other piece of hardware, you need to initialize a Color Sensor before you can use it.

In your class, you can initialize a variable of type `ColorSensor`:

```java
ColorSensor color_sensor;
```

When initializing your hardware devices, you'll need to interface with the hardware map to actually connect it.

```java
color_sensor = hardwareMap.get(ColorSensor.class, "color_sensor");
```

Now that you have your sensor initialized, you are ready to begin retrieving color values from it.

### `.red()`, `.green()`, and `.blue()`

These return the amount of red, green, and blue, respectively, that the sensor is currently detecting as an integer.

### `.alpha()`

This returns the amount of light the sensor is currently detecting as an integer.

### `.argb()`

This returns the combined amounts of red, green, and blue currently detected.

Using these methods, you can compare colors sensed at different points in your OpMode.

To learn more about sensors, you can use the code examples found in the `FtcRobotController > java > org.firstinspires.ftc.robotcontroller > external.samples` folder, or use the [official FTC JavaDocs](https://ftctechnh.github.io/ftc_app/doc/javadoc/index.html).

## Check Your Understanding

1. Why do we use sensors?
2. Can you provide an example of a game challenge that could be solved with a Color Sensor?
3. What does the .alpha\(\) method do?

