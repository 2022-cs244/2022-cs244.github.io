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

The P4 data-plane starter code is in the `src` folder.

```
src/
|- simple_router.p4 : main P4 source file
|- commands.txt : set of CLI commands to add entries to the tables specified in the P4 program
|- Makefile : compiles P4 program into intermediate representation for SDNet and generates SDNet table files
```

#### simple_router.p4

The first file you will want to familiarize yourself with is called `simple_router.p4`. It contains a very simple router design with a single table that simply matches on the packet's source port and either invokes an action called `set_output_port` or `NoAction` depending on the configured table entries. Obviously this not how an internet router works so your job is as follows:

* Define additional headers
* Extend parser to parse your additional headers
* Define additional tables and actions
* Implement match-action control-flow
* Extend deparser to emit your additional headers

We will use a ternary match table for the routing table for this project rather than a longest prefix match table (LPM) because SDNet does not fully support LPM tables at the moment. We have provided some wrapper functions in the control-plane starter code for you to try and expose LPM-like functionality on top of the ternary table. Other than higher resource utilization on the FPGA, the main difference between the ternary match and LPM tables is that the control-plane must explicitly manage the priority of each entry. The priority is indicated by the entry's address, smaller addresses indicate higher priority.

The `digest_data` struct is a metadata bus that will be prepended to the packet whenever it is forwarded to the control-plane. The exact format of this struct can be defined by the P4 programmer. The starter code defines the `digest_data` struct as follows:

```
struct digest_data_t {
    bit<240>  unused;
    bit<8>   digest_code;
    bit<8>   src_port;
}
```

We recommend that you use this format, but you do not have to if you prefer to use something different. Keep in mind that this struct must be 256 bits wide and if you change the format then you will need to update the `sss_sdnet_tuples.py` file in the `testdata` directory, as well as the `sss_digest_header.py` file in the `sw/simple_router_sw/headers` directory.

#### commands.txt

This file may contain `table_cam_add_entry` or `table_tcam_add_entry` commands. See the [workflow overview](https://github.com/NetFPGA/P4-NetFPGA-public/wiki/Workflow-Overview#writing-p4-programs) on the P4->NetFPGA wiki page. After compiling your P4 program and loading the bitstream onto the FPGA, this file can be `cat`ed into the `P4_SWITCH_CLI.py` file to load table entries. e.g. `$ cat commands.txt | ${P4_PROJECT_DIR}/sw/CLI/P4_SWITCH_CLI.py`.

---

The main data-plane simulation tools are in the `testdata` directory.

```
testdata/
|- gen_testdata.py : generates the input packets / metadata as well as the expected output packets / metadata
|- sss_sdnet_tuples.py : used for creating the input / output metadata files for SDNet simulations
|- Makefile : executes gen_testdata.py and converts pcap packets into AXI format for SDNet simulations
```

#### gen_testdata.py

This file generates the testdata used for both the SDNet and the full SUME simulation. See the [workflow overview](https://github.com/NetFPGA/P4-NetFPGA-public/wiki/Workflow-Overview#testing-p4-programs) for more details on what it should produce.

We have provided a few helper functions in the `gen_testdata.py` script to help you get going. See the starter code for a description of their functionality. We have also provided you with a few baseline test cases at the bottom of the file. You will need to add more to thoroughly test your design. 

#### sss_sdnet_tuples.py

This file defines the format of the `digest_data`, which should have an equivalent definition in the P4 program. It also imports the standard `sume_metadata`. These metadata buses are stored as python `OrderedDict()` objects. This file contains helper functions to write these metadata buses into the `Tuple_*.txt` files in the format expected by the SDNet simulation. If you choose not to modify the format of the `digest_data` bus then you shouldn't need to make any modifications to this file.

---

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

