# 🛠 Nmap OS Scan (-O) - Observation & Wireshark Analysis

## 🖥 Nmap Scan Output

Below is the command run and its corresponding output:

### 🔹 Scan Command:
![Scan-4](https://github.com/user-attachments/assets/b660e5b6-97d2-47b1-80be-a609d9c189ef)


> *Example Command*:  
> sudo nmap -O 192.168.56.103
> 
> This command performs an OS detection scan, trying multiple probes to guess the target’s operating system.

---

## 🔍 Observation

The OS scan begins by discovering open TCP ports (using a stealth approach) and then sends a variety of *fingerprinting probes* to determine the operating system. These probes check how the target responds to different TCP flag combinations, window sizes, and unusual protocols.

> *Probe: A probe here is any **crafted packet* (e.g., with unusual flags or window sizes) sent by Nmap to elicit unique responses that help identify the target OS.

- *TCP SYN Stealth*: Nmap first sends SYN packets to find open ports without completing a full handshake.  
- *NULL, FIN, and XMAS Scans*: Nmap tests how the target responds to unusual or malformed TCP packets.  
- *Window Size & MSS*: Different OSes have characteristic default values for these fields.  
- *TCP Timestamp & ICMP*: Nmap checks for timestamps and “Protocol Unreachable” responses to refine OS guesses.  
- *Duplicate ACKs*: Sometimes triggered by the unusual packet flows Nmap sends.

By correlating all these responses against its internal database, Nmap estimates the target OS with varying confidence levels.

---

# 📡 Wireshark Analysis - OS Detection (-O)

Below are the *key steps* of an OS scan, along with how each step appears in Wireshark.  
(You can insert your own screenshots for each step.)

---

## 1️⃣ TCP SYN & SYN-ACK (Stealth Scan Phase)

![scan-4-1](https://github.com/user-attachments/assets/6181c49b-0347-4a92-945a-e48f45811178)


> *What Happens*  
> - Nmap sends *SYN* packets to multiple ports.  
> - *Open ports* reply with *SYN-ACK*.  
> - *Closed ports* reply with *RST-ACK*.  
> - Nmap *does not complete* the handshake for open ports (it sends an RST to remain stealthy).

> *Wireshark Filter*  
> tcp.flags.syn == 1
> 
> This captures all SYN packets (including SYN-ACK replies).

*Key Observation*:  
- The target’s SYN-ACK indicates an open port.  
- The immediate RST from Nmap prevents a full TCP connection.

---

## 2️⃣ NULL, FIN, and XMAS Scans

![Scan-4-win-2](https://github.com/user-attachments/assets/0a01a7e2-f443-4e36-9859-3dcd4376153d)

![Scan-4-FIN-3](https://github.com/user-attachments/assets/54814dac-5447-4870-92ba-3aa85ef18946)

![Scan-4-Xmas-4](https://github.com/user-attachments/assets/c51f6c14-05a4-4c10-86e8-a5554c93d673)

> *What Happens*  
> - *NULL Scan: Packet with **no TCP flags* set.  
> - *FIN Scan: Packet with **only FIN* flag.  
> - *XMAS Scan: Packet with **FIN, URG, and PSH* flags set.  
>  
> Each OS reacts differently to these odd packets, helping Nmap fingerprint the OS.

> *Wireshark Filters*  
> - *NULL Scan*  
>   tcp.flags == 0x000
>     
> - *FIN Scan*  
>   tcp.flags.fin == 1 && tcp.flags.ack == 0
>     
> - *XMAS Scan*  
>   tcp.flags==0x29
>   

*Key Observation*:  
- *Linux/Unix-like systems* often ignore NULL/FIN/XMAS probes (no response if port is open).  
- *Windows* typically sends *RST* on receiving these packets if the port is closed.

---

## 3️⃣ Window Size & MSS Probes

![window_probe-scan-4](https://github.com/user-attachments/assets/0a79e900-0856-4d78-a943-3be648f52596)


> *What Happens*  
> - Nmap sends *SYN packets* with various *window sizes*.  
> - The target responds with characteristic *initial window sizes* and *MSS (Maximum Segment Size)* values that are typical for its operating system.

> *Wireshark Filter*  
> tcp.flags.syn==1 && tcp.window_size==5840
> 
> This helps isolate the packets where Nmap is analyzing window size and MSS values.

*Key Observation*:  
- *Windows OS* might reply with default window sizes such as *8192* or *65535*.  
- *Linux-based systems (current system - Metasploitable2)* might use different values (e.g., *5840* or *14600*), aiding in differentiating between operating systems.

---

## 4️⃣ TCP Timestamp Analysis

![image](https://github.com/user-attachments/assets/44c86cdc-3dc8-4c95-a321-5d04966b0d53)


> *What Happens*  
> - Nmap checks for *TCP timestamps* in the responses.  
> - These timestamps can provide information about the target’s uptime and are characteristic of certain OS implementations.

> *Wireshark Filter* 
> tcp.options.timestamp
> 
> This filter displays packets that include TCP timestamp options.

*Key Observation*:  
- The presence and behavior of TCP timestamps help in refining the OS fingerprint.  
- Some systems may disable timestamps, which is also a notable observation for OS detection.

---

## 5️⃣ Duplicate ACKs & Retransmissions

![image](https://github.com/user-attachments/assets/2a78e2fa-3beb-445a-8878-58443faa28bb)


> *What Happens*  
> - During the OS scan, Nmap’s unusual packet sequences can sometimes trigger *duplicate ACKs* from the target.  
> - *Retransmissions* might occur as the target attempts to process unexpected packets. In this case due to low packet loss it is not carried out thus restransmission filters run empty searches

> *Wireshark Filters*  
> - *Duplicate ACKs*  
>   tcp.analysis.duplicate_ack
>     
> - *Retransmissions*  
>   tcp.analysis.retransmission
>   

*Key Observation*:  
- Duplicate ACKs and retransmissions are artifacts of Nmap's aggressive probing and can provide additional clues to the target's TCP/IP stack behavior.
- They contribute to the overall fingerprint used by Nmap to determine the operating system.

---

## Conclusion

By correlating the responses observed in each step—*SYN/SYN-ACK handshakes, NULL/FIN/XMAS scans, window size & MSS values, TCP timestamps, and duplicate ACKs/retransmissions*—Nmap builds a comprehensive fingerprint of the target's TCP/IP stack. These unique behaviors, when compared against its internal database, allow Nmap to estimate the target's operating system with a certain level of confidence.

> *Final Note:*  
> The detailed analysis provided by these steps not only helps in OS detection but also offers valuable insights into the network stack behavior of the target system. This information is essential for network reconnaissance and security assessments.

---
