# Nmap SYN Scan Detection

## Objective

Test detection of TCP SYN reconnaissance scans using Snort.

---

# Environment

| System | Role |
|---|---|
| Kali Linux | Attacker |
| Metasploitable2 | Target |
| Snort | IDS |

---

# Attack Performed

```bash
nmap -sS 172.30.1.21
```

---

# Detection Rule

```snort
alert tcp any any -> $HOME_NET any (msg:"Nmap SYN Scan Detected";flags:S;threshold:type both, track by_src, count 20, seconds 10;sid:1000003;rev:1;)
```

---

# Detection Logic

The rule detects:
- TCP packets with SYN flag set
- High volume of SYN packets
- Multiple packets from same source within short timeframe

---

# Result

Snort successfully:
- Detected SYN scan activity
- Generated alert
- Logged attack traffic

---

# Evidence

## Example Alert

```text
[**] [1:1000003:1] Nmap SYN Scan Detected [**]
```

<img width="602" height="50" alt="image" src="https://github.com/user-attachments/assets/8ad83e5c-e5e9-4122-bcac-88cc931fafeb" />


---

# Key Learning

SYN scans are commonly used during reconnaissance to identify open ports while attempting to remain stealthier than full TCP connect scans.

Thresholding helped reduce false positives by requiring repeated SYN packets before alerting.
