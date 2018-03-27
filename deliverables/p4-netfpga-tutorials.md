---
layout: page
title: P4->NetFPGA Tutorial Assignments
---

These exercises are meant to give you experience working with the P4->NetFPGA workflow. [Here](https://github.com/NetFPGA/P4-NetFPGA-public/wiki) is the P4->NetFPGA wiki home page. Your first task is to review the [Workflow Overview](https://github.com/NetFPGA/P4-NetFPGA-public/wiki/Workflow-Overview) page. This page contains most of the documentation that you will need when working with the P4->NetFPGA tools. One caveat is that we will be using a version on Xilinx SDNet that has not been officially released yet and because of this the P4->NetFPGA Workflow Overview wiki page does not accurately describe the latest version of the SimpleSumeSwitch target architecture that we will be using for this class. Please instead refer to this [updated documentation]() of the SimpleSumeSwitch architecture.

The P4->NetFPGA workflow is built on top of the Xilinx P4-SDNet compiler. This compiler extends the open source [p4c](https://github.com/p4lang/p4c) front end compiler to generate HDL modules for Xilinx FPGAs. Eventually, all P4 features will be supported, but for now there are some that are not. Please refer to the [SDNet P4 Support]() page for a breakdown of the features that are supported/unsupported. I should also mention that these tools should be considered alpha quality research code. Throughout the quarter you may run into bugs. If you believe you have found a bug, first post a question on piazza. If the instructor confirms that it is indeed a bug, they may ask you to document the bug on [this public wiki page]() so that others are aware of its existence.

Tutorial Assignments
--------------------

The [P4->NetFPGA Tutorials](https://github.com/NetFPGA/P4-NetFPGA-public/wiki/Tutorial-Assignments) page describes three exercises:

* Switch Calculator
* TCP Monitor
* In-band Network Telemetry (INT)

The starter code for these exercises is already in the repository that you set up on your development machine in the [Getting Started]({{ site.baseurl }}/deliverables/getting-started) deliverable. This is where you should complete these exercises.

Each exercise has some starter code marked with `TODO` comments. Your job is to complete the implementation in the starter code and ensure that all of the simulation testcases are passing. You DO NOT need to compile the bitstream for ALL assignments, but you DO need to compile the bitstream for at least ONE assignment. We will let you decide which assignment to test out in hardware :) So to be clear, you need to perform up to step 9 indicated in the Switch Calculator assignment for ALL exercises. 

Submission
----------

When you are ready to submit, commit all of your changes to the source files and follow the steps below to add a tag to the commit you would like the instructors to review. You should NOT add any generated files including your bitstream to your repository. Instead, please email your bitstream to sibanez@stanford.edu along with a link to your github repository.

```
$ git tag -a tutorials-submission -m "Submission of my P4->NetFPGA Tutorial Assignments"
$ git push origin tutorials-submission
```

After the assignment deadline, instructors will checkout the commit to which the `tutorials-submission` tag points and verify that the simulations are passing. They will also verify that your provided bitstream is functioning properly.
