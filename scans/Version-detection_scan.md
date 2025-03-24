# 🛠 Nmap Service Version Scan (-sV) - Detailed Observation & Wireshark Analysis

## 📋 Initial Scan Overview

![Nmap Scan Command](https://github.com/user-attachments/assets/b00840df-2005-4779-b5a9-7dc8d101968e)

```bash
nmap -sV <target-ip>
```

> **💡 Key Insights:**
> - `-sV` flag enables service and version detection
> - Completes full TCP three-way handshake
> - Probes services to extract detailed information

## 🕵️ Scanning Methodology

### 🔬 Service Detection Process

1. **TCP Three-Way Handshake**
   - Establishes full TCP connection
   - Ensures reliable data exchange
   - Unlike SYN scan, completes full connection

2. **Service Probing**
   - Sends targeted probes to open ports
   - Retrieves banner responses
   - Extracts critical service information

### 🎯 Common Service Targets

| Port | Service | Protocol | Purpose |
|------|---------|----------|---------|
| 22   | SSH     | Secure Shell | Remote Access |
| 21   | FTP     | File Transfer | File Sharing |
| 25   | SMTP    | Mail Transfer | Email Communication |
| 443  | HTTPS   | Secure Web | Encrypted Web Traffic |
| 3306 | MySQL   | Database | Data Management |
| 445  | SMB     | File Sharing | Windows Network |

## 🌐 Detailed Wireshark Analysis

### 1️⃣ HTTPS (Port 443)
![HTTPS Scan](https://github.com/user-attachments/assets/5aed12aa-6b70-49ed-b63e-fbd9d7a830d9)

- **Key Characteristics:**
  - TCP Handshake
  - TLS Negotiation
  - Encrypted Data Exchange

### 2️⃣ SSH (Port 22)
![SSH Scan](https://github.com/user-attachments/assets/2956aa03-ce35-48f7-ba86-2cff2e11716c)

- **Key Characteristics:**
  - Secure Remote Access
  - Encrypted Communication
  - Service Version Probe

### 3️⃣ SMB (Port 445)
![SMB Scan](https://github.com/user-attachments/assets/a7648f22-d21f-4202-86e4-12f383f3d940)

- **Key Characteristics:**
  - Windows File Sharing
  - Version Detection
  - Network Resource Sharing

### 4️⃣ MySQL (Port 3306)
![MySQL Scan](https://github.com/user-attachments/assets/38bb3285-464a-465e-99d6-082d9ff00944)

- **Key Characteristics:**
  - Database Service Identification
  - Version Fingerprinting
  - Service Details Exposure

### 5️⃣ FTP (Port 21)
![FTP Scan](https://github.com/user-attachments/assets/83156a3f-4627-43f7-bf52-994046b09dc0)

- **Key Characteristics:**
  - File Transfer Protocol
  - Software Banner Reveal
  - Version Information

### 6️⃣ SMTP (Port 25)
![SMTP Scan](https://github.com/user-attachments/assets/ad227b5d-d512-4c9d-9fa1-f85a9272389e)

- **Key Characteristics:**
  - Mail Server Communication
  - Reconnaissance Potential
  - Service Details Extraction

## 🏁 Conclusion

**Nmap -sV Scan Provides:**
- Comprehensive service identification
- Detailed version information
- Insights into network infrastructure

> **🚨 Security Warning:** 
> Always obtain explicit permission before performing network scans. Unauthorized scanning may violate legal and ethical standards.

## 📚 Key Takeaways

1. Service version scans go beyond port detection
2. Banner responses reveal critical system information
3. Wireshark offers granular insights into service interactions
4. Ethical reconnaissance requires precision and consent
