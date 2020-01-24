### Self-Driving Car Engineer Nanodegree Program

### Path-Planning-Project (Highway Driving)

#### Introduction

In this project my goal was to safely and comfortably navigate around a virtual highway with other traffic within 50 MPH speed limit. Navigating safely and comfortably means we don't bump into other cars, we don't exceed the maximum speed, acceleration and jerk requirements. In this virtual simulator, it sends car's localization (car’s position and velocity) and sensor fusion data. The reach the goal for this project, I spaced points in time at 0.02 seconds representing the car’s trajectory. I used workspace, but if you want to your local machine websocket and simulator should be installed and configured which can ben find in project github reposity (https://github.com/udacity/CarND-Path-Planning-Project)

#### Project Goals Achieved For The following criteria:

- The car was able to driven at least 4.32 miles without incident. It went 5.5 miles without incident.
- The car didn't drive faster than the speed limit.
- Max Acceleration and Jerk were not exceeded.
- Car did not have collisions.
- The car stayed in its lane, except for the time between changing lanes. 
- The car is able to change lanes. The car is able to smoothly changed lanes when it makes sense to do so.

#### The Code Compiles Correctly

No changes were made in the cmake configuration. A new file was added src/spline.h. which I learned from lectures (Q&A). It works great.

#### There is a reflection on how to generate paths.

If I describe my model, I firstly start with saying "lecture notes, especially which is given end of this unit as Q&A is great roadmap for me". I started with using this lecture given codes, which was very useful as a begining especially for the trajectory blocks. Then I added necessary parts into it, for the prediction and behavior blocks.

I added all necessary codes into main.cpp. But on the other hand, as an alternative method there would be more *.cpp files created for prediction, behavior, trajectory etc. But starting my coding with Q&A, I decided to go with same cpp file, just only added splie.h to manage trajectory stage. If I had more time for the codding, I would add these separated files.

**Prediction:**

The first part is creates outputs by using car's localization (car’s position and velocity) and sensor fusion data which are given by simulator. As an output, it gives below answer, by using 30 meters as a limit for the distance:

* Is there a car in front of our car
* Is there a car to the right of our car which would make a lane change not safe
* Is there a car to the left of our car which would make a lane change not safe

**Behavior:**

The second part creates outputs by using prediction outputs. It has two decissions:

- If we have a car in front of us, do we change lanes? Is it feasible?
- Do we turn back to middle line, and do we speed up or slow down?

**Trajectory:**

The third and final part of process creates outputs of the trajectory based on the speed and lane output from the behavior, car coordinates and past path points. For this part I especially take help from Q&A video.  In order, this code does the calculation of the trajectory based on the speed and lane output from the behavior, car coordinates and past path points. The spline for the potential new path is generated based on 3 new points 30, 60 and 90 meters ahead. These s and d co-ordinates are used to produce a smooth spline. The number of points in the spline and velocity increment controls the excessive acceleration or jerk limits.

