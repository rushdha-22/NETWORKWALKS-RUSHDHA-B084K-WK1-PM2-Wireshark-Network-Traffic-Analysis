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
Analyse captured network traffic to identify and investigate a TCP SYN port scanning activity.

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
- `Lab 01.1` – TCP SYN scan traffic analysis
- `Lab 01.2` – Port scan response analysis

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
- Sensitive information could be exposed to anyone able to capture and inspect the traffic.

### Wireshark Filters
```text
tcp.port == <application_port>
tcp.flags.syn == 1
```

### Screenshots
- `Lab 02.1` – TCP chat traffic identification
- `Lab 02.2` – Reconstructed TCP conversation

---

## Lab 03 – HTTP Stream Analysis and Hidden Information Detection

### Objective
Inspect HTTP traffic to identify hidden information and understand how data can be retrieved from network streams.

### Tasks Performed
- Analysed HTTP requests and responses.
- Examined website traffic and page contents.
- Used **Follow TCP Stream** to inspect communication.
- Identified information contained in an HTML comment.
- Examined server-to-client communication.
- Analysed an HTTP response and file download.

### Key Findings
- Hidden information was identified within an HTML comment.
- Server-to-client communication contained additional information.
- An HTTP response with status code 200 indicated a successful request.

### Wireshark Filters
```text
http
http.request.method == "GET"
http.request.uri contains "download"
```

### Screenshots
- `Lab 03.1` – HTTP traffic and stream inspection
- `Lab 03.2` – Hidden information and HTTP response analysis

---

## Lab 04 – HTTP Authentication and Credential Exposure

### Objective
Investigate HTTP login traffic and understand the security risks of transmitting authentication information without encryption.

### Tasks Performed
- Identified HTTP login requests.
- Examined POST request methods.
- Inspected form-submission data.
- Analysed multiple login attempts.
- Identified exposed authentication information.
- Recommended HTTPS to protect login credentials.

### Key Findings
- Login information was transmitted over unencrypted HTTP.
- Authentication data could be inspected through packet analysis.
- HTTPS is recommended to protect credentials during transmission.

### Wireshark Filters
```text
http
http.request.method == "POST"
```

### Screenshots
- `Lab 04.1` – HTTP login request analysis
- `Lab 04.2` – Authentication data inspection

---

## Lab 05 – FTP Brute-Force Attack Detection

### Objective
Analyse FTP traffic to identify repeated login attempts and detect potential brute-force activity.

### Tasks Performed
- Identified FTP communication.
- Examined USER and PASS commands.
- Analysed repeated authentication attempts.
- Investigated FTP response codes.
- Identified failed and successful login responses.
- Classified the activity as a potential brute-force attack.

### Key Findings
- 24 failed login attempts were identified.
- FTP response code 530 indicated failed authentication.
- FTP response code 230 indicated successful authentication.
- The traffic pattern was consistent with brute-force activity.

### Wireshark Filters
```text
ftp
ftp.request.command == "USER"
ftp.request.command == "PASS"
ftp.response.code >= 500
ftp.response.code == 530
ftp.response.code == 230
```

### Screenshots
- `Lab 05.1` – FTP authentication attempts
- `Lab 05.2` – FTP response codes and login analysis

---

## Lab 06 – VoIP Traffic Analysis and Call Reconstruction

### Objective
Analyse Voice over IP (VoIP) traffic to understand call signalling, voice transmission, and potential information exposure.

### Tasks Performed
- Identified SIP signalling traffic.
- Examined call establishment messages.
- Analysed RTP voice traffic.
- Identified the audio codec used.
- Used Wireshark's Telephony features to inspect and reconstruct audio.
- Identified the security risks of transmitting voice communication without encryption.

### Key Findings
- SIP was used for call signalling.
- RTP was used to transport voice data.
- The G.711 PCMU codec was identified.
- Voice communication could be reconstructed from captured RTP traffic.
- Secure RTP (SRTP) is recommended to protect voice data.

### Wireshark Filters
```text
sip
rtp
sip.Method == "INVITE"
```

### Screenshots
- `Lab 06.1` – SIP signalling and call establishment
- `Lab 06.2` – RTP traffic and VoIP analysis

---

## Skills Developed

- Network Traffic Analysis
- Packet Capture and Inspection
- TCP/IP Protocol Analysis
- TCP SYN Port Scan Detection
- HTTP Traffic Inspection
- TCP Stream Reconstruction
- Authentication and Credential Exposure Analysis
- FTP Brute-Force Detection
- SIP and RTP Traffic Analysis
- Wireshark Display Filters
- Basic SOC Investigation and Threat Identification

## Conclusion

These practical labs provided hands-on experience in analysing network traffic and identifying suspicious activities using Wireshark. They strengthened my understanding of network protocols, common attack techniques, security weaknesses, and the importance of encrypted communication.

## Privacy and Security

Screenshots and documentation are intended for educational and portfolio purposes. Sensitive information, including credentials, personal details, internal network addresses, and other confidential data, has been excluded or redacted before publication.
