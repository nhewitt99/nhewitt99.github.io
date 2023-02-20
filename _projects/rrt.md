---
layout: page
title: RRT* in ROS
description: Manipulator path planning using the native ROS MoveIt C++ bindings
img: /assets/img/arm-onebox-good.png
importance: 0
category: Bite-Size
---

# Abstract
This was a group final project for my Kinematics, Dynamics, and Control class, done with Everardo Gonzalez and Colin Mitchell.

Path planning algorithms are a rich area of research in robotics, as finding a collision-free path between two points is essential yet combinatorially intractable.
Such algorithms output a sequence of waypoints that, if followed, would move a robot to a goal point while minimizing some cost (such as time) and satisfying environmental constraints (such as avoiding collisions).
Because of the massive search space for path planning on robots with many degrees of freedom, stochastic algorithms are often used which can provide convergence guarantees without an exhaustive search.
Randomly-exploring Random Tree (RRT) is one such algorithm commonly used.
It has many extensions, such as RRT\*, which intelligently rewires its graph of explored configurations to result in shorter trajectories.
Although ROS has a large library of watertight path planners already made available through MoveIt, our goal was to reimplement RRT and RRT\* from scratch to familiarize ourselves better with the MoveIt bindings.
*We successfully implemented RRT and RRT\*, incorporated them with the native MoveIt interfaces, and analyzed our implementations' performance on a Panda Franka model.*

# Technologies Used
- ROS, MoveIt
- C++, Boost
- Kinematics
- Graph Theory

# Results
Our completed planners successfully replicated RRT and RRT\* and interfaced with the C++ MoveIt bindings.
This meant that our custom planner could be called through the existing ROS infrastructure, such as setting goals and querying paths interactively in RViz, and used the collision checking and kinematic models available through MoveIt.

<div class="h-100 d-flex align-items-center justify-content-center">
    <video class="img-fluid rounded z-depth-1" src="{{ '/assets/vid/rrt.mp4' | relative_url }}" autoplay loop>Video of RRT goes here-- try refreshing the page.</video>
</div>
<div class="caption">
    A Panda Franka arm interpolates along a path (pink) found using RRT. The whole graph, composed of points in configuration space, is mapped to task space and visualized in green.
</div>

The animation above shows an early test of RRT, where a graph was composed with relatively few points and a large maximum connection length in order to result in an uncluttered visual.
The Panda Franka successfully finds a path from right to left as queried, and we demonstrate it interpolating along this path.
Below are some results from running RRT\* in an environment with obstacles.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        <img class="img-fluid rounded z-depth-1" src="{{ '/assets/img/arm-onebox-good.png' | relative_url }}" alt="" title="example image"/>
    </div>
    <div class="col-sm mt-3 mt-md-0">
        <img class="img-fluid rounded z-depth-1" src="{{ '/assets/img/arm-corridor.png' | relative_url }}" alt="" title="example image"/>
    </div>
</div>
<div class="caption">
    Left, our planner navigates effectively around an obstacle. Right, the planner struggles to find a good path between the corridor formed by two obstacles.
</div>

Overall, our planner is computationally slower and returns longer paths than the reference implementations from MoveIt.
This is because the MoveIt implementations draw on a wealth of optimizations and parallelization, while our project followed only the canonical algorithm laid out in the RRT\* paper.
In particular, MoveIt uses better-informed sampling methods, finding solutions even with graphs an order of magnitude smaller than ours.

Additionally, our nodes were found in configuration, not task space, resulting in some unintuitive results.
Our graphs often would consist of concentric shells with few interconnections, because moving between them would require a large change in configuration space despite their small distance in the task space.
This can be seen in the failed corridor case above.
The manipulator must move away from its target in order to reach the closest connection to move inward, before finally moving towards the target along this inner shell.
