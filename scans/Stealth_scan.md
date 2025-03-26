# 🔍 Nmap SYN Stealth Scan - Detailed Observation & Technical Analysis

## 📋 Overview
A comprehensive exploration of the SYN stealth scan technique, providing deep insights into network reconnaissance and port scanning methodologies.

## 🖥️ Initial Scan Command
![Scan-5](https://github.com/user-attachments/assets/a1c64299-cb4d-4b09-98a2-feda8798c95f)

```bash
nmap -sS -p 80,443 [target_ip]
```

> **💡 Pro Tip:**
> - The `-sS` flag enables SYN stealth scanning
> - `-p 80,443` specifies scanning web-related ports
> - Focuses on HTTP (80) and HTTPS (443) services

## 🕵️ Scanning Methodology
SYN stealth scan is a multi-stage process involving:
- Targeted port scanning
- Web service port reconnaissance
- Minimal network footprint

### 🔬 Scan Characteristics
| Characteristic | Description | Impact |
|---------------|-------------|--------|
| Port Selection | Specific web ports (80, 443) | Focused analysis |
| Connection Type | Half-open scan | Minimal network trace |
| Target Services | HTTP/HTTPS | Web infrastructure probing |

## 🌐 Detailed Scanning Stages

### 🔄 TCP SYN Stealth Scan Sequence
![scan-5](https://github.com/user-attachments/assets/b4bc810c-c726-40aa-9f12-a320dcf6c53d)

- **Web Port Targeting:**
  - Port 80: Standard HTTP
  - Port 443: Secure HTTPS
- **Packet 1 (SYN):** 
  - Initiates connection to specified web ports
  - Sends SYN packet without intent to complete
- **Packet 2 (SYN-ACK):**
  - Server responds to web service ports
  - Open ports indicate active web services
- **Packet 3 (RST):**
  - Immediately terminates connection
  - Prevents full TCP handshake
- **Wireshark Filter:** `tcp.port == 80 || tcp.port == 443`

## 🏁 Conclusion
SYN stealth scanning on web ports provides:
- Targeted web service discovery
- Minimal network detection
- Quick infrastructure mapping

> **🚨 Security Reminder:**
> Perform network scanning only with explicit authorization.
