# Google Cloud Packet Mirroring with OpenSource-IDS
Google Cloud Packet Mirroring with OpenSource IDS- Security and Identity Fundamentals | Qwiklabs Solution of LAB 07  by RAJDEEP DAS

----------------------------------------------------------------------------------------------------------------------------------------------------------------------

Overview
Traffic Mirroring is a key feature in Google Cloud networking for security and network analysis. Its functionality is similar to that of a network tap or a span session in traditional networking. In short, Packet Mirroring captures network traffic (ingress and egress) from select "mirrored sources", copies the traffic, and forwards the copy to "collectors". It is important to note that Packet Mirroring captures the full payload of each packet and thus consumes additional bandwidth. Because Packet Mirroring is not based on any sampling period, it is able to be used for better troubleshooting, security solutions, and higher layer application based analysis.

Packet Mirroring is founded on a "Packet Mirroring Policy", which contains the following attributes:

Region
VPC Network(s)
Mirrored Source(s)
Collector (destination)
Mirrored traffic (filter)
Here are a some key points that also need to be considered:

Only TCP, UDP and ICMP traffic may be mirrored. This, however, should satisfy the majority of use cases.
"Mirrored Sources" and "Collectors" must be in the SAME Region, but can be in different zones and even different VPCs, as long as those VPCs are properly Peered.
Additional bandwidth charges apply, especially between zones. To limit the traffic being mirrored, filters can be used.
One prime use case for "Packet Mirroring" is to use it in an Intrusion Detection System (IDS) solution. Some cloud-based IDS solutions require a special service to run on each source VM, or to put an IDS virtual appliance in-line between the network source and destination. Both of these have significant implications. For example, the service based solution, though fully distributed, requires that the guest operating system supports the software. The "in-line" solution can create a network bottleneck as all traffic must be funneled through the IDS appliance. The in-line solution will also not be able to capture "east-west" traffic within VMs in the same VPC.

Google Cloud Packet Mirroring does not require any additional software on the VMs and it is fully distributed across each of the mirrored virtual machines. The "Collector" IDS is placed out-of-path using an Internal Network Load Balancer (ILB) and will receive both "north-south" traffic and "east-west" traffic.

Packet Mirroring lab description
To demonstrate how Packet Mirroring can be used with an IDS consider this example using OpenSource IDS Suricata.

A single VPC with 2 subnets, one for mirrored sources and one for the collector
2 Web servers created with a public IP address
1 Collector server (IDS) created with NO public IP for security reasons
CloudNAT enabled for Internet access as needed
All VMs created in the same region and zone, for simplicity and cost reasons
In this lab you will create a Google Cloud environment, configure the "Collector" ILB, configure the Packet Mirror Policy, as well as install and configure [Suricata] (https://suricata-ids.org/) on a virtual instance to act as an IDS. Once complete, network tests will be performed to validate the configuration and use of Packet Mirroring with the Open Source IDS. A very stripped down rule-set and Suricata configuration is used to simplify the demonstration..

<img src="https://cdn.qwiklabs.com/InP14ifJfyrx5Qnxo4Ykd11A3lsCp1nwdOJWTpqwXVE%3D">

Objectives:

Build out a Google Cloud Networking environment as shown in the diagram above

Create 2 virtual machines with gcloud commands to act as WEB SERVERS

Create a single virtual machine with gcloud commands to act as IDS

Create an Internal LoadBalancer (ILB) to act as a "collector" for Packet Mirroring

Install and configure an Open Source IDS (Suricata) on the IDS VM

Review some basic IDS alert rules

Create a Packet Mirror Policy

Test Packet Mirroring by generating network traffic to the "mirrored" subnet

Test Suricata IDS by generating network traffic to simulate an IDS event and review IDS logging
