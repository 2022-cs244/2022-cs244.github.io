---
layout: page
title: Building an Internet Router
---

One of the main goals of this course is to design and build a fully functioning internet router. This document is meant to serve as a high level overview of the approach that we will take to do this.

# Development Tools

We will primarily use the [P4->NetFPGA Workflow](https://github.com/NetFPGA/P4-NetFPGA-public/wiki) to implement the data-plane portion of the router. This workflow attempts to abstract away many of the low level details required for hardware development. One its goals is to be usable by P4 developers with no prior HDL design experience.

The control-plane will be written in Python on top of the [Scapy](https://scapy.readthedocs.io/en/latest/) packet processing library. Scapy is a very flexible packet generator, sniffer, parser, and editor; and it is quite easy to use, making developers more productive.

P4.org has developed a software switch called behavioral model v2 (bmv2) and it can be used to implement a switch data-plane in a [Mininet](http://mininet.org/) topology. New this year, we've added support for the SimpleSumeSwitch P4 architecture to bmv2 and as a result can run our P4 programs in Mininet as well as on the NetFPGA. We suspect that you will find this tool very useful as you develop your router. See [this page]({{ site.baseurl }}/documentation/sss-bmv2) for a description of SimpleSumeSwitch support in bmv2 and how to use the environment.

# Approach

The [course schedule]({{ site.baseurl }}/schedule) provides a detailed set of deliverables. Here is an overview of the suggested design process:

* Complete [Getting Started]({{ site.baseurl }}/deliverables/getting-started) deliverable to get everything that you will need set up.
* Review the [router requirements]({{ site.baseurl }}/documentation/router-requirements) that you must implement for this class.
* Review the protocols. Consider rewatching some of the CS144 lectures if you need a refresher on the protocols listed below.
    * IP - understand how a router makes a decision about forwarding an IP packet based on its routing table
    * ARP - understand when ARP requests and replies sent / received
    * ICMP - understand the conditions under which ICMP messages are sent / received
    * [PWOSPF]({{ site.baseurl }}/documentation/pwospf)
* Read and understand the provided starter code, [here]({{ site.baseurl }}/documentation/starter-code) is a brief overview.
* Develop a static router first, make sure it is interoperable with the other teams, then develop your implementation of the PWOSPF protocol.
* Develop an interoperability plan early! As a class, you will want to decide on a concrete plan to make sure that everyone's router will end up interoperable. We strongly suggest that the teams work together to do incremental tests of their implementations against each other. For example, after implementing the PWOSPF HELLO protocol, ensure that inter-team routers can successfully perform neighbor discovery before going on to develop the link state updates. Testing components individually provides a much saner debugging environment than a fully built system.
* You will very likely want to test your router in Mininet first before testing it on hardware. Debugging in the Mininet environment is significantly easier than debugging the hardware implementation.
* Interoperate with other teams! As a class, you will need to prove to the instructors that all of your routers are in fact interoperable.
