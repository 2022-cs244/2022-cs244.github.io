---
layout: page
title: PWOSPF Router Functionality
---

The goal of this deliverable is to ensure that you have implemented all of the functionality required of a router running PWOSPF. The main difference between this deliverable and the [previous one]({{ site.baseurl }}/deliverables/static-router) is in the control-plane functionality. For the previous deliverable, the routing table entries were statically configured. For this deliverable, your router must participate in the PWOSPF protocol to dynamically compute routing table entries based its own configuration and link state advertisements that it hears from other routers running PWOSPF. Please refer to `$P4_PROJECT_DIR/pwospf.md` for detailed information about the PWOSPF protocol.

#  PWOSPF Baseline Tests

There are a few test cases in `$P4_PROJECT_DIR/testdata/control_plane/sanity_check.py` that test various aspects of PWOSPF functionality. Your goal is to ensure that all these test cases pass and you will also want to add your own additional tests as well.

# Mininet Testing (optional, but strongly recommended)

As in the previous deliverable, after the above baseline tests are passing you should make sure that your router works as expected in Mininet and is indeed interoperable with itself. 

# Submission

When you are ready to submit, tag the appropriate commit. Please include a description of who did what in the commit message.

```
$ git tag -a pwospf-router -m "Submission of my pwospf router functionality. <Description of who did what>"
$ git push origin pwospf-router
```

The instructors will clone your repository and checkout the commit to which this tag points. We will then run your code and ensure that the provided baseline tests are passing.

Please email the instructors the bitfile for the router that you used for the PWOSPF interoperability test.
