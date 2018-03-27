---
layout: page
title: Starter Code Overview
---

We have provided you with some starter code in a P4->NetFPGA project directory called `simple_router`. The directory structure is as follows:

```
simple_router/
|- Makefile
|- src/: P4 source files and static table entries used for data-plane simulation
|- sw/: Control-plane source files, control-plane simulation files, P4->NetFPGA generated API and CLI files
|- testdata/: source files for data-plane simulations
|- simple_sume_switch/
   |- test/: Full NetFPGA simulation files
   |- hw/: Top level HDL source files
   |- sw/: Software to read all SUME control regs
   |- bitfiles/: directory to store bitfiles
```

# Data-Plane Starter Code

The P4 data-plane starter code is in the `src` folder. The first file you will want to familiarize yourself with is called `simple_router.p4`. It contains a very simple router design with a single table that simply matches on the packet's source port and either invokes an action called `set_output_port` or `NoAction` depending on the configured table entries. Obviously this not how an internet router works so your job is as follows:

* Define additional headers
* Extend parser to parse your additional headers
* Define additional tables and actions
* Implement match-action control-flow
* Extend deparser to emit your additional headers

The `digest_data` struct is a metadata bus that will be prepended to the packet whenever it is forwarded to the control-plane. The exact format of this struct can be defined by the P4 programmer. The starter code defines the `digest_data` struct as follows:

```
struct digest_data_t {
    bit<240>  unused;
    bit<8>   digest_code;
    bit<8>   src_port;
}
```

We recommend that you use this format, but you do not have to if you prefer to use something different. Keep in mind that this struct must be 256 bits wide and if you change the format then you will need to update the `sss_sdnet_tuples.py` file in the `testdata` directory, as well as the `sss_digest_header.py` file in the `sw/simple_router_sw/headers` directory.

# Control-Plane Starter Code

The control-plane starter code is in the `sw/simple_router_sw` directory which has the following format:

```
sw/simple_router_sw/
|- control_plane.py
|- arp_cache.py
|- PWOSPF_handler.py
|- cp_config.py
|- hw_tables_api.py
|- routing_consts.py
|- topology_database.py
|- headers/
|- simulation/
|- tests/
|- utils/
```

