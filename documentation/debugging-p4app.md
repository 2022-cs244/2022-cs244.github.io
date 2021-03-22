---
layout: page
title: Debugging with p4app
---


# Log Directory Location

 - Within the Docker container, p4app saves log files to `/tmp/p4app-logs`.
 - By default, `/tmp/p4app-logs` is mounted from `/tmp/p4app-logs` on the host
   machine.
 - The log directory location can be overridden by specifying the
   `P4APP_LOGDIR` env variable.
    - e.g., `mkdir ~/mylogs`, then `P4APP_LOGDIR=~/mylogs ~/p4app/p4app run .`

# The BMv2 Log

 - Each switch logs to `/tmp/p4app-logs/p4s.XXX.log`, where `XXX` is the name
   of the switch.
    - e.g., the log for switch `s1` will be in `/tmp/p4app-logs/p4s.s1.log`.

# PCAP Files

 - By default, BMv2 dumps all packets received/sent by the switches to PCAP
   files in the log directory (`/tmp/p4app-logs`).
 - For each switch, there are two PCAP files per port: packets sent by the
   switch (`*_in.pcap`), and received (`*_out.pcap`).
    - e.g., `/tmp/p4app-logs/s1-eth2_out.pcap` contains the packets sent by `s1` on port `2`.
 - Tip: use `mergecap` for viewing both PCAPs together: `mergecap -w tmp.pcap /tmp/p4app-logs/s1-eth2_* && wireshark tmp.pcap`


# Mininet Console

 - You can launch a [Mininet console from the p4app entry point](https://github.com/2021-cs344/p4app/blob/rc-2.0.0/examples/wire.p4app/main.py#L13) (`main.py`).
 - The console can be used for inspecting Mininet, for example:
    - Show the interfaces for switch `s1`: `mininet> py s1.intfs`
    - Show help: `mininet> help`
 - This can also be used to run commands on hosts:
    - Print interface status: `mininet> h1 ifconfig`
    - Send a ping packet from `h1`: `mininet> h1 ping -c1 10.0.0.1`

# Running Commands Inside p4app

 - Once you have launched a p4app, you can interact with it from another terminal
 - The `p4app exec` command lets you run a program within the container of the most recently launched p4app.
    - Open a shell in the *container*: `~/src/p4app/p4app exec bash`
    - Open a shell on a *Mininet host* within container: `~/src/p4app/p4app exec m h1 bash`
