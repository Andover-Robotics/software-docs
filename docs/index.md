---
summary: Welcome! Let's make your robot smart.
---

# Introduction

Welcome to the world of FTC Software! By programming your team's robot for even part of a season, you will surely bring your critical thinking, engineering, and problem solving skills to the next level. It can also direct you in your career or college major searching: from collaborative engineering to advanced control theory, coding in the FTC gives you a preview of the professional industry of innovative robotics and the application of programming skills in the physical world. Although learning the FTC coding process may seem like a daunting task, this guide is here to simplify the process and guide you (and your team) to a working robot ready to dominate the competition.

This online guide serves as a parallel resource to the lessons that the Chief Software Officers host during club meetings. The lessons complement this guide by demonstrating the presented concepts using examples on real hardware.

This guide is also meant to be referenced frequently during the competition season. It includes many takeaways from the club's past mistakes that help you troubleshoot your code. It identifies some of the principles and priorities that your code should follow. It explains the social implications of programming for FTC, including the phenomena of working with a team of mostly hardware specialists. To summarize, it prepares you to produce competitive, reliable, maintainable code for a FTC robot.

Ready to get started? Let us introduce you to the FTC Control System.

{% content-ref url="the-ftc-control-system.md" %}
[the-ftc-control-system.md](the-ftc-control-system.md)
{% endcontent-ref %}

## General Programming Resources

This guide assumes that you have sufficient background knowledge in computer science fundamentals and Java syntax. To supplement your knowledge in those fields and your experience in ARC, the following resources are available:

* [_Think Java_ by Allen Downey and Chris Mayfield](https://books.trinket.io/thinkjava/index.html) (recommended)
* [A beginner's guide to Git](https://medium.com/free-code-camp/a-beginners-guide-to-git-how-to-create-your-first-github-project-c3ff53f56861)

## FTC Programming Resources

Your knowledge of FTC software should not be limited by the scope of this guide. The following resources can help you understand more aspects of programming in FTC. If you are new to coding at ARC, this is a great place to start. Just pick a spot that best reflects your current learning progress and start experimenting.

* [**Think Java**](https://books.trinket.io/thinkjava/index.html) is a full (but concise) textbook that introduces newcomers to computer science through Java. This book includes concepts that are not relevant to programming at ARC, but it can be a good option if you want to program outside of ARC or if you aren't sure about something in Java.
* [**Game Manual 0**](https://gm0.copperforge.cc/en/stable/docs/software/index.html)  is an invaluable guide for FTC teams that covers nearly everything teams need to know, including awards, mechanical concepts, and programming. It offers a rather minimalistic introduction to Java that may not lead to a full understanding of computer science. This is a good option if you want to program at ARC exclusively.
* [**Robotics Java**](https://robotics-java.learnwhiledoing.org) is a much more comprehensive guide to FTC software than its section in Game Manual 0, and its introduction to concepts in Java is more solid as well. **We recommend this resource for everyone.**
* The **ARC Software Codio course** contains questions that assess your knowledge of the topics covered in this website, ARC Software. We try to make it more interesting than rote memorization and recall by asking you to examine the club's past code and diagnose problematic code segments. Ask a member of the ARC Board for information on how to join this course.

## FTC Library Resources

To save ourselves time and enhance our competitive performance, we use a few third-party libraries (external code modules) to complement the FTC SDK. To understand how each library works, check out the following guides.

* **Road Runner** is an advanced motion planning library for FTC. We mainly use it to improve our robot's ability to navigate during autonomous.
  * [Learn Road Runner](https://www.learnroadrunner.com)
  * [Road Runner docs](https://acme-robotics.gitbook.io/road-runner/)
* **FTCLib** __ is an all-encompassing library that includes convenient abstractions for various needs, including controller reading, Mecanum drive and localization, and computer vision.
  * [FTCLib](https://docs.ftclib.org/ftclib/)
    * [WPILib tutorials](https://docs.wpilib.org/en/stable/docs/software/examples-tutorials/trajectory-tutorial/) (FTCLib is modeled after WPILib)
* [**REVExtensions2**](https://github.com/OpenFTC/RevExtensions2) offers neat extra features that give us more control over the REV Expansion Hubs (see [The FTC Control System](the-ftc-control-system.md#rev-expansion-hub)).
* [**FTC Dashboard**](https://github.com/acmerobotics/ftc-dashboard) is a neat webpage that shows the robot's detected position on the field and can graph various parameters as well as change `public static` variables on the fly.
* [**ARC-Core**](https://github.com/andover-robotics/arc-core) is our own library for code that applies to all teams. It contains a Mecanum drive implementation and support for various unit conversions.

## Other Resources

* [Official Documentation](https://www.firstinspires.org/resource-library/ftc/technology-information-and-resources)
* [Official FTC SDK Javadocs](https://first-tech-challenge.github.io/SkyStone/doc/javadoc/index.html)
* [Official Robot Controller Repository Wiki](https://github.com/FIRST-Tech-Challenge/FtcRobotController/wiki)
* [Official Java Tutorials Playlist](https://www.youtube.com/playlist?list=PLEuGrYl8iBm7wW9gyxpLDhBJAOWDZid1P)
* [_Intro to Control Theory_ by Wesley Aptekar-Cassels](https://blog.wesleyac.com/posts/intro-to-control-part-zero-whats-this)
* [_Controls Engineering in FRC_ by Tyler Veness](https://file.tavsys.net/control/state-space-guide.pdf)
* [FTC Discord Server](https://discord.gg/first-tech-challenge)
