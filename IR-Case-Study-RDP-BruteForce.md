# IR Report - SOC176 RDP Brute Force Detected

## 1. Incident Summary
- Alert ID: 234
- Date/Time: Mar 07, 2024, 11:44 AM
- Analyst: Ritesh Ade
- Severity: Medium (escalate to High)
- Status: Closed - True Positive

## 2. Alert Details
- Alert Name: SOC176 RDP Brute Force Detected
- Source System: Firewall and Endpoint Detection
- Affected Host: Matthew (172.16.17.148)
- Attacker IP: 218.92.0.56
- Protocol: RDP (port 3389)
- Initial Indicator: Multiple failed RDP logins from 
  single external IP targeting non-existing accounts

## 3. Investigation Timeline
| Time | Action | Finding |
|------|--------|---------|
| 11:44 AM | Alert triggered | RDP brute force detected |
| Investigation | AbuseIPDB check | 453051 reports - CHINANET China |
| Investigation | VirusTotal check | 9 vendors flagged malicious |
| Investigation | Log Management review | Failed attempts on admin, guest, sysadmin, Matthew |
| Investigation | Success check | EventID 4624 Logon Type 10 - Matthew compromised |
| Investigation | Post login review | RDP session maintained - firewall logs confirmed |
| Response | Containment | Matthew endpoint isolated |

## 4. IOC Analysis
- Attacker IP: 218.92.0.56
- ISP: CHINANET Jiangsu Province China
- AbuseIPDB reports: 453051 historical reports
- VirusTotal: 9 vendors flagged malicious
- Targeted host: 172.16.17.148 (Matthew)
- Targeted port: 3389 (RDP)
- Usernames attempted: admin, guest, sysadmin, Matthew
- Compromised account: Matthew
- Successful login: EventID 4624 Logon Type 10 confirmed

## 5. MITRE ATT&CK Mapping
- T1110 - Brute Force
- T1078 - Valid Accounts
- T1021.001 - Remote Services - Remote Desktop Protocol

## 6. Verdict
- TRUE POSITIVE
- Justification: Attacker successfully authenticated via 
  RDP after brute forcing Matthew account credentials. 
  EventID 4624 Logon Type 10 confirms active remote 
  interactive session from known malicious Chinese IP.

## 7. Containment Actions Taken
- Endpoint Matthew isolated via containment toggle
- RDP session terminated by isolation
- All IOCs added to case artifacts

## 8. Recommendations
- Reset Matthew account password immediately
- Assume all data on Matthew endpoint is compromised
- Block 218.92.0.56 and entire CHINANET IP range at firewall
- Disable RDP on all endpoints that do not require it
- Implement RDP access only via VPN for authorised users
- Enable Network Level Authentication on all RDP services
- Implement account lockout policy after 5 failed attempts
- Deploy geo-blocking for RDP traffic from high risk countries
- Review all other endpoints for similar brute force attempts
  from same IP or IP range

## 9. Lessons Learned
- RDP exposed directly to the internet is extremely high risk.
  Any machine with port 3389 open to external traffic will 
  be targeted within hours of exposure.
- AbuseIPDB confidence score of 0 percent does not indicate 
  a safe IP. Always check total report count alongside the 
  confidence score. 453051 reports is unambiguous.
- Logon Type 10 in EventID 4624 specifically indicates 
  Remote Interactive logon via RDP. Knowing logon types 
  is essential for RDP investigation triage.
- Account lockout policies and geo-blocking for RDP are 
  the two most effective preventive controls against 
  this attack type.