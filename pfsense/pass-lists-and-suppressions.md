# Pass Lists and Suppression Rules

This document covers the testing and tuning performed to prevent legitimate hosts from being automatically blocked by Snort during IPS testing.

---

## Environment

| Component | Value |
|---|---|
| Firewall | pfSense |
| IDS/IPS | Snort |
| Protected Network | pfVulnLabs |
| LAN Subnet | 172.30.2.0/24 |
| Host PC | 192.168.0.90 |

---

# Suppression Rules

Initial testing used suppression rules to stop alerts from the host PC.

## SSH Suppression

```text
suppress gen_id 1, sig_id 1000002, track by_src, ip 192.168.0.90
```

## ICMP Suppression

```text
suppress gen_id 1, sig_id 1000001, track by_src, ip 192.168.0.90
```

---

## Result

- Host PC could successfully:
  - Ping internal machines
  - SSH into Metasploitable2
- Snort no longer generated alerts for the host PC

---

## Limitations

| Issue | Description |
|---|---|
| Reduced visibility | Alerts from suppressed host completely disappear |
| Over-trust | Entire source IP becomes trusted |
| Detection blind spot | Compromised trusted host may go undetected |

---

# Pass Lists

Pass Lists were tested as a better alternative to suppression rules.

Unlike suppression:
- Traffic is allowed
- Alerts can still be generated
- Visibility is maintained

---

## Configuration Steps

### 1. Create Pass List

Navigate to:

```text
Services → Snort → Pass Lists
```

Create a new custom pass list.

---

### 2. Add Trusted Host

Add the host PC IP:

```text
192.168.0.90
```

---

### 3. Assign Pass List

Assign the pass list to the active Snort interface.

---

### 4. Restart Snort Interface

The Snort interface must be restarted before changes take effect.

---

# Important Observation

Initially:
- Ping traffic was still blocked

Cause:
- Default pfSense local addresses had been unchecked

Fix:
- Re-enable default pfSense local address options in the pass list configuration

After restarting Snort:
- Ping traffic succeeded
- Alerts still appeared
- Host PC was not blocked

---

# Comparison

| Feature | Suppression Rules | Pass Lists |
|---|---|---|
| Prevent blocking | Yes | Yes |
| Generate alerts | No | Yes |
| Maintain visibility | No | Yes |
| Better for monitoring | No | Yes |

---

# Key Takeaway

Pass Lists were the preferred solution for this lab because they:
- Prevented unnecessary blocking
- Allowed trusted traffic
- Maintained alert visibility for monitoring and analysis

This demonstrates the importance of IDS/IPS tuning and balancing security enforcement with operational usability.
