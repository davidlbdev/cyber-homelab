# Cybersecurity Home Lab
This project documents the design, deployment and testing of a virtualised cybersecurity lab environment. The lab simulates real-world attack and defense scenarios using vulnerable machines, an attacker and network monitoring tools.

The goal is to develop practical skills in:
 - Network security
 - Vulnerability assessment
 - Intrusion detection (snort)
 - Firewall configuration (pfSense)

---

## Lab Architecture

The lab consists of multiple virtual machines connected through a segmented network using pfSense.

 - WAN: Bridged Adapter
 - LAN: (pfVulnLabs): 172.30.2.0/24
 - Gateway: 172.30.2.1 (pfSense)

All internal lab VMs reside on the LAN and communicate through pfSense.

## Lab Evolution

### Phase 1: Flat Network (VulnLabs)
 - All VMs on a single internal network (172.30.1.0/24)
 - No traffic control or segmentation
 - Limited visibility and security

### Phase 2: Segmented Network (pfSense)
 - Introduced pfSense as a gateway firewall
 - Created isolated LAN (pfVulnLabs)
