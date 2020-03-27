# Motion Profiling

_Motion profiling_ is a technique used to plan mobile robot motion on the playing field. It is a response to the question, "how do we travel from point A to point B in a specified manner on the field consistently?" It is a mathematically-driven, more advanced approach to the question, involving trajectories defined using 2D pose coordinates and polynomial splines.

To understand how we arrive at the motion profiling approach intuitively, you should first develop a strong understanding of the simpler techniques of robot motion planning and execution.

## Motion Planning & Execution

We recommend that you watch FRC Team 254's conference presentation on motion profiling below to get a better sense of the entire motion control process. It should be more engaging and less mentally demanding than reading this documentation.

{% embed url="https://youtu.be/8319J1BEHwM" %}

In summary, the more primitive techniques of motion planning and execution include the following:

* _Dead reckoning_ \(time-based auto\)
* _Bang-bang control_
* _PID_ \(Proportional-Integral-Derivative\)
* _Motion profiles_

## Road Runner

\_\_[_Road Runner_](https://github.com/acmerobotics/road-runner) is a motion profiling software library from ACME Robotics that applies motion planning concepts to FTC. The authors of this library have created a separate [documentation GitBook](https://acme-robotics.gitbook.io/road-runner/tour/introduction) that explains the core concepts behind how motion profiling works. 

In summary, the motion planning techniques discussed in this conference presentation 

### Coordinate System

> Robot poses are specified in a coordinate system with positive x pointing forward, positive y pointing left, and positive heading measured counter-clockwise from the x-axis.

