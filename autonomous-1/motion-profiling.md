# Motion Profiling

_Motion profiling_ is a technique used to plan mobile robot motion on the playing field. It is a response to the question, "how do we travel from point A to point B in a planned manner on the field consistently?" It is a mathematically-driven, more advanced approach to the question, involving trajectories defined using 2D pose coordinates and polynomial splines.

To understand how we arrive at the motion profiling approach intuitively, you should first develop a strong understanding of the simpler techniques of robot motion planning and execution.

## Motion Planning & Execution

We recommend that you watch FRC Team 254's conference presentation on motion profiling below to get a better sense of the entire motion control process and how we intuitively arrive at the solution of motion profiling. It should be more engaging and less mentally demanding than reading this documentation.

{% embed url="https://youtu.be/8319J1BEHwM" %}

{% hint style="info" %}
When learning robotics software techniques, positioning yourself at the level of FRC \(FIRST Robotics Competition\) can often give you an advantage over other FTC teams both in competition and in judging. Don't be afraid to seek information intended for FRC if it is conceptual and applicable to your programming needs.
{% endhint %}

In summary, the more primitive techniques of motion planning and execution include the following:

* _Dead reckoning_ \(time-based autonomous\)
* _Bang-bang control_ \(always pursue the destination at a constant speed\)
* _PID_ \(Proportional-Integral-Derivative\)

Thankfully, the underlying calculus and algebra involved in motion profiling is implemented for you in a software library called _Road Runner_, so you can easily apply motion profiling techniques in FTC.

## Road Runner

\_\_[_Road Runner_](https://github.com/acmerobotics/road-runner) is a motion profiling software library from ACME Robotics that applies motion planning concepts to FTC. The authors of this library have created a separate [documentation GitBook](https://acme-robotics.gitbook.io/road-runner/tour/introduction) that explains the core concepts behind how motion profiling works. 

In summary, the motion planning techniques discussed in this conference presentation 

### Coordinate System

> Robot poses are specified in a coordinate system with positive $$x$$ pointing forward, positive $$y$$ pointing left, and positive heading measured counter-clockwise from the x-axis. \(Road Runner GitBook\)

The coordinate system described here is also applicable to field coordinates. The center of the field is$$(0,0)$$. Positive $$x$$ points toward the top of the field diagram, and positive $$y$$ points toward the left in the field diagram. Conveniently, this means that you can reason about the field coordinate system from the perspective of the **red** driver's box, as the axes align with what we expect in function graphs in algebra.

![The Road Runner field coordinate system in Skystone \(2019-2020\)](../.gitbook/assets/image%20%2820%29.png)



