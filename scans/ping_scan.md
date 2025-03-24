# 🛠 Nmap Ping Scan - Observation & Wireshark Analysis

## 🖥 Nmap Scan Output

### 🔹 Scan Command

![Nmap Scan Command](https://github.com/user-attachments/assets/072f9c4d-6212-4bdd-833a-745992e40591)

## 🔍 Observations

The scan identified 3 hosts in the local network:

### 1️⃣ Metasploitable's MAC Address is Visible

- **Observation**: Since Metasploitable has many open ports, its MAC address is exposed in the scan results.

### 2️⃣ Kali's MAC Address is Hidden

- **Observation**: Despite being an active host, Kali's MAC address is not displayed in the scan results.
- **Insight**: This suggests that Kali might be configured to suppress MAC address broadcasting, possibly due to security settings.

### 3️⃣ Windows Host Machine's MAC Address is Not Displayed

- **Observation**: The host system running the VMs did not return a MAC address.

## 📡 Wireshark Analysis - ARP & ICMP Behavior

### 🔹 Wireshark Capture

![Wireshark ARP Packet](https://github.com/user-attachments/assets/03985701-ce99-48aa-8ac7-278b719cea45)

### 🔍 Observed Behavior

1. *ICMP traffic is not visible* in Wireshark despite being expected.
2. *Nmap defaults to ARP scanning* instead.
3. *ARP requests successfully detect active hosts* in the local network.

### 🤔 Why ARP Over ICMP?

- **Efficiency in Local Networks**: ARP is more efficient in local networks where MAC addresses are used for communication.
- **Scanning Limitations**: ICMP is useful for scanning across subnets, but in a single local network, ARP is prioritized for efficiency.
- **Nmap Preference**: Nmap defaults to ARP scanning when possible, as it provides more reliable results in LAN environments.

## ✅ Conclusion

- **Effective Host Discovery**: Nmap's -sP (ping scan) effectively identifies hosts using ARP in local networks.
- **Scanning Strategy**: ICMP scanning is deprioritized in favor of ARP, making ARP the preferred method for discovering live hosts in the same subnet.
