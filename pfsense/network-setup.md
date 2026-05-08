# pfSense Network Setup

pfSense was added to the lab to improve segmentation and create a more realistic network security environment.

## VirtualBox Network Adapters

| Adapter | pfSense Interface | Mode | Purpose |
|---|---|---|---|
| Adapter 1 | WAN | Bridged Adapter | External/host network access |
| Adapter 2 | LAN | Internal Network | Internal lab network |

## LAN Network

| Setting | Value |
|---|---|
| Network Name | pfVulnLabs |
| Subnet | 172.30.2.0/24 |
| Gateway | 172.30.2.1 |
| DHCP Range | 172.30.2.100-172.30.2.150 |

## pfSense Web Setup

| Setting | Value |
|---|---|
| Hostname | pfSense |
| Domain | dlb.ca |
| Admin User | admin |

## Lab Migration

The lab was migrated from the original flat `VulnLabs` network to the segmented `pfVulnLabs` network.

This change introduced:

- A dedicated firewall gateway
- Central DHCP management
- Traffic filtering
- Gateway-level IDS/IPS capability through Snort
