# Phishing-Led Multi-Stage Attack Simulation and End-to-End SOC Investigation
###### (Email Security → Identity Protection → Endpoint Security)

## Objective:
The objective of this project was to simulate a complete real-world attack lifecycle and gain hands-on experience in detecting, analyzing, and responding to a phishing-led compromise across multiple security layers.

This exercise focused on understanding how an attack progresses from email delivery to identity compromise and finally endpoint exploitation, while validating detection capabilities within Microsoft Defender for Office 365 and Microsoft Defender for Endpoint.

## Project Overview:
This project simulates a full attack chain beginning with a phishing email and progressing through identity compromise and endpoint intrusion. The scenario demonstrates how modern attacks bypass multiple security layers using social engineering, credential theft, and post-compromise execution techniques.

The attack was executed in three stages:
- Phishing email delivery and malicious URL interaction
- Credential compromise and impossible travel sign-in simulation
- Endpoint compromise through malicious execution activity on a Windows system

The investigation included validating alerts in Microsoft Defender XDR, analyzing sign-in anomalies, and executing endpoint-based attack simulations to replicate attacker behavior.

### Tools Used:
- Microsoft Defender for Office 365 (Safe Links, Email Protection)
- Microsoft Entra ID (Identity Protection / Sign-in Logs)
- Microsoft Defender for Endpoint (EDR)
- Microsoft Defender XDR Portal
- Windows 11 Virtual Machine
- Windows Server 2022 Virtual Machine
- PowerShell
- VPN (for geo-location simulation)
- MITRE ATT&CK Framework

### Skill Developed:
- Phishing attack simulation and analysis
- Email security and Safe Links behavior understanding
- Identity compromise investigation
- Impossible travel / risky sign-in analysis
- Endpoint detection and response (EDR) analysis
- PowerShell-based attack execution analysis
- Credential harvesting simulation
- MITRE ATT&CK mapping
- SOC alert triage and investigation

### Key Deliverables:
- End-to-end phishing attack simulation (Email → Identity → Endpoint)
- Identity compromise and impossible travel scenario validation
- Endpoint compromise using PowerShell and credential dumping simulation
- Microsoft Defender XDR incident investigation
- Attack chain correlation across multiple security layers
- Detection validation and alert analysis report

## Steps Performed:

### STEP 1: Phishing Email (Email Security Simulation)
- A phishing email was sent to user Jenny’s mailbox from a random external sender.
- Microsoft Defender Safe Links rewrote the embedded malicious URL for protection tracking.
- The user clicked the rewritten link, which redirected to a DocuSign-like credential harvesting page.
- Jenny entered her username and password, simulating credential theft.
- This stage represented initial access via phishing and social engineering.

📌 Refer to the below screenshots for policy configuration and summary details.




### STEP 2: Hijacking Identity (Identity Protection & Impossible Travel Simulation)
- Logged into a Windows Server 2022 VM using VPN to simulate access from the Netherlands.
- Successfully signed into Jenny’s mailbox without MFA enforcement (Security Defaults disabled in prior setup).
- Performed additional sign-in attempts from a local machine to simulate impossible travel behavior.
- Successfully authenticated into Jenny’s mailbox from multiple geographic locations.
- Established remote access to the Windows 11 VM using RDP with Jenny’s compromised credentials.
- Modified the hosts file to map the Windows 11 system hostname.
- Used advanced RDP settings:
    - “Use a web account to sign in to the remote computer”
- Connected using hostname-based RDP access to simulate attacker persistence and access.

📌 Refer to the below screenshots for policy summary and configuration settings.


### STEP 3: Compromising Endpoints (Endpoint Threat Simulation)
- On the Windows 11 endpoint (Jenny’s machine), PowerShell was used to simulate attacker activity.
- Executed a script to deploy and run Mimikatz, simulating credential dumping behavior.
- Verified execution by locating artifacts in the %TEMP% directory.
- Ran Mimikatz to simulate extraction of credentials from LSASS memory.
- Executed Atomic Red Team technique T1059.001 (PowerShell execution simulation).
- Microsoft Defender for Endpoint generated alerts under Incidents & Alerts.
- Verified detection and correlation in the Microsoft Defender XDR portal.

📌The below screenshots demonstrate policy enforcement and inspection results within Microsoft Defender.


### Attack Flow Summary:
- Email Security: Phishing email delivered → malicious URL clicked → credential capture simulated
- Identity Protection: Credentials used for login → risky sign-ins → impossible travel detection simulated
- Endpoint Security: RDP access gained → PowerShell execution → credential dumping simulation → lateral movement behavior



### Email Investigation and Threat Analysis:
- Initiated an investigation using Microsoft Defender for a suspicious email alert.

#### Email Analysis Workflow:
- Navigated to: Email & collaboration → Explorer
- Extracted and analyzed the email message header for forensic inspection.
- Parsed key header fields using Notepad++ for structured review, including:
  - Received chain (mail routing path)
  - Authentication-Results (SPF/DKIM/DMARC validation)
  - From address
  - Message-ID
  - Return-Path
  - X-Forefront-Antispam-Report

📌 Below are the screenshots captured during the Email Workflow Analysis:
<img width="749" height="317" alt="image" src="https://github.com/user-attachments/assets/fdaca9c9-835b-4cb7-80cf-f1c9a2e992fa" />
<img width="748" height="418" alt="image" src="https://github.com/user-attachments/assets/62abcffd-af78-4f77-b29b-178c9fb39453" />
<img width="751" height="431" alt="image" src="https://github.com/user-attachments/assets/7a65c3e8-4909-4499-ab90-13199f030b59" />

#### Threat Intelligence Correlation (OSINT):
- Investigated embedded URL using VirusTotal.
  - URL was flagged as malicious by 5 security vendors.
- Performed OSINT analysis on source IP address: 79.135.106.97
  - IP had prior malicious reports. (last seen ~5 months ago)
  - Associated with suspicious activity patterns consistent with phishing infrastructure.

📌 Below are the screenshots of the OSINT performed:
<img width="750" height="412" alt="image" src="https://github.com/user-attachments/assets/51c431c0-4be2-449b-8081-a90c1a128be9" />
<img width="749" height="457" alt="image" src="https://github.com/user-attachments/assets/950fa6c8-9d41-494a-b4c6-fe89911c637a" />

### Incident Response Action:
- Based on corroborated OSINT findings and Defender telemetry:
  - Confirmed email contained malicious URL and suspicious origin infrastructure.
  - Executed remediation by deleting the email from user mailboxes.
  - Prevented further user interaction with the phishing content.

 📌 Screenshot as below:
 
<img width="749" height="412" alt="image" src="https://github.com/user-attachments/assets/bad41887-5f9b-412a-a7af-0dd5a54e033f" />


## SOC Phishing Investigation Report:

### Incident Overview:
- Timestamp: June 18, 2026 – 21:04 (UTC +04:00)
- Recipient: bob@corp88[.]onmicrosoft[.]com
- Subject: Salary Revision
- Sender Email: strangeaccount88@proton[.]me
- Sender IP Address: 79.135.106.97
- Attachment: Salary Revision[.]docx
- Embedded URL: hxxps[://]shareholds[.]com/nam/…

A phishing email impersonating an HR-related salary update was delivered to the target mailbox. The message contained both a malicious document attachment and a credential-harvesting URL designed to prompt user interaction.

### Indicators of Compromise (IOCs):
- Malicious URL: Flagged by VirusTotal as malicious across multiple security vendors.
- Sender IP (79.135.106.97): Reported as malicious on AbuseIPDB.
- Phishing Infrastructure: External ProtonMail sender used to deliver payload.

### Investigation Summary:
- At 21:04 UTC+04:00 on June 18, 2026, a phishing email titled “Salary Revision” was delivered to the organization’s mailbox. The email leveraged a social engineering lure related to payroll updates and contained:
  - A Microsoft Word attachment (Salary Revision[.]docx).
  - A malicious URL intended to redirect the user to an external resource.
- OSINT validation confirmed multiple malicious indicators associated with both the URL and the sender infrastructure. VirusTotal detections classified the URL as malicious, while AbuseIPDB reports confirmed prior malicious activity associated with the source IP address.
- Further investigation is required to determine:
  - Whether additional users were targeted.
  - Whether the URL or attachment was accessed.
  - Whether credential theft, malware execution, or unauthorized access occurred.

### Triage (5W1H Analysis):
- Who:
  - Sender: strangeaccount88@proton.me
  - Source IP: 79.135.106.97 (malicious reputation confirmed via AbuseIPDB)
- What:
  - Phishing email containing:
    - Malicious URL
    - Suspicious attachment (Salary Revision.docx)
- When:
  - June 18, 2026 – 21:04 (UTC +04:00)
- Where:
  - Recipient: bob@corp88.onmicrosoft.com
  - Subject: Salary Revision
- Why:
  - Likely objective: credential harvesting, malware delivery, or unauthorized access to internal resources.
- How:
  - Email successfully bypassed email security controls and was delivered to the user mailbox; bypass vector under investigation.

### Response Actions:
- Removed phishing email from all affected mailboxes.
- Blocked malicious indicators:
  - Sender email
  - Sender IP address
  - URL domain and path
  - Associated attachment indicators
- Conducted tenant-wide search across:
  - Sender address
  - IP address
  - URL
  - Attachment name and related artifacts
- Investigated user interaction with:
  - URL access
  - Credential submission attempts
  - Attachment execution or download
- Deployed targeted user awareness notification referencing the “Salary Revision” phishing attempt.

### Recommendations:
- Enhance email security posture using:
  - Microsoft Defender for Office 365 Safe Links
  - Safe Attachments detonation policies
  - Anti-phishing impersonation protections
- Strengthen email authentication enforcement:
  - SPF, DKIM, and DMARC alignment and strict policy enforcement.
- Improve detection tuning for HR/payroll-themed phishing campaigns.
- Enable continuous monitoring for anomalous authentication and credential abuse patterns.
- Conduct periodic phishing simulation exercises to reinforce user awareness.
- Perform gap analysis on email security controls to identify bypass conditions.

### Lessons Learned:
- Email-based threats can bypass initial filters when using trusted-looking HR or payroll lures.
- OSINT validation (VirusTotal, AbuseIPDB) is critical for confirming malicious indicators quickly.
- Message header analysis provides key visibility into email authenticity and routing.
- Early user interaction prevention is essential to limit credential theft and payload execution.
- Regular tuning of Safe Links and Safe Attachments policies improves detection coverage.
- Tenant-wide hunting helps assess blast radius and identify additional impacted users.

