# pfSense Port Forwarding

A port forwarding rule was configured on the pfSense WAN interface to allow the host machine to access Metasploitable2 inside the internal lab network.

## Objective

The goal was to simulate exposing an internal service through a firewall, allowing controlled access from outside the lab LAN.

## Target

| Device | IP Address | Purpose |
|---|---|---|
| Metasploitable2 | 172.30.2.102 | Vulnerable Linux target |

## Result

After configuring the WAN port forwarding rule:

- The host PC could ping Metasploitable2
- SSH access from the host PC to Metasploitable2 was successful

## Security Consideration

Port forwarding increases exposure because it allows traffic from outside the LAN to reach an internal machine.

In a real environment, this should be limited using:

- Source IP restrictions
- Strong authentication
- Minimal exposed services
- IDS/IPS monitoring
