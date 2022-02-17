---
layout: default
---

# Time and Location

**Term:** Spring 2022

**Lectures:** 
   * Monday/Wednesday 8:30AM - 9:50AM
   * Online

**Lab:** Online

# Announcements

Due to limited resources to help students carry out their design-challenge projects, we will be limiting enrollment to 18 students. As such, we ask that you fill out a short application so that we can select an appropriate mixture of student backgrounds and skill sets. Please fill out [this application](https://docs.google.com/forms/d/e/1FAIpQLSf5QfGm0Wca641Z183L6I5AHDcOFyhWXzRs0GPpNZedXFgSLg/viewform) **before March 29th Monday at 11:59PM** (end of first day of class). We will review the submissions and notify everyone of the selection results on March 30th by 5PM.

# Overview

High-performance network system design. Students will work in teams of two to build  a fully functioning Internet/data-center router. Students will design the control plane in Python on a linux host and will design the data plane in the new P4 language on a high-speed programmable switching ASIC (Intel Tofino). For the midterm milestone, teams must demonstrate that their routers can interoperate with the other teams by building a small topology utilizing everyone's router. In the final 4 weeks of the class, teams will participate in an open-ended design challenge. Prerequisites: At least one student in each team must have taken CS144 at Stanford and completed Lab 3 (static router).

# Teams

The class will be broken down into teams of two students. We leave it up to each team to decide how to they would like to divide up the workload amongst themselves. However, we highly encourge close collaboration and consultation so that each member is intimiately familiar with all aspects of the router implementation.

# Class Router Interoperation

Routers by nature work cooperatively in large complex environments. In fact, much of the complexity in router design and implementation is inter-operating with routers developed by different teams based on varying assumptions of standard protocol specifications. Inter-operation is such a critical feature of network infrastructure development that it is one of the major focuses of this course. For the midterm milestone, teams must demonstrate interoperability of thier router with all other teams' routers. The students are responsible for initiating communication between groups, coming up with a cooperative integration plan and ensuring that your routers inter-operate with all other routers in the class. It is our goal that every finished router will be able to route traffic cooperatively on a large shared topology built with Mininet.

We have reserved a portion of the total class points to allocate based on participation during inter-operation. This means that we expect all the students to be pro-active from the start about planning and communicating a solid inter-operation strategy between teams during development. It is a good idea to collectively map out a strategy early on in the quarter and have incremental goals that can be tested piece-wise. You may meet during designated course hours (since not all lectures are held) or use the class Slack channel for communication.

# Documentation and Deliverables

This is a project based course. There is no midterm or final exam. There is a set of deliverables specified on the [course schedule]({{ site.baseurl }}/schedule). These deliverables are meant to function as milestones for the two main tasks of the quarter: (1) building an internet router, (2) your advanced features project. We will be using github extensively throughout the course. Each team will fork the starter code from a GitHub repository and will add the instructors as collaborators on their forks. Teams will "submit" their deliverables by adding a tag to a specific commit, this will allow instructors to evaluate their work easily and efficiently, and it's also good code-development practice.

In addition to the deliverables specified in the source schedule, teams are also asked to maintain a design document as a README file in their project directory. Teams will use this document to record their progress each week along with their next steps. Every Friday, instructors will review this design document to ensure teams are on track and making good progress. A portion of the total points is reserved for these documentation checks so it's important to keep the README file organized and up-to-date.

Each team will give a 15 min presentation / demonstration at the end of the course explaining their advanced features project.


