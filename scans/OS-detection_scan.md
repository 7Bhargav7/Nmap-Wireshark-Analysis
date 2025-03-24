# 🔍 Nmap OS Scan (-O) - Detailed Observation & Wireshark Analysis

## 📋 Overview

This comprehensive guide explores the intricacies of Nmap's Operating System (-O) detection scan, providing a deep dive into the technical nuances of network reconnaissance and OS fingerprinting.

## 🖥️ Initial Scan Command

![Nmap Scan Command](https://github.com/user-attachments/assets/b660e5b6-97d2-47b1-80be-a609d9c189ef)

```bash
sudo nmap -O 192.168.56.103
```

> **💡 Pro Tip:** 
> - The `-O` flag enables OS detection
> - Requires root/sudo privileges
> - Uses multiple probing techniques to guess the target's operating system

## 🕵️ Scanning Methodology

Nmap's OS detection is a multi-stage process that involves:

- **Stealth TCP SYN Scanning**
- **Unusual Packet Probing**
- **Detailed Response Analysis**

### 🔬 Probe Types

| Probe Type | Description | Purpose |
|-----------|-------------|---------|
| TCP SYN Stealth | Sends SYN packets without completing handshake | Initial port discovery |
| NULL Scan | Packet with no TCP flags | OS response differentiation |
| FIN Scan | Packet with only FIN flag | Detect firewall and OS behaviors |
| XMAS Scan | Packet with FIN, URG, PSH flags | Advanced OS fingerprinting |

## 🌐 Detailed Analysis Stages

### 1️⃣ TCP SYN & SYN-ACK Discovery

![TCP SYN & SYN-ACK Scan](https://github.com/user-attachments/assets/6181c49b-0347-4a92-945a-e48f45811178)

- **Goal:** Identify open ports stealthily
- **Technique:** Send SYN, receive SYN-ACK, respond with RST
- **Wireshark Filter:** `tcp.flags.syn == 1`

### 2️⃣ Unusual Packet Scanning

![Windows Scan](https://github.com/user-attachments/assets/0a01a7e2-f443-4e36-9859-3dcd4376153d)

![FIN Scan](https://github.com/user-attachments/assets/54814dac-5447-4870-92ba-3aa85ef18946)

![XMAS Scan](https://github.com/user-attachments/assets/c51f6c14-05a4-4c10-86e8-a5554c93d673)

- **Objective:** Trigger unique OS responses
- **Methods:** 
  - NULL Scan (`tcp.flags == 0x000`)
  - FIN Scan (`tcp.flags.fin == 1`)
  - XMAS Scan (`tcp.flags==0x29`)

### 3️⃣ Window Size & MSS Analysis

![Window Size Probe](https://github.com/user-attachments/assets/0a79e900-0856-4d78-a943-3be648f52596)

- **Focus:** Examine TCP window sizes
- **Wireshark Filter:** `tcp.flags.syn==1 && tcp.window_size==5840`
- **Key Observations:**
  - Windows: Often uses 8192 or 65535
  - Linux: Variable window sizes

### 4️⃣ TCP Timestamp Examination

![TCP Timestamp Analysis](https://github.com/user-attachments/assets/44c86cdc-3dc8-4c95-a321-5d04966b0d53)

- **Purpose:** Analyze system uptime markers
- **Wireshark Filter:** `tcp.options.timestamp`
- **Insights:** 
  - Timestamp presence
  - System uptime characteristics

### 5️⃣ Duplicate ACKs & Retransmissions

![Duplicate ACKs](https://github.com/user-attachments/assets/2a78e2fa-3beb-445a-8878-58443faa28bb)

- **Analysis:** Network stack behavior
- **Wireshark Filters:**
  - Duplicate ACKs: `tcp.analysis.duplicate_ack`
  - Retransmissions: `tcp.analysis.retransmission`

## 🏁 Conclusion

**Nmap's OS detection is a sophisticated process that:**
- Correlates multiple response characteristics
- Builds a comprehensive TCP/IP stack fingerprint
- Estimates OS with varying confidence levels

> **🚨 Security Reminder:** 
> Always obtain proper authorization before performing network scans. Unauthorized scanning can be considered a hostile network activity.

## 📚 Key Takeaways

1. OS detection is multi-layered
2. Different OSes respond uniquely to crafted packets
3. Wireshark provides granular insight into scanning techniques
4. Reconnaissance requires technical precision and ethical consideration
