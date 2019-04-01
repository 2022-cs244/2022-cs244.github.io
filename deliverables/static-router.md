---
layout: page
title: Static Router Functionality
---

The goal of this deliverable is to ensure that you have implemented all of the required functionality of a static IPv4 router. To help get you started, we have provided some baseline data-plane and control-plane tests. These tests test *some* of the required functionality of your router so you will want to add more of your own. Although you are encouraged to add more tests of your own, please do not modify the existing baseline tests (aside from any `TODO`s) without permission of the instructors.

The baseline tests are described in `$P4_PROJECT_DIR/overview.md`.

# Mininet Testing (optional, but strongly recommended)

After the above baseline tests are passing you should make sure that your router works as expected in Mininet. The `~/tutorials/exercises/simple_router` directory on the VM has a couple of topology files that you can use to test your router (see below). Update the Makefile in that directory to point to the P4 router program in your P4-NetFPGA repo and run `$ make` to compile the P4 program and launch the Mininet topology. Once the topology is up and running, you can start your router's control plane on each switch in the topology, as described in `$P4_PROJECT_DIR/overview.md`, and run commands in the Mininet console to test your router.

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
