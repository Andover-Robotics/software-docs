---
description: 'It consists of a phone, a hardware hub, and another phone.'
---

# The FTC Control System

## Components

![Components of the FTC Control System \(from official wiki\)](.gitbook/assets/image%20%288%29.png)

Robots in FTC are controlled using Android phones. The **Robot Controller** phone is secured on the robot and connected to all of its electronics, whereas the **Driver Station** is kept with the drivers and connected to the game controllers. These two phones communicate with each other using WiFi Direct.

### Robot Controller

The **Robot Controller** phone is responsible for controlling the robot and making decisions using sensor inputs, which is what your code will accomplish. Our code runs on the FTC Robot Controller app, which is what we upload onto the Robot Controller phone. You do not need to worry about wireless communication—that is handled by the app, not your code.

### Driver Station

The **Driver Station** phone acts like a television remote. It allows you to control the execution of [OpModes](the-opmode-1/defining-the-opmode.md), [configure hardware](hardware-interaction/configuration.md), and view [telemetry](the-opmode-1/telemetry-and-debugging.md) data remotely. It runs the FTC Driver Station app. Your code should never make its way onto this phone directly—we accidentally uploaded to a Driver Station once, and the result was disastrous!

## Types of 12V Connectors

Before we dive into the hardware controllers, we need to familiarize ourselves with a few types of connectors that deliver power from the 12V robot battery to the various components of the robot.

### Anderson Powerpole

![The Anderson Powerpole Connector \(from goBILDA.com\)](.gitbook/assets/image%20%2812%29.png)

The **Anderson Powerpole** \(or simply **Powerpole**\) connector is the most popular power delivery connector in FTC. It typically delivers at least 12V to the various hardware controllers and motors of the robot.

### XT30

![The XT30 Connector \(from goBILDA.com\)](.gitbook/assets/image%20%2810%29.png)

The **XT30** connector is primarily found on REV products only. It delivers power from the 12V robot battery to the REV Expansion Hubs.

### Tamiya

![The Tamiya Connector \(from goBILDA.com\)](.gitbook/assets/image%20%283%29.png)

The **Tamiya** connector is probably the second most popular connector in modern FTC. Most competition-legal batteries have a Tamiya interface.

### JST VH

![The JST VH Connector \(from goBILDA.com\)](.gitbook/assets/image%20%286%29.png)

The **JST VH** connector connects REV Expansion Hubs to various 12V motors. They only deliver power.

## Hardware Controllers

Hardware controllers act as the middleman between the Robot Controller and the individual hardware devices. We connect the Robot Controller to one or more hardware controllers, which connect to specific motors, servos, and sensors.

As of 2019-2020, ARC has two types of hardware controllers: Modern Robotics and REV Expansion Hubs.

### Modern Robotics

![Parts included in the MR Robot Electronics Bundle \(from official website\)](.gitbook/assets/image%20%285%29.png)

Despite its optimistic name, Modern Robotics \(MR\) electronics components [will become illegal in the 2020-2021 season](http://firsttechchallenge.blogspot.com/2019/06/first-tech-challenge-technology-updates.html). ARC has primarily relied on these for the past three years, so we have them in great abundance. There are four types of controllers in the Modern Robotics system:

* The [**Core Power Distribution Module**](https://modernroboticsinc.com/product/core-power-distribution-module/) is where the Robot Controller phone and the 12V robot battery are connected to the robot's electronics. It has the following parts:
  * 6 Powerpole connectors for power distribution
  * 6 USB ports for the delivery of control commands
  * A built-in power switch
  * A built-in fuse
  * A Tamiya connector that connects to the 12V battery
  * A female Mini-USB port that connects to the Robot Controller
* The [**Core Motor Controller**](https://modernroboticsinc.com/product/core-motor-controller/) allows motors to be connected and controlled by the Core Power Distribution Module. Each Core Motor Controller has two Powerpole connectors and two 4-pin encoder connectors that connect to two motors. It also has a third Powerpole connector and a mini-USB port that connect to the Core Power Distribution Module.
* The [**Core Servo Controller**](https://modernroboticsinc.com/product/core-servo-controller/) allows servos to be connected and controlled by the Core Power Distribution Module. Each Core Servo Controller has six 3-pin connectors that connect to up to six servos. It also has a third Powerpole connector and a mini-USB port that connect to the Core Power Distribution Module.
* The [**Core Device Interface**](https://modernroboticsinc.com/product/core-device-interface-module/) connects various sensors to the Core Power Distribution Module. Check MR's website for more information.

All electronics in the Modern Robotics system \(except motors\) run at 5 volts. This is the most common voltage rating found in our numerous electronic peripherals.

{% embed url="https://youtu.be/E6bOTkQWaTI" %}

## REV Expansion Hub

![Diagram of connections for the REV Expansion Hub \(from official wiki\)](.gitbook/assets/image%20%287%29.png)

Unlike the Modern Robotics system, the [**REV Expansion Hub**](http://www.revrobotics.com/rev-31-1153/) combines the adapters for all types of peripherals into one unit. Each unit supports four motors, six servos, two analog sensors, four digital sensors, and four I²C sensors. Typically, each competition robot has two Expansion Hubs that are connected to each other using [this process](https://github.com/ftctechnh/ftc_app/wiki/Using-Two-Expansion-Hubs).

All motor encoder ports and sensor ports run at 3.3 volts in the REV ecosystem. To use any sensor or encoder that needs 5 volts to function correctly, a [level shifter](http://www.revrobotics.com/REV-31-1389/) is needed to convert the voltage.

{% hint style="info" %}
Many of our motors have encoders that require 5 volts to function. Our NeveRest 40s, for example, have built-in encoders that function incorrectly when only 3.3 volts are supplied. When your `RUN_USING_ENCODER` or `RUN_TO_POSITION`modes do not function correctly, this could be the culprit!
{% endhint %}

REV's [official guide to the Expansion Hub](https://www.revrobotics.com/content/docs/REV-31-1153-GS.pdf) is a great reference for peripheral compatibility and troubleshooting purposes.

{% embed url="https://youtu.be/fU1GXteByJw" %}



