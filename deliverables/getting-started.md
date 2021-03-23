---
layout: page
title: Getting Started
---

Step 1 - Repo Access
------

Each student should send an email to the all the [course instructors]({{ site.baseurl }}/staff) with his/her GitHub username. Please create a GitHub account if you do not already have one. GitHub will be used extensively throughout this course. Working with git is an exceptionally useful skill to have, especially if you plan to do any open source code development.

After the instructor receives your email you will be added to the [2021-cs344](https://github.com/2021-cs344) GitHub organization and you should have access to the [2021-cs344/2021-cs344-project](https://github.com/2021-cs344/2021-cs344-project) repository. Please email the instructor if you are having trouble accessing the repository.

Step 2 - Development Environment Familiarization
------

You will use the [P4 language](http://p4.org) to implement the data plane of your internet router. Note that there are two versions of the language, P4\_14 and P4\_16. For this course we will use P4\_16. You should familiarize yourself with the [P4_16 specification](https://p4.org/p4-spec/docs/P4-16-v1.2.1.html). For the control plane, you will use Python and [P4Runtime](https://p4.org/p4-runtime/) to communicate with the switch.


### Tools

* [P4C](https://github.com/p4lang/p4c) is the reference compiler for the P4
  language.
* [BMv2](https://github.com/p4lang/behavioral-model) is a software switch that
  runs P4 programs compiled with P4C.
* [Mininet](http://mininet.org/overview/) creates a virtual network running
  software switches and real user-space applications.
* [Scapy](https://scapy.readthedocs.io/en/latest/introduction.html) is a Python
  library for crafting and decoding raw packets. It also has utilities for
  sniffing and sending packets.
* [p4app](https://github.com/p4lang/p4app/tree/rc-2.0.0) is a tool for running
  P4 programs on a Mininet topology. It includes all the dependencies for
  compiling, running and testing your programs: P4C, BMv2, Mininet and Scapy.


### Writing P4 Programs

We use Vim to edit `.p4` files, but you can use any text editor. Here are some
syntax highlighters for popular editors:

* [Vim](https://github.com/p4lang/tutorials/blob/master/vm/p4.vim)
* [Emacs](https://github.com/p4lang/tutorials/blob/master/vm/p4_16-mode.el)
* [Atom](https://atom.io/packages/language-p4)
* [Sublime](https://github.com/c3m3gyanesh/p4-syntax-highlighter)

Step 3 - Virtual Machine Setup
------

For the first part of the course you will be using the open-source P4 environment (i.e. p4app) described above. While these tools can run on any Unix system with Docker, we suggest you use the Ubuntu VM we created for this course. In any case, you will need this VM later on in the course for the P4 hardware (Tofino) development enivornment.

Here are the steps to set up the virtual machine on your laptop:

1. Install [VirtualBox](https://virtualbox.org/) on your local laptop.

2. Download the VM image (the link will be shared by e-mail).

3. Open VirtualBox and click "New". Choose a name for your VM (e.g. "cs344"), type (Linux) and version (Ubuntu 64-bit). You should allocate at least 16GB of memory. When prompted for the hard disk, select "Use an existing hard disk file" and select the VM image you downloaded.

4. After the the VM boots, login with username `p4dev`.

5. Install Docker following [these instructions](https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-on-ubuntu-18-04). After installing Docker, reboot the VM.

6. Clone the p4app repository. Open a terminal in the VM and run:
```
cd ~
git clone https://github.com/2021-cs344/p4app.git
```

7. Test that p4app works by running an example:
```
~/p4app/p4app run ~/p4app/examples/basic.p4app
```

Step 4 - Setting Up Your Fork (First Assignment)
------

* Create a *private* fork of the [2021-cs344/maclearning-exercise](https://github.com/2021-cs344/maclearning-exercise) repo.

If you don't know how to create a *private* fork, [here is brief guide](https://guides.github.com/activities/forking/).

* The instructors will need access to your repositories so please add them (using [their GitHub usernames]({{ site.baseurl }}/staff)) as a collaborators on your fork.

* Once you have created your fork, clone the repository onto your development machine/VM:

```
$ git clone https://github.com/<username>/<repo-name>.git
```

You should now be ready to start working on the [first assignment]({{ site.baseurl }}/tutorial-exercises).

Step 5 - Setting Up Your Fork (Team Project)
------

Before you follow the remaining steps, you should form a team. Each team should create a single fork.

* Create a *private* fork of the [2021-cs344/2021-cs344-project](https://github.com/2021-cs344/2021-cs344-project) repo.

You may fork the repo into a personal GitHub account or you may create a new GitHub organization for the team and fork the repo there.

* The instructors will need access to your repositories so please add them (using [their GitHub usernames]({{ site.baseurl }}/staff)) as a collaborators on your fork.

* Once you have created your fork, clone the repository onto your development machine:

```
$ git clone https://github.com/<username>/<repo-name>.git
```

Step 6 - Decision Time and First Commits
------

As a team you must both work together to build your internet router. That being said, each team can decide how they would like to divide their efforts. Some teams may decide to work on everything together, others may decide that one teammate will be mainly responsible for the data-plane implementation and the other teammate will be mainly responsible for the control-plane implementation. Once you decide how to allocate responsibilities, update the README file in the root directory of the repo to indicate your plan of attack. Each week you will update this README file with your progress for the week and your next steps. Every Friday, instructors will review this document to track your progress. Instructors may take this opportunity to offer suggestions and/or ask probing questions. A portion of the total points is reserved for these documentation checks so it is important to keep this document organized and up-to-date.

After you have updated the README file be sure to commit the changes and push it to your remote repository before the due date of this deliverable.


Step 7 - Sign up for Team Meeting Slots
------

Teams will be required to meet with instructors and discuss their current progress and next steps. These meetings are mainly used to ensure that teams are making progress and are on the right track. Instructors will be available to meeting with teams during the scheduled lecture slots since not all lectures will be held. Each team must sign up for two meeting slots before the interoperability test and two meeting slots after for a total of 4 meetings. Please sign up for your first two meeting slots before this deliverable is due.

[XXX TODO Team Meeting Slots](https://github.com/cs344-stanford-19/P4-NetFPGA-CS344-19/wiki/Team-Meeting-Slots)

Step 8 - Review Documentation and Schedule
------

Read over the [documentation page]({{ site.baseurl }}/documentation) and [course schedule]({{ site.baseurl }}/schedule) on the  website to familiarize yourself with the information that is available to you.

Step 9 - Submission
------

Please send an email to all [course instructors]({{ site.baseurl }}/staff) with a link to your team's fork of the starter code repository.

That's all for now!
