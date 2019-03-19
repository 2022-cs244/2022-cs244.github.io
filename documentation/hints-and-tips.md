---
layout: page
title: Hints and Tips
---

Here's a set of hints and tips that you may find useful as you develop the router:

* Are you handling PWOSPF HELLO packets correctly in the data-plane? What IP address are they sent to?
* Be sure to make use of the CLI tool to add/remove/inspect table entries and read/write counters
* Here is useful command for configuring the tables in your P4 switch:
    * `cat ${P4_PROJECT_DIR}/src/commands.txt | ${P4_PROJECT_DIR}/sw/CLI/P4_SWITCH_CLI.py`
* Possible initial tests:
    * Is your router forwarding correctly with statically configured table entries?
    * Can you ping each of the routers interfaces?
    * Is the router responding to ARP requests?
    * Be careful if you are trying to ping one interface from the other. Unless you are careful, linux will force the traffic to use the loopback interface rather than sending packets out onto the wire. [It is possible](https://serverfault.com/questions/127636/force-local-ip-traffic-to-an-external-interface) to do this, but it'll be easier (and less confusing) if you can arrange a time with a neighboring group to use their NIC. Then you can do small tests like sending pings through the router, traceroute to and through the router, send iperf flows through the router, and so on.
* Occassionally the `nf0` - `nf3` network interfaces do not come up after programming the FPGA. Try running the following command to bring it back up:
    * `# ifdown nf0 && ifup nf0`
* Configure interface with IP address: 
    * `# ifconfig eth1 1.2.3.4 netmask 255.255.255.0`
* Configure interface with MAC address:
    * `# ifconfig eth1 hw ether 00:11:22:33:44:55`
* Adding routing table entries on Ubuntu:
    * `# route add -net 1.1.1.0 netmask 255.255.255.0 gw 12.12.12.13 dev eth2`
* Show routing table entries:
    * `# route -n`
* Show arp table entries:
    * `# arp -i eth1`
* If you try to program the FPGA and you see something like the following message: `Check programming FPGA or Reboot machine !`, that probably means that the machine has been shut off since the last time the FPGA was programmed. If the links of the SUME board do not come up when the BIOS enumerates the PCIe endpoints then the SUME board will not be detected. The easiest solution to this problem is simply to do a warm reboot after programming the FPGA: `$ sudo reboot now`. Then try programming the FPGA again after the machine comes back up.
* If the `eth1` or `eth2` interfaces are down then you probably just need to configure them with an IP address using the `ifconfig` command as shown above.
* You can safely ignore the following error that you get when programming the FPGA: `rmmod: ERROR: Module sume_riffa is not currently loaded` because the programming script simply always attempts to unload and reload the `sume_riffa` drivers (even if they are not currently loaded).
* We recommend using VNC Viewer if you'd like a graphical desktop:
    * Install [VNC Viewer](https://www.realvnc.com/en/connect/download/viewer/) if you don't already have it installed.
    * Start a VNC server on your development machine: `$ vncserver`. This command indicates the port on which the VNC server is running.
    * You can then use VNC Viewer to connect to your development machine on the appropriate display port. To connect to a VNC server running on port 1 of packet-3 connect to `packet-3:1` from within VNC Viewer.
    * You can start multiple vnc servers, in which case the port number would just increment.
    * To kill the VNC server runing on port 1: `$ vncserver -kill :1`
