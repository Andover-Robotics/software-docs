---
description: What happens on competition day?
---

# FTC Match Structure

A standard match in an FTC competition consists of several important elements. Two **alliances**, red and blue, face off in each match and try to score as many points as possible. Each alliance consists of **two robots.** Every match is **two and a half minutes long**, but that time may be split into 4 distinct phases. Each phase is briefly described below.

## Pre-Match 

Before any robots start moving, teams bring their robots to the field. Every season has different rules, but there will always be rules that determine where a robot can and cannot be placed before the match. Robots are placed in the field in accordance with these rules. Once the robots are in the field, the drivers of each **initialize but do not run** their program for the next phase, the autonomous period. When both alliances and all 4 sets of drivers have initialized their programs, any randomization required for the game is done \(most games will include sets of elements that are placed in a specific area of the field but are in random pattern\).

### How does this period affect code?

* The **starting position** of the robot may be known before competition day \(it may be narrowed down to one or a small number of locations, depending on your alliance partner's starting position\)
* The **starting orientation** of the robot may be known before competition day
* The **initial state** of the robot \(servo positions, lift height, etc.\) may be known before competition day
* The state of any **randomized game elements** may not be known before competition day, so **writing a different program for each possible outcome is not an option**

## Autonomous

The match begins with a **30-second** autonomous period. During the autonomous phase, robots may only operate on **preprogrammed instructions**. That is to say, **drivers cannot touch the phone or controllers during this phase to control the robot**. Each game will typically have objectives that only give points when performed autonomously or will be worth more points during the autonomous phase. 

### How does this period affect code?

* Autonomous code must be written so that the robot can perform it **without any outside influence**
  * Copious **testing** will be required to ensure consistency and performance
* **Communication** is essential! If some team members focus exclusively on software and others focus exclusively on hardware, it is unlikely that the robot will perform at its best autonomously. New additions to the robot may often make autonomous objectives possible or easier. The mechanic that performs best in the TeleOp will not always be the mechanic that performs the best in the Autonomous period, so always make sure your team is communicating!

## TeleOp

The TeleOp period follows the Autonomous period. It is **two minutes long**, and there is a short period of time between Autonomous and TeleOp so that drivers may initialize their TeleOp programs and pick up their controllers. The TeleOp period **allows the drivers to control their robot** with their controllers \(a team may use either 1 or 2 controllers\), although segments of autonomous code may often be included to simplify controls and allow the drivers to focus on the game. Game objectives during the TeleOp period are different than those of the Autonomous period, and are often involve far too much variability to make fully-autonomous programming viable.

### How does this period affect code?

* The **gamepad** can \(and should\) be read and its state should be interpreted to decide what the robot will do
* Code efforts should be **focused on the drivers**: be sure to listen to your drivers to adjust controls and speeds according to their comforts
  * If your team is using 2 controllers during TeleOp, it is important to consider which actions are delegated to which controllers; some may find it difficult to drive, rotate, and control the intake simultaneously while others may prefer to do so. 

## End Game

The final 30 seconds of the TeleOp period is known as "end game." The rules remain the same, and no program switches should be made. However, each game typically has at least one objective that only scores points during end game, such as parking in a certain location.

### How does this period affect code?

* Be sure drivers have enough control over the robot to be able to achieve all of the TeleOp objectives your team wants to complete, including end-game-exclusive objectives

Now that you have an understanding of the structure of a FTC match, we will explore how programs are written for Autonomous and TeleOp in depth.



