---
description: It is 30 seconds of fully automatic robot action.
---

# The Autonomous Period

Each match in FTC starts with the **Autonomous period**, in which the robot has to operate on entirely pre-programmed instructions to complete certain objectives. This portion of the game lasts 30 seconds. Objectives often include:

* Ways the robot can start the game \(like descending from a game element\)
* Sensing game elements and performing actions based on their color
* Deploying a _Team Scoring Element_
* Moving the robot to a certain location

Even though the Autonomous period lasts only 30 seconds, its scoring objectives are typically worth more points than those in TeleOp, so it is important to understand how to effectively manipulate the hardware available to accomplish the objectives consistently.

## The Priorities of an Autonomous OpMode

The Autonomous period is where all eyes of the team will point to you, the programmers. A great majority of your work throughout the season will be reflected in these 30 second periods, where your code is subject to the utmost scrutiny. The most important priorities of your Autonomous OpMode should reflect all the scoring objectives of the current year's game. In addition, you should prioritize the following goals:

* **Reliable navigation**: The robot's motion must be consistent between runs such that the scoring objectives have a high chance of being fulfilled _\(See_ [_Motion Profiling_](motion-profiling.md) _for how to accomplish this\)_
* **Human authority**: The drive team should always be able to abort your Autonomous OpMode instantly _\(See_ [_Stopping LinearOpModes_](../the-opmode-1/stopping-linearopmodes.md) _for how to accomplish this\)_
* **System transparency**: Use [telemetry](../the-opmode-1/telemetry-and-debugging.md) appropriately to show information about your Autonomous OpMode's state
* **General consistency**: When making decisions about how to interact with hardware, prioritize consistency between runs

## Devising Paths and Strategies

Each year, the game elements and autonomous scoring objectives are laid out such that teams seeking to complete all scoring objectives during autonomous must design several movement paths for the robot. These paths are implemented into software, executed on the playing field, and reflected in the Control Award submission sheet. The decisions you make when designing them has significant influence on your team's performance, and any small act of negligence in any part of the process can lead to catastrophic consequences.

When designing these paths, you must consider the robot's limitations of independent navigation. Traversing through small corridors between fixed game elements, for example, introduces a factor of uncertainty and should be avoided. Have the robot use external tracking targets to calibrate its spatial awareness against the playing field. Use measurements from the [inertial measurement unit](../hardware-interaction/inertial-measurement-unit.md) to ensure that the robot is oriented correctly for each leg of the path. If it is practical, ask your team about the feasibility of odometry, a localization technique that keeps track of position by measuring the rotation of dead-axle omniwheels as they are spun by the field floor during robot movement.

{% embed url="https://youtu.be/lb1Sn7KMev0" caption="Part 2 of Wizards.exe\'s Odometry Spell Book" %}

## Imperative Implementation

The most common strategy for the Autonomous period is to perform a predetermined sequence of tasks, which can be easily achieved by writing a series of statements in the `runOpMode` method of a `LinearOpMode`. For example, consider the following OpMode definition:

{% code title="MyAuto.java" %}
```java
@Autonomous(name = "My Autonomous", group = "Competition")
public class MyAuto extends LinearOpMode {
  private DriveTrain drive;
  private Arm arm;

  @Override
  public void runOpMode() {
    // initialization statements...
    waitForStart();
    
    drive.driveForwards(10);
    drive.rotateClockwise(90);
    arm.lower();
    arm.grab();
    drive.driveBackwards(5);
    arm.raise();
    drive.rotateClockwise(45);
    drive.driveForwards(30);
    arm.lower();
    arm.release();
  }
}
```
{% endcode %}

{% hint style="info" %}
In this example, we are almost able to read the contents of `runOpMode` out loud and be understood as if we were speaking plain English. Instead of issuing raw numbers to individual hardware devices, this example describes the procedure in a high level of [abstraction](https://youtu.be/6V1sr0XV_Ng), so the technical details are hidden from those who don't need to know them. As your autonomous programs accumulate complexity over time, it is important to utilize abstraction in order to make your code more maintainable and readable to other programmers. Check out [_Integrate with your Team_](../working-with-a-team/integrate-with-your-team.md) for more tips on maximizing your code's cleanliness.
{% endhint %}

If you have an autonomous strategy in mind for your team, think about how it could be translated into software that your robot can execute. Think about how you would structure it and vary it for different starting positions. Think about the points of failure and how your robot would behave it any of them were to fail. Think about how your robot would collaborate with an alliance partner.

The Autonomous period is a very lucrative, risky, and rewarding component of the FTC game. Watching your team's robot execute a successful Autonomous run on the competition field is an experience that you will not forget. A _"**full auto**,"_ an Autonomous procedure that satisfies all of the Autonomous period's scoring objectives, is an incredibly valuable asset of your team that improves your chances of being selected during Alliance Selection dramatically if not make your team an Alliance Captain. Being able to score points consistently during Autonomous qualifies you for the **Control Award**, which specifically recognizes advanced control algorithms that improve your team's competitive performance. The next pages of the Autonomous section will help you leverage the tools at hand to the greatest extent and boost your team's ability to succeed.

