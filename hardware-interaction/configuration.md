---
description: How do you call the motor plugged into this port? "motorFL".
---

# Configuring Hardware

To be ultimately useful, your OpMode needs to be able to interact with robot hardware. In FTC, each hardware device that you wish to use has a distinct name, using which you reference the device in code. A collection of mappings from device names to their respective hardware ports is a **configuration**.

Configurations can be created on the Robot Controller or the Driver Station. You can create as many configurations as you want on one device, but only one configuration can be active at any moment. When an OpMode runs, only the mappings from the active configuration can be used.

## Connecting Two Expansion Hubs

One REV Expansion Hub only provides four motor ports, and that is not sufficient in most competitive designs. Since it is legal to have up to eight motors in an FTC robot, we typically daisy-chain two Expansion Hubs together and connect electronics to both of them.

Most of the existing Expansion Hubs in the club should be configured for daisy-chaining already, but if we decide to obtain more, refer to FTC's official [control system documentation](https://github.com/ftctechnh/ftc_app/wiki/Using-Two-Expansion-Hubs) for how to configure them. Alternatively, you may reference the following video.

{% embed url="https://youtu.be/7rbLDden-Rs" %}

## Making a Configuration

{% embed url="https://youtu.be/qm9mcyrjY54" caption="Configuring with Modern Robotics modules" %}

{% embed url="https://youtu.be/VHyKE3B170k" caption="Configuring with REV Expansion Hubs" %}

Follow the flow of the video that corresponds to your control system. When creating a new configuration, ensure that the REV Expansion Hubs or Modern Robotics modules that are connected to the Robot Controller are the ones that will be used on the final competition robot. Since configurations apply to specific hubs and modules, replacing them typically requires a total reconfiguration.

In addition to the configuration itself, we recommend that you put descriptive, distinct labels on the wires that connect to your Expansion Hubs. Not only will this help you reconfigure the robot later on, it will also save time when troubleshooting potential problems with electronics. Make sure that these labels stay up-to-date as you make changes to the wiring scheme of your robot, as misleading labels are far worse than not having any labels.

![A label for a wire \(from FTC YouTube video &quot;REV - Managing Wires&quot;\)](../.gitbook/assets/image%20%283%29.png)

Although the club does not have official device naming conventions, we recommend that your team establish some guidelines about device names. Following these guidelines reduces inconsistency and helps you remember the names exactly when referencing them in code later.

