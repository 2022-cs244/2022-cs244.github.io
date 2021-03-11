---
layout: page
title: Getting Started
---

Step 1 - Repo Access
------

Each team should send an email to the all the [course instructors]({{ site.baseurl }}/staff) with the github username of each teammate. Please create a github account if you do not already have one. Github will be used extensively throughout this course. Working with git is an exceptionally useful skill to have, especially if you plan to do any open source code development.

After the instructor receives your email you will be added to the [XXX TODO cs344-stanford-2021](https://github.com/cs344-stanford-19) github organization and you should have access to the [P4-NetFPGA-CS344-19](https://github.com/cs344-stanford-19/P4-NetFPGA-CS344-19) repository. Please email the instructor if you are having trouble accessing the repository.

The instructors will send you an email after adding you to the repository, this email will contain the password that you can use to access the development machine to which your team has been assigned.

Step 2 - Development Environment Setup
------

You will use the [P4 language](http://p4.org) to implement the data plane of
your internet router. Note that there are two versions of the language, P4\_14
and P4\_16. For this course we will use P4\_16. You should familiarize yourself
with the [P4_16 specification](https://p4.org/p4-spec/docs/P4-16-v1.1.0-spec.html).
You should implement the control plane with Python, and use
[P4Runtime](https://p4.org/p4-runtime/) to communicate with the switch.


## Tools

* [P4C](https://github.com/p4lang/p4c) is the reference compiler for the P4
  language.
* [BMV2](https://github.com/p4lang/behavioral-model) is a software switch that
  runs P4 programs compiled with P4C.
* [Mininet](http://mininet.org/overview/) creates a virtual network running
  software switches and real user-space applications.
* [Scapy](https://scapy.readthedocs.io/en/latest/introduction.html) is a Python
  library for crafting and decoding raw packets. It also has utilities for
  sniffing and sending packets.
* [p4app](https://github.com/p4lang/p4app/tree/rc-2.0.0) is a tool for running
  P4 programs on a Mininet topology. It includes all the dependencies for
  compiling, running and testing your programs: P4C, BMV2, Mininet and Scapy.


## How to run p4app on Mac OSX:

* **Install [Vagrant](https://www.vagrantup.com) and [VirtualBox](https://www.virtualbox.org/):**


* **Install homebrew:**

```
xcode-select --install
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```


* **Install docker, docker-toolbox, and docker-machine:**

```
brew install --cask docker
brew install docker-toolbox
brew install docker-machine docker
```

* **Install git:**

```
brew install git
```

* **Clone p4app github repo:**

```
git clone --branch rc-2.0.0 https://github.com/p4lang/p4app.git
```


* **Make p4app command available:**

```
ln -s <PATH_TO_P4APP_REPO>/p4app/p4app /usr/local/bin/p4app
```

* **Launch docker quickstart terminal:**

```
open -a Docker\ Quickstart\ Terminal -j
```

* **Run program through p4app:**

```
p4app run <PROG_NAME>.p4app/
```

* **For example, run `wire.p4app`:**


```
p4app run <PATH_TO_P4APP_REPO>/p4app/examples/wire.p4app
```


## Writing P4 Programs

We use Vim to edit `.p4` files, but you can use any text editor. Here are some
syntax highlighters for popular editors:

* [Vim](https://github.com/p4lang/tutorials/blob/master/vm/p4.vim)
* [Emacs](https://github.com/p4lang/tutorials/blob/master/vm/p4_16-mode.el)
* [Atom](https://atom.io/packages/language-p4)
* [Sublime](https://github.com/c3m3gyanesh/p4-syntax-highlighter)

Step 3 - Setting up your fork
------

* Create a fork of the [P4-NetFPGA-CS344-19](https://github.com/cs344-stanford-19/P4-NetFPGA-CS344-19) repo.

You may fork the repo into a personal github account or you may create a new github organization for the team and fork the repo there. If you don't know how to create a fork, [here is brief guide](https://guides.github.com/activities/forking/).

* The instructors will need access to your repositories so please add Sarah Tollman (github username: `sktollman`) as a collaborator on your fork.

* Once you have created your fork, clone the repository onto your development machine:

```
$ git clone https://github.com/<username>/<repo-name>.git
```

Step 4 - Decision Time and First Commits
------

As a team you must both work together to build your internet router. That being said, each team can decide how they would like to divide their efforts. Some teams may decide to work on everything together, others may decide that one teammate will be mainly responsible for the data-plane implementation and the other teammate will be mainly responsible for the control-plane implementation. Once you decide how to allocate responsibilities, update the README file in the `$SUME_FOLDER/contrib-projects/sume-sdnet-switch/projects/simple_router/` directory to indicate your plan of attack. Each week you will update this README file with your progress for the week and your next steps. Every Friday, instructors will review this document to track your progress. Instructors may take this opportunity to offer suggestions and/or ask probing questions. A portion of the total points is reserved for these documentation checks so it is important to keep this document organized and up-to-date.

After you have updated the README file be sure to commit the changes and push it to your remote repository before the due date of this deliverable.

Step 5 - *TODO* Virtual Machine Setup
------

We will use a virtual machine throughout the quarter to develop and test P4 programs in Mininet. Here are the steps to set up the virtual machine on your laptop:

1. Install [Vagrant](https://vagrantup.com/) and [VirtualBox](https://virtualbox.org/) on your local laptop.

2. Clone `https://github.com/CS344-Stanford/tutorials/tree/si/skt/SimpleSumeSwitch` onto your laptop.

```
$ git clone -b si/skt/SimpleSumeSwitch https://github.com/CS344-Stanford/tutorials.git
```

3. `cd` into the [vm directory](https://github.com/CS344-Stanford/tutorials/tree/si/skt/SimpleSumeSwitch/vm) directory and run `$ vagrant up`. It will take about 45 minutes for the virtual machine to provision so be patient, go grab a cup of coffee :)

4. Once the previous command completes you should have a virtual machine up and running. Restart the virtual machine then you should be able to login with username `p4` and password `p4`. You can also run the command `$ ssh -p 2222 p4@127.0.0.1` from laptop to ssh into the VM so you don't have to use the graphical interface.

5. Clone your fork of the P4-NetFPGA repo onto the VM as the p4 user in the p4 user's home directory. Then update the p4 user's `~/.bashrc` file with the following two lines:

```
#### P4-NetFPGA #####
source ~/P4-NetFPGA-CS344-19/tools/settings.sh
```

6. Source the `~/.bashrc` file and make sure that running the command `$ cd $SUME_FOLDER` puts you into your cloned repo. You may need to update the `SUME_FOLDER` environment variable in the `tools/settings.sh` file.

Step 6 - Sign up for Team Meeting Slots
------

Teams will be required to meet with instructors and discuss their current progress and next steps. These meetings are mainly used to ensure that teams are making progress and are on the right track. Instructors will be available to meeting with teams during the scheduled lecture slots since not all lectures will be held. Each team must sign up for two meeting slots before the interoperability test and two meeting slots after for a total of 4 meetings. Please sign up for your first two meeting slots before this deliverable is due.

[Team Meeting Slots](https://github.com/cs344-stanford-19/P4-NetFPGA-CS344-19/wiki/Team-Meeting-Slots)

Step 7 - Review Documentation and Schedule
------

Read over the [documentation page]({{ site.baseurl }}/documentation) and [course schedule]({{ site.baseurl }}/schedule) on the  website to familiarize yourself with the information that is available to you.

Step 8 - Submission
------

Please send an email to all [course instructors]({{ site.baseurl }}/staff) with a link to your team's fork of the starter code repository.

That's all for now!
