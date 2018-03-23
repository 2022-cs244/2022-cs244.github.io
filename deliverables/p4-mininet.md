---
layout: page
title: Working with P4 in Mininet on BMV2
---

P4.org has developed an open source software switch called BMV2 (behavioral model version 2) designed to be a target for P4 programs. That is, P4 programs can be compiled onto it to configure how it processes packets. Every P4 target supports one or more P4 target architectures. The target architecture supported by BMV2 that we will be using for these exercises is called the V1Model. A diagram of the V1Model is shown below:

![V1Model]({{ site.baseurl }}/images/V1Model.png)

The V1Model consists of six P4 programmable components:
* Parser
* Checksum verification control block
* Ingress Match-Action processing control block
* Egress Match-Action processing control block
* Checksum update control block
* Deparser

