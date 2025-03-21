# 🛠 Nmap Simple_Scan - Observation & Wireshark Analysis  

## 🔍 Observation  
Despite not using root privileges, Nmap Simple_Scan performed a **SYN scan (-sS), executing a *two-way handshake* instead of the default , a full **three-way handshake (-sT)** on Metasploitable.  

This indicates that:  
- The Metasploitable VM allows raw packet transmission.  
- User or system may have implicit permissions to send raw packets.
- A security policy or kernel setting might be enabling this behavior.
- Nmap may have been modified or configured differently in the Kali VM.

---

## 📡 Wireshark Analysis - Packet Capture  

Below is a *Wireshark capture* showing the two-way handshake:  
![scan-1](https://github.com/user-attachments/assets/d2f6cfdf-c846-4a55-bf77-0ea93cead9b7)
1️⃣ *Nmap sends a SYN packet*  
2️⃣ *Target responds with SYN-ACK*  
3️⃣ *Nmap sends a RST (Reset) instead of ACK* - Completing the *two-way handshake*   

Since the connection never completes with an ACK, it confirms that Nmap *did not establish a full connection* (i.e., no three-way handshake).  

---

✅ This validates that **Nmap performed a stealth SYN scan (-sS)** on Metasploitable without needing root privileges.
