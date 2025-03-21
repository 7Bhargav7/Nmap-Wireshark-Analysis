# *Nmap Scans & Wireshark Analysis*  
### Exploring Network Scanning & Traffic Analysis in a Local Virtual Lab  

## 📌 *Overview*  
This project documents *Nmap scanning experiments* and *Wireshark packet analysis, performed in a **self-hosted lab* using *Kali Linux* as the scanning system and *Metasploitable* as the target.  

The goal is to:  
- 🔍 *Understand different types of Nmap scans* and their impact on network traffic  
- 📊 *Analyze packet-level behavior* using Wireshark  
- 🔥 *Explore open ports in Metasploitable* and their security implications  

## 🛠 *Lab Setup*  
This project is based on a *static IP network setup* with:  
- 🖥 *Kali Linux* → Attacker/Scanner  
- 🖥 *Metasploitable* → Target with multiple open ports  
- 🌐 *Oracle VirtualBox* → Networking: *Host-Only Adapter*  

## 🔎 *Types of Nmap Scans Covered*  
Nmap categorizes ports into *6 states*, which are observed in this project:  
1. *🟢 Open* – The target is accepting connections.  
2. *🔴 Closed* – The target actively rejects connections.  
3. *🟡 Filtered* – The port is blocked by a firewall.  
4. *⚪ Unfiltered* – The port is accessible but Nmap can’t determine its state.  
5. *🟠 Open|Filtered* – Nmap can’t confirm if it’s open or filtered.  
6. *🔘 Closed|Filtered* – Nmap can’t confirm if it’s closed or filtered.  

### 🛡 *Key Nmap Commands Used*  
This project covers *16 essential Nmap commands* inspired by [Recorded Future's guide](https://www.recordedfuture.com/threat-intelligence-101/tools-and-techniques/nmap-commands), including:  

#### *🔹 Basic Scans*  
- nmap -sn → *Ping scan* (detect live hosts)  
- nmap -p- → *Scan all 65,535 ports*  
- nmap -sV → *Service/version detection*  

#### *🔹 Stealth Scans*  
- nmap -sS → *SYN scan (half-open scan, avoids detection)*  
- nmap -f → *Fragmented scan (bypass IDS/IPS)*  

#### *🔹 Aggressive & OS Detection*  
- nmap -A → *Aggressive scan (OS, services, scripts)*  
- nmap -O → *OS detection*  

#### *🔹 Firewall Evasion Techniques*  
- nmap -D → *Decoy scan*  
- nmap --data-length → *Adds random padding to evade firewalls*  

#### *🔹 UDP & Specific Port Scans*  
- nmap -sU → *UDP scan*  
- nmap -p → *Scan specific ports*  

## 🔥 *Common Ports in Metasploitable*  
Metasploitable has many *open ports by default*, including:  
- *FTP* (21)  
- *SSH* (22)  
- *Telnet* (23)  
- *SMTP* (25)  
- *HTTP* (80, 443)  
- *SMB* (445)  
- *PostgreSQL* (5432)  
- *More...*  

## 🖥 *Wireshark Analysis*  
Wireshark is used to *capture traffic from Nmap scans*, allowing deeper insight into:  
- *Packet handshakes & responses*  
- *How different scans interact with ports*  
- *Firewall & IDS/IPS behaviors*  

## 📂 *Structure of the Repository*  
📁 */scans/* → Nmap scan results & explanations  
📁 */wireshark/* → Packet captures & analysis screenshots  
📁 */README.md* → Overview of scans & findings  

## 🎯 *Goals of the Project*  
✅ *Learn* how different Nmap scans interact with *open & filtered ports*  
✅ *Observe* *packet-level behavior* using *Wireshark*  
✅ *Understand* how *firewalls & IDS* react to scans  
✅ *Document* findings for *future reference & learning*
