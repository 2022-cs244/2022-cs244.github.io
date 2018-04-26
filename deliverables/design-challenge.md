---
layout: page
title: Design Challenge Project Proposal
---

The design challenge is your opportunity to do something novel and interesting. You may propose to do a project of your own choosing, but we do encourage you to consider pursuing one of the potential projects listed below. We would like to avoid having too many groups working on the same project so the proposal will help us to gauge interest in the various topics. The proposal should be a 1-page document that includes the information listed below:

* Project title
* Motivation - why is this project interesting?
* Initial thoughts for system design / verification

# Potential Projects

#### Scheduling Algorithms in P4

The packet processing capabilities of the P4 language are second to none. That being said, there has been very little discussion around ways to program the traffic management capabilities of network devices. Modern programmable switches offer a small menu of common scheduling algorithms, but provide no mechanism for allowing network operators to define their own algorithms. The [PIFO (Push-In-First-Out) queue](http://web.mit.edu/pifo/pifo-sigcomm.pdf) was recently proposed as a convenient abstraction that can be used to implement many different scheduling algorithms, and hence provides a mechanism to make packet scheduling programmable. PIFOs differ from traditional scheduling mechanisms because they decide the packet’s scheduling order at the time of enqueue rather than as the packet leaves the queue. The PIFO queue consists of two components: a programmable rank computation and a fixed scheduler. The rank computation can be expressed in P4 and it produces the packet's rank, which is an indication of its priority. The scheduler then schedules the packet relative to the packets that are sitting in the queue according to it's assigned priority. By using the appropriate rank computation, we can implement many different scheduling algorithms such as:

* Priority queues
* Round robin
* Weighted round robin
* Minimum rate guarantees
* Start time fair queueing
* Deficit round robin
* Least slack time first
* Stop-and-Go Queueing

In this project, you will explore how to practically implement the rank computation for various scheduling algorithms in P4. You may want to use the count-min sketch technique presented earlier in this class or some of the other building blocks described in the [flexswitch paper](https://homes.cs.washington.edu/~arvind/papers/flexswitch.pdf).


#### BMv2 Support for SimpleSumeSwitch

As you saw at the beginning of the class, Mininet is a very convenient tool to use for testing out the functionality of your P4 programs. It allows you to quickly spin up an arbitrary topology of network devices running your programs without needing to compile to an FPGA or manually wire up the topology. The [behavioral model v2](https://github.com/p4lang/behavioral-model) (BMv2) is essentially a library of packet processing components that can be used to build software switches. BMv2 currently supports the simple_switch target. P4 programs that are written for the V1Model architecture can be compiled to run on the simple_switch target. The framework for integrating the BMv2 software switch into the Mininet environment already exists.

This project will consist of two components:

1. Adding support for a new BMv2 target to which P4 programs that are written for the SimpleSumeSwitch architecture can be compiled.
2. Updating the bmv2 backend of the open source [p4c](https://github.com/p4lang/p4c) compiler to support your new BMv2 target.

The end goal is to demonstrate a P4 program written for the SimpleSumeSwitch architecture running in Mininet.


#### Performance Measurement System




#### Heavy Hitter Detection


#### DDos Detection Techniques


#### Improving Congestion Control


#### Network Monitoring System



#### Data Streaming Aggregation


# The Prize

We will invite some members from the networking community to the final presentations & demonstration day. These invited guests will serve as judges along with the instructors to decide upon the best final project. The winning group will have the opportunity to present their demo at the [P4 Workshop in Cambridge, UK](https://p4.org/events/2018-09-24-p4-eu-workshop/). 


# Submission

Please email your proposal to the instructors using the subject line: CS344 Project Proposal - Team-X



