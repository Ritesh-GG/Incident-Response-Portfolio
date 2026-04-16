# Incident Response Portfolio

## Overview
SOC alert investigations completed on LetsDefend, a real 
world SOC simulation platform. Each case study follows a 
structured IR methodology aligned to NIST IR lifecycle 
and MITRE ATT&CK framework.

## Investigations Completed

| Alert | Scenario | MITRE Techniques | Verdict |
|-------|----------|-----------------|---------|
| SOC251 | Quishing - QR Code Phishing | T1566.001 Phishing | True Positive |
| SOC153 | Suspicious PowerShell Script | T1059, T1071, T1027, T1105 | True Positive |
| SOC176 | RDP Brute Force | T1110, T1078, T1021.001 | True Positive |

## Investigation Highlights

### SOC251 - Quishing Attack
Investigated a QR code phishing email impersonating 
Microsoft MFA setup. Decoded QR code revealed an IPFS 
hosted phishing page confirmed malicious by multiple 
VirusTotal vendors. Sender domain was unregistered and 
spoofed. Closed as True Positive.

### SOC153 - Azorult Infostealer
Investigated a suspicious PowerShell script downloaded 
via Chrome from an S3 bucket. File hash confirmed as 
Azorult infostealer by 33/62 VirusTotal vendors. Fileless 
second stage payload executed in memory via IEX technique. 
C2 callback to 91.236.116.163 confirmed with HTTP 200 
response. Endpoint isolated. Closed as True Positive.

### SOC176 - RDP Brute Force
Investigated RDP brute force from CHINANET IP 218.92.0.56 
with 453051 AbuseIPDB reports. Attacker successfully 
authenticated as Matthew after 9-10 failed attempts. 
EventID 4624 Logon Type 10 confirmed active RDP session. 
Endpoint isolated. Closed as True Positive.

## IR Report Template
Reusable IR report template following NIST IR lifecycle 
covering Detection, Analysis, Containment, Eradication, 
Recovery and Lessons Learned phases.

## Tools Used
- LetsDefend SOC simulation platform
- VirusTotal for hash, URL and IP analysis
- AbuseIPDB for IP reputation checking
- URLScan.io for URL analysis
- ZXing QR code decoder
