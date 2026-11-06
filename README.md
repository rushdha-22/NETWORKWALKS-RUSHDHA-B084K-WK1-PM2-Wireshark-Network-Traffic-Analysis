# Wireshark Network Traffic Analysis

## Overview

This repository documents my practical experience in analysing network traffic using **Wireshark** through a series of SOC-focused lab exercises provided by Networkwalks.

The labs cover network reconnaissance, TCP analysis, HTTP traffic inspection, credential exposure, FTP brute-force detection, and VoIP traffic analysis.

## Tools Used
- Wireshark
- Network packet capture (PCAP) files
- TCP/IP and application-layer protocols

---

## Lab 01 – TCP SYN Port Scan Detection

### Objective
Analyse captured network traffic to identify and investigate TCP SYN port scanning activity.

### Tasks Performed
- Captured and analysed network packets.
- Identified TCP SYN requests sent to multiple ports.
- Examined SYN-ACK and RST-ACK responses.
- Distinguished between open and closed ports.
- Identified the activity as a TCP SYN port scan.

### Key Findings
- 40 ports were probed.
- 3 ports were identified as open.
- 37 ports were identified as closed.
- The activity was classified as a TCP SYN (half-open) port scan.

### Wireshark Filters
```text
tcp.flags.syn == 1
tcp.flags.syn == 1 && tcp.flags.ack == 0
tcp.flags.reset == 1
```

### Screenshots

![Lab 01.1](./Lab%2001.1.png)

![Lab 01.2](./Lab%2001.2.png)

---

## Lab 02 – TCP Stream and Plain-Text Chat Analysis

### Objective
Investigate unencrypted TCP communication and examine how sensitive information can be exposed through plain-text network traffic.

### Tasks Performed
- Identified TCP communication associated with a chat application.
- Examined the connection initiation process.
- Used **Follow TCP Stream** to reconstruct the conversation.
- Analysed client-to-server and server-to-client messages.
- Identified the security risks of transmitting information without encryption.

### Key Findings
- Chat communication was transmitted over TCP.
- Conversation contents were readable in plain text.
- Sensitive information could be exposed through packet inspection.

### Wireshark Filters
```text
tcp.port == <application_port>
tcp.flags.syn == 1
```

### Screenshots

![
