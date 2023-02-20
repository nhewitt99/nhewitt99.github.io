---
layout: page
title: VHDL CPU
description: Designing a pipelined CPU from scratch, running a subset of the ARM ISA
img: /assets/img/cpu.png
importance: 4
category: Bite-Size
---

# Abstract
This was a final project for my undergraduate Computer Organization course.
Using VHDL, a hardware description language, I wrote a pipelined 32-bit CPU entirely from scratch.
It is a Harvard-style CPU based on a subset of ARMv8, and is capable of running arbitrary programs written in its assembly language.
There is a supplied demo program that recursively solves for the n'th entry of the Fibonacci sequence.
The pipelined version lacks hazard detection, requiring NOPs to be manually entered while programming.
My memory of VHDL has almost completely faded, but this remains one of my favorite undergrad projects.

## [Find it on my Github!](https://github.com/nhewitt99/vhdl-cpu)