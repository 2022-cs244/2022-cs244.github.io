---
layout: page
title: Building an Internet Router
---

One of the main goals of this course is to design and build a fully functioning internet router. This document is meant to serve as a high level overview of approach that we will take to do this.

# Tools

We will use the [P4->NetFPGA Workflow](https://github.com/NetFPGA/P4-NetFPGA-public/wiki) to implement the data-plane portion of the router. This workflow attempts to abstract away many of the low level details required for hardware development. The goal is for it to be usable by P4 developers with no HDL design experience.

The control-plane will be written in Python on top of the [Scapy](https://scapy.readthedocs.io/en/latest/) packet processing library. Scapy is a very flexible packet generator, sniffer, parser, and editor; and it is quite easy to use, making developers more productive.

# Approach

Complete [Getting Started]({{ site.baseurl }}/deliverables/getting-started)


# Hints
