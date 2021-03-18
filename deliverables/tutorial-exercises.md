---
layout: page
title: P4 Tutorial and MAC Learning Exercise
---

The goal of the P4 tutorial and the MAC learning exercise is to allow you to become familiar with the following development tools that you will be using to build your router:
* The P4 compiler
* BMv2 in Mininet
* p4app

Here is a bit of information about each of these tools.

## P4 Compiler

To run P4 code, it has to be compiled for the target (e.g. hardware switch, NIC, software switch). Each target has a different P4 compiler backend. In the first part of this course we will be using the [P4 reference compiler](https://github.com/p4lang/p4c) for BMv2.


## BMv2 in Mininet

P4.org has developed an open source software switch called BMv2 (behavioral model version 2) designed to be a target for P4 programs. That is, P4 programs can be compiled onto it to configure how it processes packets. Every P4 target supports one or more P4 target architectures. BMv2 was initially designed with support for the so called V1Model architecture.

## p4app

This tool provides a portable way of packaging and running P4 code and control planes with BMv2 and Mininet. Inside a p4app package (simply referred to as a "p4app"), there is a `main.py` entry point. This defines the topology and the P4 program for each switch, and runs a workload on the network by executing commands on the hosts. The p4app runs inside a Docker container that has all the dependencies and tools (P4 compiler, BMv2, Mininet, scapy), so they don't have to be installed directly on the host machine (or VM).

Prerequisites
-------------

Make sure that you have completed the [Getting Started]({{ site.baseurl }}/deliverables/getting-started) deliverable where you set up your environment. If you have problems installing the dependencies directly on your computer, you can use the virtual machine, which has all of the necessary dependencies installed on it to work with p4app (i.e. Docker).

P4 Tutorial
-------------

There are two main [P4 tutorial](https://github.com/2021-cs344/tutorials/) exercises for you to complete: basic forwarding and basic tunneling. In the first exercise, you will implement a very basic IPv4 router. In the second exercise you will extend the basic forwarding with support for a basic tunneling protocol.

### How to run the P4 tutorial exercises

Start by cloning the P4 tutorials repository:
```
git clone --recursive https://github.com/2021-cs344/tutorials/
```

Since we are using p4app, you should use the p4app versions of the exercises in `tutorials/p4app-exercises/`. Each exercise is self contained and includes detailed step-by-step instructions in the READMEs. We strongly encourage you to complete both of the tutorial exercises before attempting the MAC learning exercise.


MAC Learning Exercise
---------------------

When a host wants to send a packet to an IP address, it first has to resolve the MAC address associated with that IP address. This is done with the [Address Resolution Procotol (ARP)](https://en.wikipedia.org/wiki/Address_Resolution_Protocol). The host sends an ARP packet requesting the MAC address for a given IP. Typically, the switch broadcasts this requests to all hosts. When a host receives an ARP request for its IP address, the host replies with an ARP response containing its MAC address.

With MAC learning, the switch learns about hosts by monitoring ARP packets. It uses this information for two purposes: 1) associating MAC addresses with switch ports, in order to perform L2 forwarding; and 2) to populate an ARP cache table, which can be used to respond to ARP requests directly, without broadcasting the request to all ports.

In this exercise you will implement the data plane and control plane components of a MAC learning switch. You can find more detailed instructions in README of the [exercise repository](https://github.com/2021-cs344/maclearning-exercise) and `TODO`s in the starter code.

### Submission

You should create a _private_ fork of the [exercise repository](https://github.com/2021-cs344/maclearning-exercise). When you finish the exercise, tag the commit with your solution. You should then send an e-mail to all the [course instructors]({{ site.baseurl }}/staff) with a link to your private fork, along with the tag of your solution.
