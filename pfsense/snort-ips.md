# Snort on pfSense

Snort was installed on pfSense to provide gateway-level intrusion detection and prevention.

Unlike the standalone Snort VM, this deployment monitors traffic through the pfSense firewall interface.

## Purpose

Snort on pfSense is used to:

- Detect suspicious traffic entering or leaving the lab network
- Block offending hosts automatically
- Compare gateway-level detection with standalone Snort VM monitoring

## Initial Rules

Custom alert rules were configured for:

- ICMP traffic
- SSH traffic
- Nmap SYN scans
- Nmap Xmas scans
- SSH brute force attempts
- FTP brute force attempts
- Reverse shell behaviour
- Web command injection attempts

## Blocking Mode

Snort was configured to block offenders that triggered selected rules.

Observed behaviour:

1. Traffic matched a Snort rule
2. Snort generated an alert
3. Source IP was added to the blocked list
4. Further communication from that IP was denied

## Example Behaviour

When testing outbound traffic to Google:

- The first ping passed
- Snort detected the traffic
- The source was blocked
- Further traffic was stopped

## Key Lesson

Snort on pfSense can operate as an IPS, not only an IDS.

This is useful for prevention, but it also introduces the risk of false positives blocking legitimate traffic.
