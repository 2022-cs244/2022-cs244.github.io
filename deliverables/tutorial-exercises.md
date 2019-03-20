---
layout: page
title: Tutorial Exercises
---

The goal of these exercises is to allow you to become familiar with the following two development tools that you will be using to build your router:
* P4->NetFPGA
* BMv2 in Mininet

Here is a bit of information about each of these tools.

P4->NetFPGA
-----------

[Here](https://github.com/NetFPGA/P4-NetFPGA-public/wiki) is the P4->NetFPGA wiki home page. Your first task is to quickly skim the [Workflow Overview](https://github.com/NetFPGA/P4-NetFPGA-public/wiki/Workflow-Overview) page. This page contains most of the documentation that you will need when working with the P4->NetFPGA tools. [Here](https://www.repository.cam.ac.uk/handle/1810/288563) is a paper that describes the tools in more detail if you are interested.

The P4->NetFPGA workflow is built on top of the Xilinx P4-SDNet compiler. This compiler extends the open source [p4c](https://github.com/p4lang/p4c) front end compiler to generate HDL modules for Xilinx FPGAs. Eventually, all P4 features will be supported, but for now there are some that are not. Please refer to the [SDNet P4 Support]({{ site.baseurl }}/documentation/p4c-sdnet-missing-features.pdf) page for a breakdown of the features that are supported/unsupported. These tools should be considered alpha quality research code. Throughout the quarter you may run into bugs. If you believe you have found a bug, first post a question on the slack channel. If the instructor confirms that it is indeed a bug, they may ask you to submit a GitHub issue to the [starter code repo](https://github.com/cs344-stanford-19/P4-NetFPGA-CS344-19) so that others are aware of its existence.


BMv2 in Mininet
---------------

P4.org has developed an open source software switch called BMv2 (behavioral model version 2) designed to be a target for P4 programs. That is, P4 programs can be compiled onto it to configure how it processes packets. Every P4 target supports one or more P4 target architectures. BMv2 was initially designed with support for the so called V1Model architecture. The CS344 instructors have added initial support for the [SimpleSumeSwitch architecture](https://github.com/NetFPGA/P4-NetFPGA-public/wiki/Workflow-Overview#simplesumeswitch-architecture) so that we can run (virtually) the same P4 programs in both Mininet and the NetFPGA platform. Please review [this page]({{ site.baseurl }}/documentation/sss-bmv2) to learn more about the current SimpleSumeSwitch support in bmv2 and Mininet.

Prerequisites
-------------

Make sure that you have completed the [Getting Started]({{ site.baseurl }}/deliverables/getting-started) deliverable where you set up your virtual machine and P4-NetFPGA repository. The virtual machine has all of the necessary dependencies installed on it to work with bmv2 in Mininet.

The Exercises
-------------

There are two main exercises for you to complete. In the first exercise, you will implement a very basic IPv4 router in Mininet only (i.e. not on the NetFPGA platform). In the second exercise you will implement a simple switch calculator on both the NetFPGA platform and in Mininet.

### Exercise 1 - Basic IPv4 Forwarding

In this exercise you will implement very basic (and static) IPv4 forwarding with just enough functionality to be able to ping between the different hosts that are connected to the routers. We have provided starter code for you, which you can find in the following directory in the p4 user's home on the virtual machine: `~/tutorials/exercises/basic`. Read through the [README](https://github.com/CS344-Stanford/tutorials/tree/si/skt/SimpleSumeSwitch/exercises/basic) file located in that directory for more details about how to complete the exercise.

After you complete the exercise and can successfully ping between the various hosts connected in the Mininet topology, you will need to answer the set of questions listed in the [README](https://github.com/CS344-Stanford/tutorials/tree/si/skt/SimpleSumeSwitch/exercises/basic) file. Please include your answers in the README file located at `$SUME_SDNET/projects/simple_router`, i.e. the README file for the simple_router project in your fork of the P4-NetFPGA repository. After you've answered the questions, please commit the changes and push your changes to GitHub so that the instructor's can see your answers.

### Exercise 2 - Switch Calculator

In this exercise you will complete the functionality of a P4 program to configure a switch as a basic calculator. You will first develop and test your P4 program using the P4->NetFPGA workflow and run it on the NetFPGA platform. Then you will see how you can also test that P4 program in the Mininet environment.

The [P4->NetFPGA Tutorials](https://github.com/NetFPGA/P4-NetFPGA-public/wiki/Tutorial-Assignments) page describes three exercises:
* Switch Calculator
* TCP Monitor
* In-band Network Telemetry (INT)

The starter code for these exercises is already in the repository that you set up on your development machine in the [Getting Started]({{ site.baseurl }}/deliverables/getting-started) deliverable. For this assignment you only need to complete the [switch_calc exercise](https://github.com/NetFPGA/P4-NetFPGA-public/wiki/Tutorial-Assignments#assignment-1-switch-calculator), but you may want to review the other exercises as well.

You should complete this exercise on your assigned development machine, which has all of the necessary dependencies required to use the P4->NetFPGA workflow (e.g. Xilinx SDNet, Vivado, etc.). Go through the entire process of generating the FPGA bitstream for your switch_calc solution and testing the design on hardware using the approach outlined in the above link.

After you have the design successfully working in hardware, the next step of this assignment is to test (virtually) the same design in Mininet. Commit and push your switch_calc solution to your repository and then pull the changes into the clone of your repo on the virtual machine that you used to complete Exercise 1.

Change directories into the `~/tutorials/exercises/switch_calc` folder on the VM and follow the instructions in the README file there test your solution in Mininet.

Submission
----------

After you have completed the above exercises, please send an email to the instructors (sibanez@stanford.edu and stollman@stanford.edu) with two things:
* A link to your README file on GitHub that contains the answers to the questions from Exercise 1.
* The FPGA bitfile that you generated for the switch_calc exercise.

