---
summary: It is 2 minutes of driver operated robot action.
---

# The TeleOp Period

After the Autonomous period \(where the robot must operate entirely on preprogrammed instructions\), the TeleOp period, in which the drive team can control the robot using gamepads, begins and continues until the end of the match. The TeleOp period lasts 120 seconds \(or 2 minutes\) in total.

The TeleOp period has fewer possible scoring objectives than Autonomous, so being competitive in TeleOp means being able to accomplish the scoring objective quickly and repeatedly. For the first 90 seconds of TeleOp, the robot works with its alliance partner to score as many points as possible using the TeleOp scoring objectives. The last 30 seconds are what is known as the End Game, where we have opportunities to complete specific scoring objectives to earn extra points. These objectives revolve around the way the robot finishes the game \(like parking in a specific area or hanging off of a game element\).

## The Duty of a TeleOp OpMode

Your TeleOp OpMode should be programmed to respect the following priorities:

1. Relay driver inputs to robot hardware as quickly as possible
2. Use software limits to prevent damage to hardware components
3. Use Driver-Controlled Enhancements to facilitate driver operations

In addition, your TeleOp OpMode should abide by the following principles:

1. Drivers must be able to abort and override automated operations instantly
2. Drivers must be able to override software limits
3. The cycle rate of the OpMode should be maximized \(see the Optimization section for how to accomplish this\)

## Driver-Controlled Enhancements

Many scoring objectives during TeleOp from previous years involve a fixed sequence of actions for the driver. If the hardware is reliable enough, it is often advantageous for your TeleOp program to perform this sequence of actions automatically. Doing so can improve your team's scoring performance and give you an advantage in the Control Award application.

You can implement these enhancements with Finite State Machines, which provide an abstraction for the drivers by having states represent series of actions and either transitioning between states automatically or allowing the drivers to cause state transitions. Of course, there should be a "Manual" state that allows drivers to exercise total control over the robot.

