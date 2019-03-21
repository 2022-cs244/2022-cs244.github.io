---
layout: page
title: Static Router Functionality
---

The goal of this deliverable is to ensure that you have implemented all of the required functionality of a static IPv4 router. To help get you started, we have provided some baseline data-plane and control-plane tests. These tests test *some* of the required functionality of your router so you will want to add more of your own. Please do not modify the provided baseline tests without instructor approval.

The baseline tests use the following test topology defined in `$P4_PROJECT_DIR/sw/simple_router_sw/simulation/test_topology.py`.

```
               ##################
               eh0 - ip: 10.6.3.2
               ##################
                       |
                       |
                iface3:10.6.3.3   iface2:
             #################### 10.6.2.3        ##################
             self - rid: 10.6.0.3 --------------- r2 - rid: 10.2.0.3
             ####################        10.6.2.2 ##################
     iface1:10.6.1.3     iface0:10.6.0.3      10.2.0.3
            /                     \               /
           /                       \             /
     10.6.1.2                    10.6.0.2    10.2.0.2
##################                ##################
r1 - rid: 10.1.0.3                r0 - rid: 10.0.0.3
##################                ##################
       10.1.0.3                  10.0.0.3
           \                       /
            \                     /
           10.1.0.2          10.0.0.2
               ################## 10.3.1.3      #########################
               r3 - rid: 10.3.0.3 ------------- default route to internet
               ##################     0.0.0.0/0 #########################
                    10.3.0.3
                       |
                       |
                    10.3.0.2
              ################## 10.4.0.3        ########
              r4 - rid: 10.4.0.3 --------------- firewall
              ##################     10.4.0.0/16 ########
```

# Data-Plane Baseline Tests

The data-plane baseline tests are located in the simple_router's `gen_testdata.py` script. Each test is defined by an input packet + metadata and an expected output packet + metadata. See the `gen_testdata.py` script for a short description of the functionality that each test is intended to exercise.

In order to run the tests, your `commands.txt` file should reflect the following topology:
```
               ##################
               eh0 - ip: 10.6.3.2
               ##################
                       |
                       |
                iface3:10.6.3.3   iface2:
             #################### 10.6.2.3        ##################
             self - rid: 10.6.0.3 --------------- r2 - rid: 10.2.0.3
             ####################        10.6.2.2 ##################
     iface1:10.6.1.3     iface0:10.6.0.3      10.2.0.3
            /                     \               /
           /                       \             /
     10.6.1.2                    10.6.0.2    10.2.0.2
##################                ##################
r1 - rid: 10.1.0.3                r0 - rid: 10.0.0.3
##################                ##################
       10.1.0.3                  10.0.0.3
           \                       /
            \                     /
           10.1.0.2          10.0.0.2
               ##################
               r3 - rid: 10.3.0.3
               ##################
```
You must also have a routing entry for `50.64.3.7` that does not have a corresponding arp cache entry.

# Control-Plane Baseline Tests

The control-plane baseline tests are located in `$P4_PROJECT_DIR/sw/simple_router_sw/simulation/sanity_check.py`.

It is possible that, although a new control plane is instantiated for each test, your state will not be fully cleared before the start of each test. If you encounter this issue, simply clear state in `setUp`.

# Mininet Testing (optional, but strongly recommended)

After the above baseline tests are passing you should make sure that your router works as expected in Mininet. The `~/tutorials/exercises/simple_router` directory on the VM has a couple topology files that you can use to test your router (see below). Update the Makefile in that directory to point to the P4 router program in your P4-NetFPGA repo and run `$ make` to compile the P4 program and launch the Mininet topology. Once the topology is up and running, you can start your router's control plane on each switch in the topology. For example,

```
# cd $P4_PROJECT_DIR/sw/simple_router_sw
# ./control_plane.py --mode bmv2 --thrift_port 9090 --iface s1-eth1 --config topos/single-router.json
```

You can then open up xterm windows on each host and try tests such as:
* ping between hosts
* ping router interfaces
* traceroute to and through routers
* iperf through routers

**Single Switch Topology**

![single-router-topo]({{ site.baseurl }}/images/single-router-topo.png)

**Triangle Topology**

![triangle-topo]({{ site.baseurl }}/images/triangle-topo.png)

# Submission

When you are ready to submit, tag the appropriate commit. Please include a description of who did what in the commit message.

```
$ git tag -a static-router -m "Submission of my static router functionality. <Description of who did what>"
$ git push origin static-router
```

The instructors will clone your repository and checkout the commit to which this tag points. We will then run your code and ensure that the provided baseline tests are passing.
