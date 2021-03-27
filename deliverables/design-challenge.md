---
layout: page
title: Design Challenge Project Proposal
---

The design challenge is your opportunity to do something novel and interesting. You may propose to do a project of your own choosing, but we do encourage you to consider pursuing one of the potential projects listed below. We would like to avoid having too many groups working on the same project so the proposal will help us to gauge interest in the various topics. The proposal should be a 1-page document that includes the information listed below:

* Project title
* Problem Statement and Motivation
* Initial thoughts for system design and final demonstration

The project suggestions listed below are inspired by an on-going research effort to change the data-plane programming model from one that is purely packet driven to one that is more generally event-driven. The key insight is that many data-plane algorithms need to maintain state that must be accessed and updated potentially multiple times and sometimes independently of packets arriving or departing. 

You're required to implement and test your ideas using BMv2 and Mininet. If needed, you may have to extend BMv2, Mininet, p4app, or even p4c to realize your ideas. Although it's not mandatory, if you implement and test your ideas using the Tofino ASIC model as well, you may be able to receive extra credits. In such a case, please set the right expectation for yourselves because, although Tofino and the associated tools are much more powerful than BMv2, etc., the ASIC model is not suitable for testing use cases that require handling packets at high speed or running multiple ASIC models in parallel.

# Potential Projects

### Microburst Detection

* [Snappy paper](https://www.cs.princeton.edu/~jrex/papers/snappy18.pdf)
* How would you improve microburst detection when using an event-driven architecture?

### Fast-Reroute

* [FRR paper](https://www.net.t-labs.tu-berlin.de/~stefan/neat18.pdf)
* How would you implement fast re-route using an event-driven architecture?

### Load Balancing

* [HULA paper](https://conferences.sigcomm.org/sosr/2016/papers/sosr_paper67.pdf)
* How would you improve HULA using an event-driven architecture?

### Network Monitoring

* [Network Monitoring Lecture](https://cs344-stanford.github.io/lectures/Lecture-4-Chang-Kim-BFN.pdf)
* [Marple paper](http://web.mit.edu/marple/marple-sigcomm17.pdf)
* [Sonata paper](https://arxiv.org/pdf/1705.01049.pdf)
* What sorts of interesting network monitoring techniques can you develop using an event-driven architecture?
  * E.g. Generating an INT report whenever:
	  * Number of active flows exceeds some threshold
	  * Per-flow packet drop rate exceeds threshold
	* New sketch techniques

### Active Queue Management (AQM)

* [P4 TM SubWG AQM Google Doc](https://drive.google.com/open?id=15-e15lsVHrZAFA7jbMgNTOto5dC-iclsjDqtKSH49yA)
* [P4 TM SubWG Meeting 4](https://drive.google.com/open?id=1gH3Cwi5eJeYVncNl_y9-bdQbTXzAIjwo)
* [P4 TM SubWG Meeting 5](https://drive.google.com/open?id=1nMZiW6bLlQ-Rk-pjwN5CGemTQdkM6djZ)
* The ability to derive congestion signals naturally facilitates the implementation of AQM algorithms.
* Pick a few AQM policies, then implement and evaluate them on the NetFPGA.

### P4 on Raspberry Pi

* [p4pi (link to come)](https://github.com/p4lang/p4pi)
* Software router running on the [Raspberry Pi 4](https://www.raspberrypi.org/products/raspberry-pi-4-model-b/?variant=raspberry-pi-4-model-b-4gb).
* Develop the tools and infrastructure for prototyping P4 programs on the RPI.
* What functionality would be useful for a home router? E.g., parental controls, firewall, monitoring network usage (time spent on different applications).

### P4 Externs

* [P4 extern objects and functions](https://p4.org/p4-spec/docs/P4-16-v1.2.1.html#sec-external-units)
* What functionality is missing from the BMv2 SimpleSwitch pipeline?
* What useful features could be implemented as externs? E.g., packet encryption, persistent storage.

# Submission

Each team should email your proposal to the instructors using the subject line: CS344 Project Proposal - Team-X



