# pfSense

This folder documents the pfSense firewall deployment used in the cybersecurity home lab.

pfSense is used to provide:

- Gateway routing
- DHCP for the internal lab network
- Firewall rule enforcement
- Port forwarding
- Snort IDS/IPS integration

## Network Role

pfSense separates the lab into:

- **WAN**: Bridged adapter for external/host access
- **LAN**: Internal network `pfVulnLabs`
- **LAN Gateway**: `172.30.2.1`

## Related Files

- `network-setup.md` – pfSense interface and LAN configuration
- `port-forwarding.md` – WAN-to-LAN forwarding to Metasploitable2
- `snort-ips.md` – Snort installed on pfSense
- `pass-lists-and-suppressions.md` – Tuning false positives and trusted hosts
