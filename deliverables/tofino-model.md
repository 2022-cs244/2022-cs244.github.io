---
layout: page
title: Developing and Testing Programs for Tofino
---

# Background

Now that each team has built a working router system and tested it with other teams' implementations at the network level, it's time try to port each team's router program for Tofino, a 6.4Tbps P4-programmable switching ASIC. As you have learned from a lecture, as a P4 target, the PISA machine offers unique and very powerful benefits compared to software switches or CPU-based P4 targets in general; for those programs that compile successfully, it ensures extremely "high" and "predictable" performance in terms of throughput, latency, and power consumption at run time irrespective of any incoming traffic workloads. 

Such benefits, however, do not come for free. The PISA machine trades some amount of flexibility and generality for performance. Hence it supports only a small, limited length of dependency chains in program logic, offers a limited memory-access model, provides a limited set of instructions optimized mainly for packet processing, and equips a limited amount of physical resources to parse packets and carry the parsed representation. Hence, in order to develop useful P4 programs customized for PISA, it's necessary to understand such limitations and adapt your programs appropriately to the limitations.

# Goals

The main goal of this assignment is 1) porting your existing router P4 program for Tofino using [Tofino Native Architecture](https://github.com/barefootnetworks/Open-Tofino/blob/master/PUBLIC_Tofino-Native-Arch-Document.pdf), and 2) testing the program with a simple test framework, called PTF (Packet-level Test Framework). The first part requires modifying your existing P4 program for TNA and compiling it successfully using the Tofino-specific P4 compiler (p4c-tofino). If necessary, you'll have to use a compile-assistance tool, called `p4i` for this. The second part requires writing a simple Python program that uses the APIs derived from your P4 program through the compilation process.

# Preparations

You'll use Intel P4 Studio Lite for this assignment. You can find the original P4 Studio Lite package at `/home/p4dev/shared_folder/install-bf-sde-9.4.0-lite` in the VM you're using for the class. The directory contains `README.md`, which explains how to install the package on a vanilla Ubuntu machine. Note, however, that we have already installed the package in the VM for you; you won't have to repeat the installation process. 

The installation process creates the following three directories in your home directory:

- `bf-sde-9.4.0` - The Intel/Barefoot SDE 9.4.0, lite version.
- `tools` - A few scripts that will be useful.
- `demos` - Some demo P4 programs written for 

Before you try to port your router P4 program, make sure you try compiling `demo1_tna.p4`, a sample TNA program in the `demos/demo1_tna` directory. Please take a look at `README.md` in that directory, which explains how you can set up the right environment, compile the program, produce a P4 binary file, investigate the compilation results (a.k.a., resource consumption status) using a visualization tool called p4i, and test the program using the Tofino ASIC model and PTF framework.

You can find .. (https://github.com/barefootnetworks/Open-Tofino).

**__Do NOT share Intel P4 Studio Lite with anyone outside the class by mistake or redistribute it on purpose__**. Intel P4 Studio Lite is Intel's product, and hence Intel reserves the sole right to redistribute it. CS344 has received a special permission to use it only for the class.

# The Assignment

Once you have succedeed in following all the steps above, you need to 

1. Port the P4 program

- Learn TNA and modify your existing P4 program for that.
- Replace BMv2-specific intrinsic metadata with TNA-specific intrinsic metadata. 
- Use the new architecture model (find an example TNA program in ...)

2. Write a PTF test script to test the P4 program 




3. Enhance your P4 program and test it. You'll need to try at least three out of these four recommendations.

- Increase table sizes
- Implement additional protocols in the data plane. ICMP, ARP, 
- ECMP
- Implement programs based on data-plane state (round-robin)


