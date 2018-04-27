---
layout: page
title: Design Challenge Project Proposal
---

The design challenge is your opportunity to do something novel and interesting. You may propose to do a project of your own choosing, but we do encourage you to consider pursuing one of the potential projects listed below. We would like to avoid having too many groups working on the same project so the proposal will help us to gauge interest in the various topics. The proposal should be a 1-page document that includes the information listed below:

* Project title
* Problem Statement and Motivation
* Initial thoughts for system design / verification

# Potential Projects

---

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

---

#### BMv2 Support for SimpleSumeSwitch

As you saw at the beginning of the class, Mininet is a very convenient tool to use for testing out the functionality of your P4 programs. It allows you to quickly spin up an arbitrary topology of network devices running your programs without needing to compile to an FPGA or manually wire up the topology. The [behavioral model v2](https://github.com/p4lang/behavioral-model) (BMv2) is essentially a library of packet processing components that can be used to build software switches. BMv2 currently supports the simple_switch target. P4 programs that are written for the V1Model architecture can be compiled to run on the simple_switch target. The framework for integrating a BMv2 software switch into the Mininet environment already exists.

This project will consist of two components:

1. Adding support for a new BMv2 target to which P4 programs that are written for the SimpleSumeSwitch architecture can be compiled.
2. Updating the bmv2 backend of the open source [p4c](https://github.com/p4lang/p4c) compiler to support your new BMv2 target.

The end goal is to demonstrate a P4 program written for the SimpleSumeSwitch architecture running in Mininet.

---

#### P4 Performance Measurement System

The rise of P4 is bringing with it the need to verify the functionality of P4 programs and measure their performance. There is some prior work in P4 program verification, most recently:

* [p4pktgen](https://conferences.sigcomm.org/sosr/2018/sosr18-finals/sosr18-final72.pdf) is a tool that can be used to generate packets that exercise all possible paths through a P4 program (developed here at Stanford).
* [ASSERT-P4](https://conferences.sigcomm.org/sosr/2018/sosr18-finals/sosr18-final78.pdf) provides the P4 programmer with the ability to annotate their P4 program with `assert` statements, which are then verified using symbolic execution.

There has also been a little bit of prior work exploring how to measure the performance of P4 programs:

* [Whippersnapper: A P4 Language Benchmark Suite](https://conferences.sigcomm.org/sosr/2017/papers/sosr17-whippersnapper.pdf)

This project will consist of two components:

1. Design and build a performance measurement system on top of P4->NetFPGA. This system should be capable of measuring the packet processing latency through of any packet processing device (e.g. HW switch, SW switch, NPU, etc.).
2. Automate the test packet generation and DUT configuration in order to measure the latency through all possible paths of the P4 program that is used to describe the DUT's functionality. You may want to make use of the [p4pktgen](https://conferences.sigcomm.org/sosr/2018/sosr18-finals/sosr18-final72.pdf) tool to do this.

The end goal is to build a system that can automatically measure the latency of all possible paths through your router design. You may also want to extend your system to measure additional performance metrics such as throughput.

---

#### DDoS Detection Techniques

One of the key benefits enabled by programable data-planes is the increased visibility into our networks. The reason for this is because it becomes possible to develop new algorithms that see every packet and make an intelligent decision. As a result, many systems are being developed to monitor network traffic and detect suspicious behavior:

* [Sonata](https://pdfs.semanticscholar.org/7c5a/c6fa8270ef609ae0996f9e7e1246277765d8.pdf)
* [UnivMon](https://users.ece.cmu.edu/~vsekar/papers/sigcomm16_univmon.pdf)
* [Marple](http://web.mit.edu/marple/marple-sigcomm17.pdf)
* [FlowRadar](https://www.usenix.org/system/files/conference/nsdi16/nsdi16-paper-li-yuliang.pdf)

In this project you will explore data-plane techniques for detecting DDoS attacks. The DDoS attack detection problem can roughly be summarized as follows: detect when more than *K* distinct sources are sending to the same destination, see the [OpenSketch](http://stanford.edu/~lavanyaj/papers/opensketch12.pdf) paper for more details. You may want to develop some performance metrics for DDoS detection and then compare these metrics across various techniques.

---

#### Improving Congestion Control

[Timely](https://conferences.sigcomm.org/sigcomm/2015/pdf/papers/p537.pdf) is a congestion control protocol that uses very accurate RTT measurements to estimate queueing within the network and then adjust transmission rates appropriately. Programmable data-planes enable new techniques such as [In-band Network Telemtry (INT)](https://p4.org/p4/inband-network-telemetry/) which can directly provide end hosts with exact queue size measurements. INT can compliment protocols like Timely. If the source of a flow is able to quickly learn the size of the largest queue along its path it can adjust its transmission rate more accurately. This project will consist of a combination of simulation and HW implementation. You will use a network simulator such as [NS2](http://nsnam.sourceforge.net/wiki/index.php/User_Information#The_Network_Simulator_-_ns-2) to evaluate the performance benefits of using queue size measurements over traditional approaches such as TCP-Reno, DCTCP, and Timely. You will also build a hardware prototype of the switch that is required for your new congestion control algorithm.

---

#### Network Monitoring System

New telemetry techniques like [In-band Network Telemetry (INT)](https://p4.org/p4/inband-network-telemetry/) and [Packet Postcards](http://www.openvswitch.org/support/ovscon2016/7/0900-mckeown.pdf) can provide detailed information about a packet's journey through the network. For example, INT can provide the packet's exact path, the queue sizes it encountered, the delay at each switch, and more. This detailed information is great, but once we try to start collecting and processing this metadata from every single packet in our network we realize that we have a big data problem. 

The goal of this project is to develop a monitoring system that is able to efficiently present the relevant information to a network operator. The techniques that you use may be borrowed from the literature on machine learning techniques for anomaloy detection. This is primarily a software based project with little to no P4 programming.

---

#### Heavy Hitter Detection

Heavy Hitter Detection is a well studied topic in the programmable data-plane literature [[1](https://dl.acm.org/citation.cfm?id=3063772), [2](https://arxiv.org/pdf/1611.04825), [3](https://dl.acm.org/citation.cfm?id=3060606), [4](https://dl.acm.org/citation.cfm?id=3185476), [5](https://dl.acm.org/citation.cfm?id=3098832), [6](https://dl.acm.org/citation.cfm?id=3131377)]. In this project you will implement a few different techniques for performing heavy hitter detection and provide a performance comparison. You may choose to implement existing methods or develop your own.

---

#### Data Streaming Aggregation

The rise of programmable data-planes allows us to reconsider how computation is divided between end hosts and the network infrastructure. [DAIET](https://mcanini.github.io/papers/daiet.hotnets17.pdf) argues that by implementing aggregation functions in the network data-plane we can significantly reduce the amount of network traffic for MapReduce type applications. In this project you will explore the tradeoffs involved in offloading aggregation to network devices. You should build a hardware prototype on the NetFPGA and evaluate its performance. Are there other types of workloads that would benefit from in-network processing? Search? Sorting?


# The Prize

We will invite some members from the networking community to the final presentations & demonstration day. These invited guests will serve as judges along with the instructors to decide upon the best final project. The prize for the winning team will be announced at the end of the interoperability test on May 9th :) 


# Submission

Each team should email your proposal to the instructors using the subject line: CS344 Project Proposal - Team-X



