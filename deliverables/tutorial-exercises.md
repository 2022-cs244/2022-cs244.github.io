---
layout: page
title: Tutorial Exercises
---

The goal of these exercises is to allow you to become familiar with the following development tools that you will be using to build your router:
* The P4 compiler
* BMv2 in Mininet
* p4app

Here is a bit of information about each of these tools.

P4 Compiler
-----------

To run P4 code, it has to be compiled for the target (e.g. hardware switch, NIC, software switch). Each target has a different P4 compiler backend. In the first part of this course we will be using the [P4 reference compiler](https://github.com/p4lang/p4c) for BMv2.


BMv2 in Mininet
---------------

P4.org has developed an open source software switch called BMv2 (behavioral model version 2) designed to be a target for P4 programs. That is, P4 programs can be compiled onto it to configure how it processes packets. Every P4 target supports one or more P4 target architectures. BMv2 was initially designed with support for the so called V1Model architecture.

p4app
-----

This tool provides a portable way of packaging and running P4 code and control planes with BMv2 and Mininet. Inside a p4app package (simply referred to as a "p4app"), there is a `main.py` entry point. This defines the topology, the P4 code to run, and runs a workload on the network by executing commands on hosts. The p4app runs inside a Docker container that has all the dependencies and tools (P4 compiler, BMv2, Mininet, scapy), so they don't have to be installed on the host computer.

Prerequisites
-------------

Make sure that you have completed the [Getting Started]({{ site.baseurl }}/deliverables/getting-started) deliverable where you set up your environment. If you have problems installing the dependencies directly on your computer, you can use the virtual machine, which has all of the necessary dependencies installed on it to work with p4app (i.e. Docker).

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

