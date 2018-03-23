---
layout: page
title: Working with P4 in Mininet on BMV2
---

P4.org has developed an open source software switch called BMV2 (behavioral model version 2) designed to be a target for P4 programs. That is, P4 programs can be compiled onto it to configure how it processes packets. Every P4 target supports one or more P4 target architectures. The target architecture supported by BMV2 that we will be using for these introductory exercises is called the V1Model. A diagram of the V1Model is shown below:

![V1Model]({{ site.baseurl }}/images/V1Model.png)

The V1Model consists of six P4 programmable components:
* Parser
* Checksum verification control block
* Ingress Match-Action processing control block
* Egress Match-Action processing control block
* Checksum update control block
* Deparser

P4.org has defined this target architecture in a file called [v1model.p4](https://github.com/p4lang/p4c/blob/master/p4include/v1model.p4) and added support for it to the open source P4 front end compiler called [p4c](https://github.com/p4lang/p4c). This allows p4c to compile P4 programs written for the V1Model into a json file that can be used to configure the BMV2 software switch.

P4.org has put together a set of tutorial exercises designed to incrementally introduce new features of the P4 language. For each exercise (with the exception of the P4Runtime exercise), you will write a P4 program targeting the V1Model and type `make` to compile the program and launch a Mininet network with three switches where each switch is running your P4 program. Each exercise (again, with the exception of the P4Runtime exercise) provides a set of statically configured table entries for each of the three switches so we will be focused on data plane development only. Here is the topology that we will be using:

![topo]({{ site.baseurl }}/images/mininet-topo.png)

Getting Set Up
--------------

