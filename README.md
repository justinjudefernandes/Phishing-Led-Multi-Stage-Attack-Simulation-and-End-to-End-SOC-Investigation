# Phishing-Led Multi-Stage Attack Simulation and End-to-End SOC Investigation

## Objective:
The Email Security & Phishing Analysis in Microsoft Defender project focused on configuring email security controls within Microsoft Defender for Office 365, validating their effectiveness against phishing threats, and performing an end-to-end phishing investigation. Through this project, I strengthened my skills in email security, threat analysis, OSINT, incident response, and Microsoft Defender technologies by simulating a real-world phishing attack scenario.

## Project Overview:
This project focuses on implementing Safe Links and Safe Attachments policies in Microsoft Defender for Office 365, validating email protection controls, investigating a phishing email, analyzing email headers, performing OSINT on indicators of compromise (IOCs), and documenting incident response actions.

### Tools Used:
- Microsoft Defender for Office 365
- Microsoft Defender XDR
- Microsoft 365 Explorer
- Safe Links
- Safe Attachments
- Notepad++
- VirusTotal
- AbuseIPDB
- Proton Mail

### Skill Developed:
- Email security administration
- Phishing investigation
- Email header analysis
- IOC identification and analysis
- Threat intelligence validation
- Incident response
- Microsoft Defender for Office 365

### Key Deliverables:
- Safe Links policy configuration
- Safe Attachments policy configuration
- Email security policy testing
- Email header analysis
- IOC enrichment using OSINT
- Phishing investigation report
- Incident response documentation
- Security recommendations and remediation actions

## Steps Performed:
### Safe Links Policy Configuration:
- Configured a Safe Links policy in Microsoft Defender to protect users from malicious URLs and attachments delivered via email.
  - Navigated to: Microsoft Defender → Email & collaboration → Policies & rules → Threat policies → Safe Links
  - Created and deployed a policy named: 'MyDFIR-Justin-SafeLinksforInvestigation'.
  - Enabled URL rewriting and real-time link scanning to ensure time-of-click protection against phishing and malicious redirects.

📌 Refer to the below screenshots for policy configuration and summary details.
<img width="752" height="420" alt="image" src="https://github.com/user-attachments/assets/a6d4dfb9-f579-4f8e-b4b9-35d9a3a73eb5" />
<img width="752" height="411" alt="image" src="https://github.com/user-attachments/assets/3e73cd77-0e17-4e44-8fbd-413ce6f4480a" />

### Safe Attachments Policy Configuration:
- Implemented a Safe Attachments policy to provide detonation-based malware protection for email attachments.
  - Navigated to: Microsoft Defender → Email & collaboration → Policies & rules → Threat policies → Safe Attachments
  - Created a policy named: 'MyDFIR-Justin-SafeAttachments&Links'.
  - Configured attachment scanning to detect and block potentially malicious payloads before delivery.

📌 Refer to the below screenshots for policy summary and configuration settings.
<img width="751" height="410" alt="image" src="https://github.com/user-attachments/assets/eccb3733-9b03-4668-8e1c-086e94839590" />
<img width="753" height="413" alt="image" src="https://github.com/user-attachments/assets/feac727d-50dd-45a5-b7f3-df9be83aaac6" />

### Policy Validation and Testing:
- Performed controlled testing to validate enforcement of Safe Links and Safe Attachments policies.
  - Sent a test phishing-style email from a newly created external ProtonMail account: 'strangeaccount88@proton[.]me'
  - Verified policy behavior through message inspection in Defender.
  - Confirmed that Safe Links and Safe Attachments protections were actively applied to the message content.

📌The below screenshots demonstrate policy enforcement and inspection results within Microsoft Defender.
<img width="749" height="286" alt="image" src="https://github.com/user-attachments/assets/b1a55330-82df-4099-8c4c-7062c319b7eb" />
<img width="749" height="374" alt="image" src="https://github.com/user-attachments/assets/eb301f83-3db1-412c-ab57-d997452d69a1" />

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

