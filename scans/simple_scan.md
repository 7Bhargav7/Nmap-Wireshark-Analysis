# 🛠 Nmap Simple Scan - Observation & Wireshark Analysis

## 🖥 Nmap Scan Output

### 🔹 Scan Command

![Nmap Scan Command](https://github.com/user-attachments/assets/0307efd8-c0aa-4007-8cc8-6dfc2bd58968)

## 🔍 Observations

### Port Scanning Overview

Nmap scanned the most common 1000 ports by default. Multiple open ports were detected, which is expected in Metasploitable since it is designed for penetration testing.

### Port States

- **open**: Service is running and accepting connections
- **closed**: No service is running on the port
- **filtered**: A firewall or security rule is blocking the scan response

## 🕵️ Scan Methodology

The scan was performed using a SYN scan (-sS) despite running as a non-root user. Despite not using root privileges (sudo), Nmap Simple Scan performed a **SYN scan (-sS)**, executing a **two-way handshake** instead of the default full **three-way handshake (-sT)** on Metasploitable.

### Potential Indicators

- The Metasploitable VM allows raw packet transmission
- User or system may have implicit permissions to send raw packets
- A security policy or kernel setting might be enabling this behavior
- Nmap may have been modified or configured differently in the Kali VM

## 📡 Wireshark Analysis - Packet Capture

![Wireshark Packet Capture](https://github.com/user-attachments/assets/d2f6cfdf-c846-4a55-bf77-0ea93cead9b7)

### Handshake Sequence

1. *Nmap sends a SYN packet*
2. *Target responds with SYN-ACK*
3. *Nmap sends a RST (Reset) instead of ACK* - Completing the *two-way handshake*

**Note**: Since the connection never completes with an ACK, it confirms that Nmap *did not establish a full connection* (i.e., no three-way handshake).

## ✅ Conclusion

This validates that **Nmap performed a stealth SYN scan (-sS)** on Metasploitable without needing root privileges.
