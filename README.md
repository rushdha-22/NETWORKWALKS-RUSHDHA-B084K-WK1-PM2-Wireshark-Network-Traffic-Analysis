# Wireshark Network Traffic Analysis Labs

## Overview

This repository documents my hands-on practice in network traffic analysis and security investigation using Wireshark.

Through a series of practical SOC-based scenarios, I explored network packet capture, protocol analysis, suspicious traffic identification, authentication monitoring, TCP stream analysis, and VoIP traffic inspection.

The exercises helped develop practical skills in analysing network communications, identifying potential security threats, and understanding how sensitive information can be exposed through unencrypted protocols.

## Tools & Technologies

- Wireshark
- Windows 11
- TCP/IP Networking
- HTTP / HTTPS
- FTP
- TCP / UDP
- SIP / RTP
- Wireshark Display Filters
- Packet Capture and Analysis

---

## Lab 01 – TCP SYN Port Scan Detection

### Scenario
Investigated unusual traffic reported on a company's web server to identify the type of attack and determine the source of suspicious network activity.

### Tasks Performed
- Captured network traffic using Wireshark.
- Analysed TCP SYN packets to identify connection attempts.
- Identified suspicious traffic originating from a single source.
- Determined the targeted server.
- Examined TCP source and destination ports.
- Identified open and closed ports by analysing TCP responses.
- Distinguished between SYN-ACK and RST-ACK responses.
- Determined the type of network reconnaissance activity.

### Wireshark Filters Used

```text
tcp.flags.syn == 1
tcp.flags.syn == 1 && tcp.flags.ack == 0
tcp.flags.reset == 1
```

### Findings
- Identified 40 different ports probed.
- Found 3 open ports.
- Identified 37 closed ports.
- Open ports responded with SYN-ACK packets.
- Closed ports responded with RST-ACK packets.
- Identified the activity as a TCP SYN port scan.

### Key Learning
Understanding TCP connection establishment, SYN-based scanning, TCP response flags, port identification, and network reconnaissance techniques.

---

## Lab 02 – TCP Stream and Plain-Text Chat Analysis

### Scenario
Investigated an outdated office chat application that transmitted messages without encryption.

### Tasks Performed
- Analysed network traffic to distinguish web traffic from other TCP communication.
- Identified an application using a non-standard web communication port.
- Determined which computer initiated the TCP connection.
- Examined TCP stream information.
- Used Follow TCP Stream to reconstruct a chat conversation.
- Analysed communication between the client and server.
- Identified sensitive information transmitted through the chat application.
- Examined client-to-server and server-to-client communication.

### Wireshark Filters Used

```text
tcp.port == <application_port>
tcp.flags.syn == 1 && tcp.flags.ack == 0
```

### Findings
- Identified an unencrypted office chat communication.
- Reconstructed the conversation using TCP stream analysis.
- Observed that sensitive information was transmitted in readable plain text.
- Identified the security risks associated with unencrypted messaging.

Sensitive conversation contents and credentials are intentionally excluded from this repository.

### Key Learning
Understanding TCP streams, client-server communication, packet direction, and the importance of encryption in protecting sensitive communications.

---

## Lab 03 – HTTP Stream Analysis and Hidden Information Detection

### Scenario
Investigated company intranet traffic to identify a hidden message embedded within one of the webpages.

### Tasks Performed
- Captured and analysed HTTP traffic.
- Identified webpage requests using HTTP GET methods.
- Examined HTTP responses.
- Investigated TCP streams associated with individual webpages.
- Identified hidden information embedded in HTML source content.
- Recognised HTML comments that are not displayed in normal browser views.
- Examined HTTP response status codes.
- Analysed downloaded text files and their contents.

### Wireshark Filters Used

```text
http
http.request.method == "GET"
http.request.uri contains "download"
```

### Findings
- Identified a webpage containing a hidden HTML comment.
- Determined that the hidden information travelled from server to client.
- Identified the relevant TCP stream.
- Examined the HTTP response and its status code.
- Investigated a downloaded text file and its contents.

Hidden access codes, internal server details, and personal information are excluded.

### Key Learning
Understanding HTTP requests and responses, TCP stream reconstruction, HTML comments, HTTP status codes, and identifying information that may be overlooked during normal web browsing.

---

## Lab 04 – HTTP Authentication and Credential Exposure

### Scenario
Investigated an outdated staff portal using unencrypted HTTP to determine what information could be exposed during user authentication.

### Tasks Performed
- Analysed HTTP authentication traffic.
- Identified the protocol used during sign-in.
- Examined HTTP POST requests.
- Identified the login endpoint.
- Determined the number of authentication attempts.
- Inspected submitted form data.
- Identified the packet details section containing form parameters.
- Compared unencrypted HTTP communication with encrypted HTTPS traffic.

### Wireshark Filters Used

```text
http
http.request.method == "POST"
```

### Findings
- Identified HTTP as the protocol used for the sign-in process.
- Determined that authentication used the POST method.
- Identified multiple login attempts.
- Observed that submitted credentials were readable in unencrypted traffic.
- Identified HTTPS as the recommended solution to protect authentication data.

Actual usernames and passwords are intentionally redacted.

### Key Learning
Understanding HTTP authentication, POST requests, form data analysis, credential exposure, and the importance of HTTPS encryption.

---

## Lab 05 – FTP Brute-Force Attack Detection

### Scenario
Investigated repeated failed authentication attempts against an FTP server to identify suspicious login activity and determine whether authentication was eventually successful.

### Tasks Performed
- Examined FTP traffic using Wireshark.
- Identified the FTP server and the source of authentication attempts.
- Analysed FTP USER and PASS commands.
- Identified repeated username submissions.
- Examined FTP authentication response codes.
- Distinguished between failed and successful login responses.
- Investigated the successful authentication attempt.
- Identified the attack technique based on repeated password guessing.

### Wireshark Filters Used

```text
ftp
ftp.request.command == "USER"
ftp.request.command == "PASS"
ftp.response.code >= 500
ftp.response.code == 530
ftp.response.code == 230
```

### Findings
- Identified repeated FTP authentication attempts.
- Observed 24 failed login responses.
- Identified the FTP response code 530 for unsuccessful authentication.
- Identified response code 230 as successful authentication.
- Confirmed that one login attempt eventually succeeded.
- Classified the activity as a brute-force attack.

Actual usernames, passwords, and internal network identifiers are excluded.

### Key Learning
Understanding FTP authentication, protocol response codes, failed login monitoring, credential exposure, and brute-force attack detection.

---

## Lab 06 – VoIP Traffic Analysis and Call Reconstruction

### Scenario
Investigated a voice call transmitted through a company's VoIP system to identify the protocols involved and examine the information exchanged during the conversation.

### Tasks Performed
- Captured and analysed VoIP network traffic.
- Identified the call setup protocol.
- Examined SIP signalling messages.
- Identified RTP as the protocol carrying voice data.
- Analysed caller and receiver information.
- Examined RTP packet details and audio codec information.
- Used Wireshark's Telephony features to inspect and replay VoIP calls.
- Identified sensitive information communicated during the call.
- Evaluated the importance of encrypted voice communication.

### Wireshark Filters Used

```text
sip
rtp
sip.Method == "INVITE"
```

### Findings
- Identified SIP as the call setup protocol.
- Identified RTP as the voice transmission protocol.
- Identified the G.711 PCMU audio codec.
- Successfully reconstructed and replayed the captured VoIP conversation.
- Observed that unencrypted voice traffic could expose confidential spoken information.
- Identified Secure Real-Time Transport Protocol (SRTP) as a protection mechanism for voice traffic.

Personal identities, call details, and payment information are intentionally excluded.

### Key Learning
Understanding VoIP communication, SIP signalling, RTP packet analysis, audio codecs, call reconstruction, and the importance of SRTP encryption.

---

## Overall Skills Developed

Through these practical exercises, I developed experience in:

- Network packet capture and traffic inspection.
- TCP/IP protocol analysis.
- TCP connection and handshake analysis.
- Port scanning detection.
- Identifying suspicious network activity.
- HTTP and HTTPS traffic analysis.
- TCP stream reconstruction.
- FTP authentication monitoring.
- Brute-force attack identification.
- Credential exposure investigation.
- VoIP traffic analysis.
- SIP and RTP protocol inspection.
- Wireshark display filters and packet interpretation.
- Understanding network security controls and encryption.

## Conclusion

These practical Wireshark labs provided hands-on experience in investigating network traffic from a Security Operations Centre (SOC) perspective.

The exercises strengthened my understanding of network protocols, suspicious traffic patterns, authentication mechanisms, and the security risks associated with unencrypted communication.

They also highlighted the importance of network monitoring, secure communication protocols, and analysing packet-level evidence when investigating potential security incidents.

**Note:** This repository contains educational lab findings. Sensitive credentials, personal information, payment details, and internal network identifiers have been deliberately excluded to maintain security and privacy.
