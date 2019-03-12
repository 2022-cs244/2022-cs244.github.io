---
layout: page
title: Getting Started
---

This is your first deliverable of the course. The goals are as follows: 
* Set up your P4-NetFPGA repository (each team should have one P4-NetFPGA repo)
* Set up your hardware development machine and your virtual machine
* Make sure that you have access to everything that you will need

Step 1 - Repo Access
------

Each team should send an email to sibanez@stanford.edu and stollman@stanford.edu with the github username of each teammate. Please create a github account if you do not already have one. Github will be used extensively throughout this course. Working with git is an exceptionally useful skill to have, especially if you plan to do any open source code development.

After the instructor receives your email you will be added to the [cs344-stanford-19](https://github.com/cs344-stanford-19) github organization and you should have access to the [P4-NetFPGA-CS344-19](https://github.com/cs344-stanford-19/P4-NetFPGA-CS344-19) repository. Please email the instructor if you are having trouble accessing the repository.

The instructors will send you an email after adding you to the repository, this email will contain the password that you can use to access the development machine to which your team has been assigned.

Step 2 - Development Machine Access
------

Each team will be given access to a development machine. See the [Team Assignments]({{ site.baseurl }}/teams) page to check which development machine your team has been assigned to. Each machine is running Ubuntu 14.04 and contains the following two hardware components installed on PCIe slots:
* NetFPGA SUME board
* Dual port 10G NIC

Each machine has three accounts:
* `cs344` and `cs344-2` - one account for each team member assigned to this development machine.
* `cs344-dev-test` - one additional account for teams that would like to "borrow" another team's development machine for testing purposes.

Make sure that you can sucessfully log onto your machine. Ask on the Slack channel if you run into issues.

Step 3 - Setting up your fork
------

* Create a fork of the [P4-NetFPGA-CS344-19](https://github.com/cs344-stanford-19/P4-NetFPGA-CS344-19) repo.

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
$ git remote add upstream https://github.com/cs344-stanford-19/P4-NetFPGA-CS344-19
$ git remote -v
```

You should see that you now have two remotes, `origin` and `upstream`. When working on your projects throughout the quarter, you will push changes to `origin`. If the instructors need to make a change to the starter code we will push changes to `https://github.com/cs344-stanford-19/P4-NetFPGA-CS344-19`, post an instructor note on piazza, and ask you to pull the changes from `upstream`: `$ git pull upstream master`. Please this in mind as you modify the starter code.

Step 4 - Decision Time and First Commits
------

As a team you must both work together to build your internet router. That being said, each team can decide how they would like to divide their efforts. Some teams may decide to work on everything together, others may decide that one teammate will be mainly responsible for the data-plane implementation and the other teammate will be mainly responsible for the control-plane implementation. Once you decide how to allocate responsibilities, update the README file in the `$SUME_FOLDER/contrib-projects/sume-sdnet-switch/projects/simple_router/` directory to indicate your plan of attack. Each week you will update this README file with your progress for the week and your next steps. Every Friday, instructors will review this document to track your progress. Instructors may take this opportunity to offer suggestions and/or ask probing questions. A portion of the total points is reserved for these documentation checks so it is important to keep this document organized and up-to-date.

After you have updated the README file be sure to commit the changes and push it to your remote repository before the due date of this deliverable.

Step 5 - Virtual Machine Setup
------

We will use a virtual machine throughout the quarter to develop and test P4 programs in Mininet. Here are the steps to set up the virtual machine on your laptop:

1. Install [Vagrant](https://vagrantup.com/) and [VirtualBox](https://virtualbox.org/) on your local laptop.

2. Clone `https://github.com/CS344-Stanford/tutorials/tree/si/skt/SimpleSumeSwitch` onto your laptop.

```
$ git clone -b si/skt/SimpleSumeSwitch https://github.com/CS344-Stanford/tutorials.git
```

3. `cd` into the [vm directory](https://github.com/CS344-Stanford/tutorials/tree/si/skt/SimpleSumeSwitch/vm) directory and run `$ vagrant up`. It will take about 45 minutes for the virtual machine to provision so be patient, go grab a cup of coffee :)

4. Once the previous command completes you should have a virtual machine up and running. Restart the virtual machine then you should be able to login with username `p4` and password `p4`. You can also run the command `$ vagrant ssh` from within the `vm` directory on your laptop to ssh into the VM so you don't have to use the graphical interface.

5. Clone your fork of the P4-NetFPGA repo onto the VM as the p4 user in the p4 user's home directory. Then update the p4 user's `~/.bashrc` file with the following two lines:

```
#### P4-NetFPGA #####
source ~/path/to/my-repo/tools/settings.sh
```

6. Source the `~/.bashrc` file and make sure that running the command `$ cd $SUME_FOLDER` puts you into your cloned repo. You may need to update the `SUME_FOLDER` environment variable in the `tools/settings.sh` file.

Step 6 - Access to the Lab
------

You will be working with real hardware this quarter! This means that you will get hands on experience in the lab. The lab is room 325 in the Gates computer science building. In order to access the lab you will need a key. You should be cc'ed on an email from Andi Villanueva to the Gates Key Office asking them to give you access to Gates 325. If you already have a key to the Gates building they will add room 325 to your key. If you do not already have a key then you will need to provide a $20 security deposit when you pick up your key, please bring cash. The security deposit will be refunded when you return the key so do NOT lose the key! After you have a key with access to Gates 325, be sure to initialize the key as soon as you can. Do so by inserting the key into the handle and waiting for the beep. You are encouraged to check out the development machines when you go to initialize your key, they are on the side of the lab closest to the professors' offices. The machines are labeled so you should be able to easily find your assigned machine.

Step 7 - Sign up for Team Meeting Slots
------

Teams will be required to meet with instructors and discuss their current progress and next steps. These meetings are mainly used to ensure that teams are making progress and are on the right track. Instructors will be available to meeting with teams during the scheduled lecture slots since not all lectures will be held. Each team must sign up for two meeting slots before the interoperability test and two meeting slots after for a total of 4 meetings. Please sign up for your first two meeting slots before this deliverable is due.

[Team Meeting Slots](https://github.com/cs344-stanford-19/P4-NetFPGA-CS344-19/wiki/Team-Meeting-Slots)

Step 8 - Submission
------

Please send an email to sibanez@stanford.edu and stollman@stanford.edu with a link to your team's fork of the P4-NetFPGA repository.

That's all for now!

