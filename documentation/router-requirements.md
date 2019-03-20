---
layout: page
title: Router Requirements
---

# Data-Plane Basic Requirements

* Provide a routing table that can store IP address/prefix pairs with their associated port and next-hop IP address.
* Use the routing table to perform a longest prefix match on destination IP addresses and return the appropriate egress port and next-hop address (or 0.0.0.0 for a directly attached destination). 
    * NOTE: We will use a ternary match table for the routing table because LPM tables are not fully supported by SDNet yet.
* Provide an ARP table that can store at least 64 entries. This will accept an IP address as a search key and will return the associated MAC address (if found). This table is modified by the software, which runs its own ARP protocol.
* Provide a “local IP address table”. This will accept an IP address as a search key and will return a signal that indicates whether the corresponding address was found. This table is used to identify IP addresses that should be forwarded to the local control-plane.
* Decode incoming IP packets and perform the operations required by a router. These include (but are not limited to):
    * verify that the existing checksum and TTL are valid
    * look up the next-hop port and IP address in the routing table
    * look up the MAC address of the next-hop in the ARP table
    * set the src MAC address based on the port the packet is departing from
    * decrement TTL
    * calculate a new IP checksum
    * transmit the new packet via the appropriate egress port
    * local IP packets (destined for the router) should be sent to the local control-plane
    * PWOSPF packets should be sent to the local control-plane
    * packets for which no matching entry is found in the routing table should be sent to the software
    * any packets that the hardware cannot deal with should be forwarded to the local control-plane. (e.g. not Version 4 IP)
* Provide counters for the following:
    * IP packets
    * ARP packets
    * Packets forwarded to the control-plane

# Control-Plane Basic Requirements

### Static Router Requirements

* Sending ARP requests
* Updating entries in the hardware ARP cache
* Timing out entries in the hardware ARP cache
* Queuing packets pending ARP replies
* Responding to ICMP echo requests
* Generating ICMP host unreachable packets
* Handling corrupted or otherwise incorrect IP packets
* Handling all packets addressed directly to the router
* Support static routing table entries

### Dynamic Router Requirements

* Building the routing table via a dynamic routing protocol [PWOSPF](({{ site.baseurl }}/documentation/pwospf))
* Support static routing table entries in addition to the routes computed by PWOSPF

# You Decide

* Responding to ARP requests is fairly straight forward to express in P4. You can decide whether you want to implement ARP responding in the control-plane or the data-plane.

# Additional Resources

You may find it useful to refer to [RFC 1812](https://tools.ietf.org/html/rfc1812) for a detailed description of IPv4 router requirements. Note that we only require you to implement a subset of the requirements for this class.


