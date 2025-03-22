
# 🛠 Nmap Service Version scan (-sV) - Observation & Wireshark Analysis  

## 🖥 *Nmap Scan Output*  

Below is the command run and its corresponding output:

### 🔹 *Scan Command:*
![Scan-3](https://github.com/user-attachments/assets/b00840df-2005-4779-b5a9-7dc8d101968e)



## 🔍 Observation  

The scan checks for open TCP ports and then probes for specific services on common ports such as HTTPS, SSH, FTP, SMTP, MySQL, and SMB. After establishing a TCP connection using a full three-way handshake, Nmap sends a probe to interact with each detected service.

> Probe: A probe is a packet or set of packets sent by Nmap to a service to elicit a response, which helps identify the service's characteristics.



Based on the banner response received from each service, Nmap is able to determine key details.

> Banner Response: The banner is the initial data sent by a service when a connection is established. It typically reveals the service name, version number, and sometimes the underlying operating system or additional software details.


---


**TCP Three-Way Handshake:** Unlike the SYN scan (-sS), the service version scan (-sV) completes a full TCP connection (SYN → SYN-ACK → ACK) to ensure reliable data exchange.

**Service Probing:** After the connection is established on the common ports, Nmap sends probes to obtain a banner response from each service.

**Banner Analysis:** The received banner reveals valuable details including-

_**Service Name**_

_**Version Number**_

_**Operating System or Software Information**_



This detailed probing allows for a deeper understanding of the services running on the target machine.


---


## 📡 Wireshark Analysis - Service Detection (-sV)  

After running nmap -sV <target-ip>, Wireshark captures show TCP three-way handshakes, followed by probes interacting with detected services.

**HTTPS (443)** is the most common internet-facing service.

**SSH (22)** is widely used in internal networks and remote management.

Other frequently detected ports include:

**FTP (21)** → File transfer service.

**SMTP (25)** → Mail server communication.

**MySQL (3306)** → Database service.

**SMB (445)** → Windows file-sharing protocol.

🔹 Key Observations:

On Metasploitable hosted on  local network , SSH and SMB are more likely to be present, whereas HTTPS may not be as commonly availiable.


🔹 Wireshark Packet Captures:

1️⃣ HTTPS(443) - Hyper Text Transfer Protocol Secure


![scan-3-80,443](https://github.com/user-attachments/assets/5aed12aa-6b70-49ed-b63e-fbd9d7a830d9)


> Wireshark shows a TCP handshake followed by TLS negotiation, ensuring encrypted data exchange.



1️⃣ SSH (22) - Secure Shell Login


![scan-3-22](https://github.com/user-attachments/assets/2956aa03-ce35-48f7-ba86-2cff2e11716c)


> SSH provides secure encrypted remote access. Here, Wireshark shows a TCP handshake followed by a service probe.



2️⃣ SMB (445) - Windows File Sharing


![scan-3-445,139](https://github.com/user-attachments/assets/a7648f22-d21f-4202-86e4-12f383f3d940)


> SMB is used for file sharing. The scan reveals its presence and version details.



3️⃣ MySQL (3306) - Database Service


![scan-3-3306](https://github.com/user-attachments/assets/38bb3285-464a-465e-99d6-082d9ff00944)


> MySQL responses expose database version info, useful for fingerprinting.



4️⃣ FTP (21) - File Transfer Protocol


![scan-3-21](https://github.com/user-attachments/assets/83156a3f-4627-43f7-bf52-994046b09dc0)


> FTP servers respond with a banner revealing software details.



5️⃣ SMTP (25) - Mail Transfer


![scan-3-25,587](https://github.com/user-attachments/assets/ad227b5d-d512-4c9d-9fa1-f85a9272389e)


> SMTP scans reveal mail server details that may help in reconnaissance.




---

✅ This confirms that -sV scans actively probe services after detecting open TCP ports, using responses (banners) to identify software versions.
