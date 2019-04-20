---
layout: page
title: SUME Event Switch
---

As part of an on-going research project, we've developed a new P4 programmable architecture for the NetFPGA SUME board: the "SUME Event Switch". The SUME Event Switch is similar to the SimpleSumeSwitch is many ways. In particular, you still describe the functionality of a parser, match-action pipeline, and deparser by writing a single P4 program. The key difference lies in the events that trigger the pipeline to execute. In the SimpleSumeSwitch, the only event that could trigger the pipeline to execute was an ingress packet arrival. In the SUME Event Switch, your P4 program will now be executed on all of the following data-plane events:
* Ingress Packet Arrival
* Generated Packet Arrival
* Packet Enqueued into an output queue
* Packet Dropped from an output queue (buffer overflow)
* Packet Dequeued from an output queue
* Configurable timer expires
* Link status changes

Below is a block diagram of the SUME Event Switch Architecture:

![SUME Event Switch]({{ site.baseurl }}/images/SUME-Event-Switch.png)

Recall that the SDNet Pipeline is the HDL implementation of your P4 program. Every packet that enters the SDNet pipeline comes with the following metadata fields:

```
struct sume_metadata_t {
    // request a packet to be generated
    bit<1> gen_packet;
    // *_trigger fields indicate when a particular event has fired
    bit<1> link_trigger;
    bit<1> timer_trigger;
    bit<1> drop_trigger;
    bit<1> deq_trigger;
    bit<1> enq_trigger;
    bit<1> pkt_trigger;
    // Current link status (one-hot)
    bit<4> link_status;
    // time when timer event fired (20ns resolution)
    bit<48> timer_now;
    // period at which timer events are configured to fire (20ns resolution)
    bit<32> timer_period;
    // ports and user metadata for enq/deq/drop events
    port_t drop_port;
    port_t deq_port;
    port_t enq_port;
    bit<32> drop_data;
    bit<32> deq_data;
    bit<32> enq_data;
    // standard metadata fields
    port_t dst_port;
    port_t src_port;
    bit<16> pkt_len;
}
```

