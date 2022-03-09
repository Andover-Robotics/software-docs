---
summary: What happens on competition day?
---

# FTC Match Structure

A standard match in an FTC competition consists of several important elements. Two **alliances**, red and blue, face off in each match and try to score as many points as possible. Each alliance consists of **two robots.** Every match is **two and a half minutes long**, but that time may be split into 4 distinct phases. Each phase is briefly described below.

![](../assets/FTC Match Structure@2x (1).png)

## Pre-Match&#x20;

Before any robots start moving, teams bring their robots to the field. Every season has different rules, but there will always be rules that determine where a robot can and cannot be placed before the match. Robots are placed in the field in accordance with these rules.

* Once the robots are in the field, the drivers of each **initialize but do not run** their program for the next phase, the autonomous period.
* When both alliances and all 4 sets of drivers have initialized their programs, the four drive teams will enter a **"hands-off position,"** where they are not allowed to touch the Driver Station phone or any controllers. Any randomization required for the game is done (most games will include sets of elements that are placed in a specific area of the field but are in random pattern).

### How does this period affect code?

* The **starting position** of the robot may be known before competition day (it may be narrowed down to one or a small number of locations, depending on your alliance partner's starting position)
  * For some seasons' games, you might need to negotiate with your alliance partner regarding starting positions, but other seasons may incentivize specific starting configurations.
* The **initial state** of the robot (servo positions, lift height, etc.) may be known before competition day
* The state of any **randomized game elements** is not known before enacting the "hands-off position" in each match, so **selecting a different OpMode for each possible outcome is not an option**

## Autonomous

The match begins with a **30-second** autonomous period. During the autonomous phase, robots may only operate on **preprogrammed instructions**. That is to say, **drivers cannot touch the phone or controllers during this phase to control the robot**. Each game will typically have objectives that only give points when performed autonomously or will be worth more points during the autonomous phase.

### How does this period affect code?

* Autonomous code must be written so that the robot can perform it **without any driver control**
  * Copious **testing** will be necessary to ensure consistency and performance
* **Communication is essential!** If some team members focus exclusively on software and others focus exclusively on hardware, it is unlikely that the robot will perform at its best autonomously. New additions to the robot may often make autonomous objectives possible or easier. The mechanism that performs best in the TeleOp will not always be the mechanism that performs the best in the Autonomous period, so always make sure your team is communicating!

## TeleOp

The TeleOp period follows the Autonomous period. It is **two minutes long**, and there is a short period of time between Autonomous and TeleOp so that drivers may initialize their TeleOp programs and pick up their controllers. The TeleOp period **allows the drivers to control their robot** with their controllers (a team may use either 1 or 2 controllers), although segments of autonomous code may often be included to simplify controls and allow the drivers to focus on strategy. Most game objectives during the TeleOp period are different than those of the Autonomous period, and often involve far too much variability to make fully-autonomous programming viable.

### How does this period affect code?

* The **gamepad** can (and should) be read, and its state should be interpreted to decide what the robot will do
* Code efforts should be **focused on the drivers**: be sure to listen to your team's drivers to adjust controls and speeds according to their preferences
  * If your team is using 2 controllers during TeleOp, it is important to consider which actions are delegated to which controllers; some may find it difficult to drive, rotate, and control the intake simultaneously while others may prefer to do so. Evaluating control schemes through testing is a good idea.

## End Game

The final 30 seconds of the TeleOp period is known as "end game." The rules remain the same, and the robot should continue running the same OpMode. However, each game typically has at least one objective that only scores points during end game, such as parking in a certain location.

### How does this period affect code?

* Be sure drivers have enough control over the robot to be able to achieve all of the TeleOp objectives your team wants to complete, including end-game-exclusive objectives

Now that you have an understanding of the structure of a FTC match, we will explore how programs are written for Autonomous and TeleOp in depth.

