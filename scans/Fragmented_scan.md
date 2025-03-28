# 🔍 Nmap Fragmentation Scan (-f) - Evasion & Packet Manipulation Techniques

## 📋 Overview

The Nmap fragmentation scan (`-f`) is a sophisticated network reconnaissance technique designed to bypass intrusion detection systems (IDS) and firewall filters by splitting packets into smaller fragments.

## 🖥️ Initial Scan Command

```bash
sudo nmap -f 192.168.56.103
```

> **💡 Pro Tip:**
> - The `-f` flag enables packet fragmentation
> - Breaks TCP/IP packets into smaller fragments
> - Default fragment size is 8 bytes
> - Can be customized using `--mtu` option

## 🌐 Fragmentation Mechanics

### 🔬 IP Fragmentation Fundamentals

| Concept | Description | Purpose |
|---------|-------------|---------|
| IP Fragmentation | Splitting IP packets larger than network MTU | Network transmission optimization |
| Default Fragment Size | 8 bytes | Minimal packet size for evasion |
| MTU Customization | Adjustable via `--mtu` | Flexible packet splitting |

## 🕵️ Evasion Techniques

### 1️⃣ IDS/Firewall Bypass

- **Objective:** Circumvent packet inspection mechanisms
- **Technique:** Fragmenting packets to confuse stateful inspection
- **Key Benefits:**
  - Breaks signature-based detection
  - Challenges packet reassembly algorithms
  - Potentially evades strict firewall rules

### 2️⃣ Packet Fragmentation Strategies

- **NULL Scan Fragmentation**
  - Sends fragmented packets with no TCP flags
  - Obscures scanning intent

- **SYN Scan Fragmentation**
  - Breaks connection establishment packets
  - Reduces predictability of network traffic

### 3️⃣ MTU Manipulation

- **Custom MTU Sizes:**
  ```bash
  sudo nmap -f --mtu 16 192.168.56.103
  ```
- **Advantages:**
  - Finer control over packet fragmentation
  - Increased evasion potential
  - Adaptive to network conditions

## 🔬 Wireshark Analysis

### Packet Fragmentation Insight

- **Connection Establishment**
  - Initial SYN packet triggers fragmentation
  - IPv4 header reveals fragmentation details
  - Offset and flag analysis critical

> **🚨 Ethical Reminder:**
> Fragmentation techniques should only be used for legitimate network testing
> Unauthorized scanning can be considered malicious activity

## 📚 Key Takeaways

1. Fragmentation is a nuanced network reconnaissance technique
2. Helps bypass strict network security mechanisms
3. Requires deep understanding of network protocols
4. Ethical use is paramount in cybersecurity practices
