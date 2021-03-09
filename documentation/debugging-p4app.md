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
