# IR Report - SOC251 Quishing (QR Code Phishing)

## 1. Incident Summary
- Alert ID: 214
- Date/Time: Jan 01, 2024, 12:37 PM
- Analyst: Ritesh Ade
- Severity: Medium (escalate to High)
- Status: Closed - True Positive

## 2. Alert Details
- Alert Name: SOC251 Quishing Detected (QR Code Phishing)
- Source System: Exchange Email Gateway
- Affected User: Claire@letsdefend.io
- Initial Indicator: QR code in suspicious MFA email

## 3. Investigation Timeline
| Time | Action | Finding |
|------|--------|---------|
| 12:37 PM | Alert triggered | QR code phishing email detected |
| Investigation | IP lookup AbuseIPDB | 339 abuse reports, Canada |
| Investigation | Domain WHOIS lookup | microsecmfa.com never registered |
| Investigation | QR code decoded | Points to IPFS hosted phishing page |
| Investigation | VirusTotal URL scan | Multiple vendors flag as malicious |

## 4. IOC Analysis
- Sender IP: 158.69.201.47 - 339 abuse reports
- Sender Domain: microsecmfa.com - never registered, spoofed
- Phishing URL: https://ipfs.io/ipfs/Qmbr8wmr41C35c3K2GfiP2F8YGzLhYpKpb4K66KU6mLmL4#
- VirusTotal: Multiple vendor detections confirmed malicious
- Technique: IPFS hosting used to evade takedown and bypass filters

## 5. MITRE ATT&CK Mapping
- Tactic: Initial Access
- Technique ID: T1566.001
- Technique Name: Phishing - Spearphishing Link
- Sub-technique note: QR code used to bypass email URL scanners

## 6. Verdict
- TRUE POSITIVE
- Justification: Spoofed sender domain, IPFS hosted 
  phishing page confirmed malicious by multiple vendors, 
  email impersonates Microsoft using urgency and threats

## 7. Containment Recommendations
- Block sender IP 158.69.201.47 at email gateway
- Block IPFS phishing URL at web proxy
- Notify Claire@letsdefend.io not to scan the QR code
- Check if Claire device made any connections to the 
  IPFS URL after receiving the email
- Report phishing URL to VirusTotal community

## 8. Lessons Learned
- QR codes in emails bypass traditional URL scanners.
  Consider implementing QR code scanning at email gateway
- IPFS hosted phishing pages cannot be taken down.
  Block at proxy/firewall level instead
- MFA themed lures are highly effective. User awareness 
  training should specifically cover MFA phishing