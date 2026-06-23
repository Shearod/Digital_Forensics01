<h1> Digital Forensics Lab</h1>



<h2>Description</h2>
In this lab, I used Wireshark to analyze network traffic and identify potentially suspicious activity within a packet capture (PCAP) file. The investigation focused on detecting beaconing behavior, examining HTTP and FTP communications, and identifying Remote Desktop Protocol (RDP) connection attempts.
<br />


## Languages and Utilities Used
- Wireshark
- Windows 10
- PCAP Network Capture File

## Objectives

- Analyze network traffic using Wireshark
- Identify potential beaconing behavior
- Investigate FTP authentication traffic
- Detect RDP connection attempts
- Document findings and security observations

## Install Wireshark 
<img width="1245" height="498" alt="Download Wireshark" src="https://github.com/user-attachments/assets/d4923ea8-8204-429f-94a0-f0c94d76e50d" />


Keep Default Installation Options
<img width="1004" height="535" alt="Keep Default Install Options" src="https://github.com/user-attachments/assets/0fa751ca-6625-4d33-96df-7d87e81ddbfc" />

## Open Packet Capture
<img width="1340" height="641" alt="Wireshark Window" src="https://github.com/user-attachments/assets/cbe6115e-d2c4-4943-abde-11b2da825982" />
Scroll through the packet list and find what looks normal, repeated events, and events that stand out.

## Use Display Filters
<img width="1219" height="572" alt="DNS Filter" src="https://github.com/user-attachments/assets/07e449dd-277c-4917-9ef6-2d75b26b9981" />
<img width="1291" height="596" alt="httprequestfilter" src="https://github.com/user-attachments/assets/afcef1bb-7ec0-46f0-a429-d963632bc3bd" />
Filtering is useful because you can see one category of traffic at a time, which makes it easier to scan for patterns.

## Filter One IP at a Time
<img width="1366" height="388" alt="IP Filter 5610" src="https://github.com/user-attachments/assets/b95aed24-c5d1-4bac-a72b-dd0924deffc4" />
<img width="1128" height="443" alt="IP Filter5620 (3389)" src="https://github.com/user-attachments/assets/5f99b072-70c6-4588-994d-1d6c70467e41" />

## Scenario A: Repeated Check-In
<img width="1034" height="330" alt="Repeated Check In" src="https://github.com/user-attachments/assets/b782ff89-c1ec-4fa4-9018-d9e8992d1c9c" />

**Identify the internal system that repeatedly contacts the same outside system:**
- Finding: Possible beaconing from 192.168.56.10
- Evidence: Repeated HTTP GET /status traffic to 203.0.113.10 at regular intervals
- Reasoning: Timing and repeated destination look more automated than normal browsing
- Action: Preserve evidence and inspect the responsible process
- Next check: Review host logs and identify what launched the communication

  ## Scenario B: Service Targeting
  <img width="1046" height="325" alt="Scneario B Service Targeting" src="https://github.com/user-attachments/assets/ca13bebd-72d7-4a81-8803-64262895a6f2" />

  **Identify the system that repeatedly targets the same internal service:**
- Finding: Suspected RDP attack activity against 192.168.56.20
- Evidence: 6 Repeated TCP 3389 connection attempts from 192.168.56.50 in a short burst
- Reasoning: Repeated service targeting suggests automated or repeated access attempts
- Action: Review authentication logs and protect the target service
- Next check: Determine whether any logon succeeded

## Scenario C: OUtbound Upload
<img width="1130" height="311" alt="Scenario C" src="https://github.com/user-attachments/assets/b2348e3a-f15c-4d62-90a7-6e6c4909fbd0" />

**Identify the outbound file transfer activity:**
- Finding: Possible FTP-based data exfiltration from 192.168.56.10
- Evidence: FTP commands show an outbound upload and Sysmon shows archive creation plus ftp.exe activity
- Reasoning: the file creation and outbound transfer line up closely in time
- Action: preserve evidence and determine what data was prepared for upload
- Next check: inspect the ZIP file contents and validate whether the destination was authorized

## Comparisons
<img width="1098" height="416" alt="CSV file analysis" src="https://github.com/user-attachments/assets/b179d65d-c3d2-42ec-b707-a1cacf51ddc0" />
(⬆Compared packet capture to CSV log)

<br />




<img width="1307" height="188" alt="NDJSON LOG" src="https://github.com/user-attachments/assets/4b19a4ec-b127-4e73-a6da-89d625e715e6" />
(⬆Compared packet capture to NDJSON log)





<img width="872" height="396" alt="SYSMON SAMPLE" src="https://github.com/user-attachments/assets/39c22281-9c61-410b-adb6-c66feb5b0419" />
(⬆ Host Side Evidence)

