

# 🛠 Nmap Ping_Scan - Observation & Wireshark Analysis  

## 🖥 *Nmap Scan Output*  

Below is the command run and its corresponding output:

### 🔹 *Scan Command:*
![Scan-2](https://github.com/user-attachments/assets/072f9c4d-6212-4bdd-833a-745992e40591)



## 🔍 Observation  

The scan identified 3 hosts in the local network:

1️⃣ **Metasploitable's MAC Address is Visible**


Since Metasploitable has many open ports, its MAC address is exposed in the scan results.


2️⃣ **Kali's MAC Address is Hidden**


Despite being an active host, Kali’s MAC address is not displayed in the scan results.

This suggests that Kali might be configured to suppress MAC address broadcasting, possibly due to security settings.


3️⃣ **Windows Host Machine’s MAC Address is Not Displayed**


The host system running the VMs did not return a MAC address.

---

## 📡 *Wireshark Analysis - ARP & ICMP Behavior*  

Below is a *Wireshark capture* showing the ARP packet: 

![scan-2](https://github.com/user-attachments/assets/03985701-ce99-48aa-8ac7-278b719cea45)

### 🔹 *Observed Behavior:*  
1️⃣ *ICMP traffic is not visible* in Wireshark despite being expected.  
2️⃣ *Nmap defaults to ARP scanning* instead.  
3️⃣ *ARP requests successfully detect active hosts* in the local network.  

### 🔍 *Why ARP Over ICMP?*  
- *ARP is more efficient in local networks* where MAC addresses are used for communication.  
- *ICMP is useful for scanning across subnets*, but in a single local network, ARP is prioritized for efficiency.  
- *Nmap defaults to ARP scanning when possible*, as it provides more reliable results in LAN environments.  

### ✅ *Conclusion:*  
- **Nmap's -sP (ping scan) effectively identifies hosts using ARP** in local networks.  
- *ICMP scanning is deprioritized in favor of ARP*, making ARP the preferred method for discovering live hosts in the same subnet.

