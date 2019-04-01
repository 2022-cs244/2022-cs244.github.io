---
layout: page
title: SimpleSumeSwitch in BMv2 Mininet
---

P4.org has developed an open source software switch called BMv2 (behavioral model version 2) designed to be a target for P4 programs. That is, P4 programs can be compiled onto it to configure how it processes packets. Every P4 target supports one or more P4 target architectures. BMv2 was initially designed with support for the so called V1Model architecture. The CS344 instructors have added initial support for the [SimpleSumeSwitch architecture](https://github.com/NetFPGA/P4-NetFPGA-public/wiki/Workflow-Overview#simplesumeswitch-architecture) so that we can run "virtually" the same P4 programs in both Mininet and the NetFPGA platform.

I say "virtually" because there are a number of ways in which the SimpleSumeSwitch in BMv2 differs from the SimpleSumeSwitch on NetFPGA. Here is a list of the major differences:
* The extern functions in the [NetFPGA Extern Function Library](https://github.com/NetFPGA/P4-NetFPGA-public/wiki/Workflow-Overview#p4-netfpga-extern-library) are currently unsupported in BMv2. So do not try to use them in your P4 programs that you run in BMv2.
* The `digest_data` metadata bus is currently unused. In order to send digest information to the control-plane, you should create a separate `digest_header` and prepend that header to packets that are sent to the control-plane. The control-plane should then extract the `digest_header` from the packet before processing.
* Broadcasting packets is currently unsupported. So only try to set one bit of the `sume_metadata.dst_port` field.
* P4 support in BMv2 is generally more comprehensive than P4 support in SDNet. As a result, some P4 programs that work fine in BMv2 may not compile with SDNet. See [here]({{ site.baseurl }}/documentation/p4c-sdnet-missing-features.pdf) for a description of the P4 features that are currently unavailable in SDNet. As a result, we recommend that you first develop your P4 programs using P4->NetFPGA and once your HDL simulations are working, run the same program on bmv2 in Mininet.

## Using BMv2 Mininet

This section provides an overview of using the BMv2 Mininet environment in the virtual machine that you set up in the [Getting Started]({{ site.baseurl }}/deliverables/getting-started) deliverable.

The main directory is located in `/home/p4/tutorials`. The `exercises` directory contains various projects. The only ones we will be using for this course are `basic`, `switch_calc`, and `simple_router`; although feel free to create your own as well. Each exercise directory contains one or more the following files:
* `s*-commands.txt` - one file for each switch in the topology that includes BMv2 CLI commands to populate table entries upon building the topology. See below for more info on the 
* `topology.json` - a JSON file that contains a description of the topology and any commands to run on each host upon building the topology. See below for more details on the topology file.
* `Makefile` - indicates which P4 program to compile and which topology file to use

#### BMv2 CLI Commands

The BMv2 CLI commands are slightly different from the P4->NetFPGA CLI commands. Here are a few examples of commands to populate entries for the various table types:

```
# Exact Match Table
table_add <table_name> <action_name> <keys (space separate)> => <action_data (space separated)>

# Ternary Match Table
table_add <table_name> <action_name> <key>&&&<mask> => <action_data (space separated)> <priority (0 is highest)>

# LPM Table
table_add <table_name> <action_name> <key>/<prefix_len> => <action_data (space separated)>

```

#### Building a Topology

Below is an example topology file that simply connects two hosts to a single switch and runs a single command on each host to tell it how to reach the other host through the switch.

```
{
    "hosts": {
        "h1": {"ip": "10.10.10.11/31", "mac": "08:10:10:10:10:11",
               "commands":["route add -net 20.20.20.20 netmask 255.255.255.254 gw 10.10.10.10 dev eth0"]},
        "h2": {"ip": "20.20.20.21/31", "mac": "08:20:20:20:20:21",
               "commands":["route add -net 10.10.10.10 netmask 255.255.255.254 gw 20.20.20.20 dev eth0"]}
    },
    "switches": {
        "s1": {"cli_input": "s1-commands.txt"}
    },
    "links": [
        ["h1", "s1-nf0"], ["h2", "s1-nf1"]
    ]
}
```

To build the Mininet topology and deploy your P4 program on each switch run `$ make` in the project directory. When the topology is built, a controller host (`cX`) will be connected to each switch on the `sX-eth1` interface. This is the equivalent of the `nf0` DMA interface when using P4->NetFPGA.
