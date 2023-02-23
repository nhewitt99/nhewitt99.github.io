---
layout: page
title: Multiobjective Manipulator Control
description: Learning what matters when to complete challenging, sparsely-rewarded manipulation tasks
# img: /assets/img/apis.jpg
importance: 0
category: Large
---

# Abstract
This project is the focus of my Master's degree, completed under the advising of Dr. Kagan Tumer at Oregon State University.

Autonomous robots are a promising technology for fields such as underwater maintenance or marine biological sampling, where existing robotic solutions require skilled and expensive human teleoperators.
These tasks are extremely challenging for autonomous solutions, in large part because a high level task, such as caching a starfish, encodes many implicit tradeoffs between disparate objectives, such as speed, stability, energy use, and not harming the creature.
We propose a system that handles manipulation tasks in an inherently multi-objective framework, rather than compressing a desired behavior into a single signal via scalarization or reward shaping.
This leverages the intuition that *conflict is good*; preserving multiple objectives in a system lends adaptivity to a controller, since it can receive rich feedback related to different outcomes as its priorities change.
The resulting system can model complex environmental dynamics, generates controls that simultaneously optimize potentially-conflicting objectives, and learns "what matters when" to handle the dynamic trade-offs encountered during a robotic deployment.

# Technologies Used
- Python
- Multi-objective optimization
- Model predictive control
- Deep learning
- PyBullet, OpenAI Gym

:construction: Under Construction! :construction: