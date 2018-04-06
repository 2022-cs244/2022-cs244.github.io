---
layout: page
title: Getting Started
---

This is your first deliverable of the course. The goals are as follows: 
* Set up the repository that you will be using for the rest of the quarter on your assigned development machine
* Make sure that you have access to everything that you will need

This assignment is to be completed as a team. That is, each team will only have one repository.

Step 1 - Repo Access
------

Each team should send an email to sibanez@stanford.edu with the github username of each teammate. Please create a github account if you do not already have one. Github will be used extensively throughout this course. Working with git is an exceptionally useful skill to have, especially if you plan to do any open source code development.

After the instructor receives your email you will be added to the [CS344-Stanford-18](https://github.com/CS344-Stanford-18) github organization and you should have access to the [P4-NetFPGA-CS344-18](https://github.com/CS344-Stanford-18/P4-NetFPGA-CS344-18) repository. Please email the instructor if you are having trouble accessing the repository.

The instructor will send you an email after adding you to the repository, this email will contain the password that you can use to access the development machine to which you have been assigned. Feel free to change your password once you log on.

Step 2 - Development Machine Access
------

Each team will be given access to a development machine. See the [Team Assignments]({{ site.baseurl }}/teams) page to check which development machine your team has been assigned to. Each machine is running Ubuntu 14.04 and contains the following two hardware components installed on PCIe slots:
* NetFPGA SUME board
* Dual port 10G NIC

Each machine has three accounts:
* `cs344` and `cs344-2` - one account for each team member assigned to this development machine.
* `cs344-dev-test` - one additional account for teams that would like to "borrow" another team's development machine for testing purposes.

Make sure that you can sucessfully log onto your machine. Ask on piazza if you run into issues.

Step 3 - Setting up your fork
------

* Create a fork of the [P4-NetFPGA-CS344-18](https://github.com/CS344-Stanford-18/P4-NetFPGA-CS344-18) repo.

You may fork the repo into a personal github account or you may create a new github organization for the team and fork the repo there. If you don't know how to create a fork, [here is brief guide](https://guides.github.com/activities/forking/).

* The instructors will need access to your repositories so please add Sarah Tollman (github username: `sktollman`) as a collaborator on your fork.

* Once you have created your fork, clone the repository onto your development machine:

```
$ git clone https://github.com/<username>/<repo-name>.git
```

* Update the `tools/settings.sh` file so that `SUME_FOLDER` points to the installation location of the repo.

* Add the following two lines to your `~/.bashrc` file (updating the path appropriately):

```
#### P4-NetFPGA #####
source ~/path/to/my-repo/tools/settings.sh
```

* Log out and log back in, then make sure that running `$ cd $SUME_FOLDER` puts you into your cloned repo. The development machines already have all of the required dependencies installed, so there's not too much more to set up.

* Build the SUME hardware library cores and some software to access registers:

```
$ cd $SUME_FOLDER/lib/hw/xilinx/cores/tcam_v1_1_0/ && make update && make

$ cd $SUME_FOLDER/lib/hw/xilinx/cores/cam_v1_1_0/ && make update && make

$ cd $SUME_SDNET/sw/sume && make

$ cd $SUME_FOLDER && make
```

You will only need to run these commands once unless you (or the instrucors) make changes to one of the modules in the `$SUME_FOLDER/lib` folder.

* Build and load the SUME drivers:

```
$ sudo bash
# cd $DRIVER_FOLDER
# make all
# make install
# modprobe sume_riffa
# lsmod | grep sume_riffa
```

* Point your local clone to the github repo that you originally forked:

```
$ cd $SUME_FOLDER
$ git remote add upstream https://github.com/CS344-Stanford-18/P4-NetFPGA-CS344-18.git
$ git remote -v
```

You should see that you now have two remotes, `origin` and `upstream`. When working on your projects throughout the quarter, you will push changes to `origin`. If the instructors need to make a change to the starter code we will push changes to `https://github.com/CS344-Stanford-18/P4-NetFPGA-CS344-18.git`, post an instructor note on piazza, and ask you to pull the changes from `upstream`: `$ git pull upstream master`. Please this in mind as you modify the starter code.

Step 4 - Decision Time and First Commits
------

As a team you must both work together to build your internet router. That being said, one team member will be mainly responsible for the P4 data plane implementation and the other team member will be mainly responsible for the Python control plane implementation. Once you decide how to allocate responsibilities update the README file in the `$SUME_FOLDER/contrib-projects/sume-sdnet-switch/projects/simple_router/` directory to indicate who is responsible for what. Throughout the quarter you MUST keep this README file up to date with descriptions of your router design and explain your various design choices. Consider including diagrams, pseudocode, flow charts, or whatever else you think would be helpful to explain your design to the instructors. Every Friday instructors will review this design document to ensure you are keeping it up to date and to ensure you are on the correct track. Instructors may take this opportunity to offer suggestions and/or ask probing questions. A portion of the total points is reserved for these documentation checks so it is important to keep this document clear and organized.

After you have updated the README file be sure to commit the changes and push it to your remote repository before the due date of this deliverable.


Step 5 - Access to the Lab
------

You will be working with real hardware this quarter! This means that you will get hands on experience in the lab. The lab is room 325 in the Gates computer science building. In order to access the lab you will need a key. You should be cc'ed on an email from Lancy Nazaroff to the Gates Key Office asking them to give you access to Gates 325. If you already have a key to the Gates building they will add room 325 to your key. If you do not already have a key then you will need to provide a $20 security deposit when you pick up your key, please bring cash. The security deposit will be refunded when you return the key so do NOT lose the key! After you have a key with access to Gates 325, be sure to initialize the key as soon as you can. Do so by inserting the key into the handle and waiting for the beep. You are encouraged to check out the development machines when you go to initialize your key, they are on the side of the lab closest to the professors' offices. The machines are labeled so you should be able to easily find your assigned machine.

Step 6 - Sign up for Team Meeting Slots
------

Teams will be required to meet with instructors and discuss their current progress and next steps. These meetings are mainly used to ensure that teams are making progress and are on the right track. Instructors will be available to meeting with teams during the scheduled lecture slots since not all lectures will be held. Each team must sign up for two meeting slots before the interoperability test and two meeting slots after for a total of 4 meetings. Please sign up for your first two meeting slots before this deliverable is due.

[Team Meeting Slots](https://github.com/CS344-Stanford-18/P4-NetFPGA-CS344-18/wiki/Team-Meeting-Slots)

That's all for now!

