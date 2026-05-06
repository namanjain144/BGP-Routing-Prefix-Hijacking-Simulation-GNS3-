BGP Routing & Prefix Hijacking Simulation (GNS3)
⚠️ Disclaimer
This project was completed as part of a university networking/security lab. Some configuration details, topology files, and instructions are confidential and not publicly shared. This repository provides a high-level overview of the implementation, concepts, and results.

📌 Overview
This project simulates Border Gateway Protocol (BGP) behaviour across multiple Autonomous Systems (AS) using GNS3. It demonstrates how routing information is exchanged, how prefix hijacking attacks occur, and how they can be mitigated using routing policies.
The goal was to gain hands-on experience with inter-domain routing, control-plane behaviour, and real-world Internet vulnerabilities.

🌐 Network Architecture

Multi-AS topology with 4 routers across different Internet Exchanges (IXs)
Each router configured with:

Unique Autonomous System Number (ASN)
Router ID


eBGP peering established between adjacent AS nodes
Route propagation enabled via redistribution and manual advertisement


⚙️ Key Implementations
1. BGP Configuration

Created BGP instances with ASN assignments on MikroTik RouterOS
Configured eBGP peer relationships between routers
Enabled route redistribution (connected + BGP routes)
Advertised network prefixes into BGP

2. Route Propagation Analysis

Observed BGP UPDATE messages using Wireshark
Analysed key attributes:

AS-PATH
NEXT_HOP
Prefix information


Verified routing tables across all routers after convergence

3. Prefix Hijacking Attack

Simulated BGP prefix hijacking from a malicious AS (AS-3004)
Announced a more specific prefix (/27) over the legitimate route (/24)
Leveraged longest-prefix match rule to redirect traffic away from the legitimate owner (AS-3001)
Verified traffic redirection using ICMP and Wireshark packet capture

4. Attack Flow
IX-4 (AS-3004) advertised a malicious /27 prefix, which was propagated by IX-3 (AS-3003) upstream to IX-2 and IX-1. ICMP traffic originally destined for AS-3001 was redirected to AS-3004. A prefix-length filter applied at IX-3 discarded the /27 announcement and restored the legitimate /24 route, recovering correct traffic flow across all ASes.
5. Attack Mitigation

Implemented inbound prefix filtering policies on the upstream router (IX-3)
Blocked invalid route advertisements based on prefix length (discarding /25–/32 on the hijacked block)
Restored legitimate routing paths and verified traffic flow returned to AS-3001
Demonstrated the importance of routing policy enforcement at ISP/upstream boundaries


🔍 Key Concepts Learned

BGP control-plane behaviour and route selection
Longest-prefix match and its security implications
Inter-AS routing and trust-based vulnerabilities
Filter-based defence at the upstream AS level, simulating a real ISP response to a hijacking incident
Importance of filtering, validation, and routing policy enforcement
Real-world risks such as route leaks, hijacking incidents, and their impact on Internet-scale routing reliability


🛠️ Tools & Technologies

GNS3 (Network Simulation)
Wireshark (Packet Analysis)
MikroTik RouterOS CLI (BGP configuration)
Linux-based networking environment


📊 Results

Successfully demonstrated traffic hijacking via malicious prefix advertisement
Observed routing table changes propagating across multiple AS nodes in real time
Implemented mitigation to restore correct routing behaviour and verified via packet capture
Identified that trust-based BGP architecture creates systemic Internet-scale risk, motivating the need for RPKI and filtering standards like MANRS
Gained practical understanding of how BGP impacts Internet-scale routing reliability


🚀 Next Steps / Extensions

Exploring RPKI for cryptographic route origin validation and BGPsec for path-level authentication
Automate BGP configuration and policy deployment using Python or Ansible
Simulate larger-scale topologies with additional AS nodes and route reflectors


📎 Note
This project focuses on educational and defensive security purposes only. All experiments were conducted in a controlled GNS3 lab environment.
