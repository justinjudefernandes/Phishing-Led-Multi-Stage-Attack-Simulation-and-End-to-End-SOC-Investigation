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
- Endpoint compromise and lateral movement via RDP and malicious execution

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
- Lateral movement simulation via RDP
- PowerShell-based attack execution analysis
- Credential harvesting simulation
- MITRE ATT&CK mapping
- SOC alert triage and investigation

### Key Deliverables:
- End-to-end phishing attack simulation (Email → Identity → Endpoint)
- Identity compromise and impossible travel scenario validation
- Endpoint compromise using PowerShell and credential dumping simulation
- Lateral movement simulation using RDP
- Microsoft Defender XDR incident investigation
- Attack chain correlation across multiple security layers
- Detection validation and alert analysis report

## Steps Performed:

### STEP 1: Phishing Email (Email Security Simulation)
- A phishing email was sent to user Jenny’s mailbox from a random external sender.
- Microsoft Defender Safe Links rewrote the embedded malicious URL for protection tracking.
- The user Jenny clicked the rewritten link, which redirected to a DocuSign-like credential harvesting page.
- Jenny entered her username and password, simulating credential theft.
- This stage represented initial access via phishing and social engineering.

📌 Refer to the below screenshots:

<img width="605" height="324" alt="image" src="https://github.com/user-attachments/assets/99ad9052-ae06-4313-a751-5f0263aa0ad7" />
<img width="701" height="380" alt="image" src="https://github.com/user-attachments/assets/1f991a43-dfb7-4959-ae06-20f7ce7e38e8" />
<img width="697" height="340" alt="image" src="https://github.com/user-attachments/assets/c3909741-7ca9-461d-bf56-a5fa1b6e4375" />


### STEP 2: Hijacking Identity (Identity Protection & Impossible Travel Simulation)
- Logged into a Windows Server 2022 VM using VPN to simulate access from the Netherlands.
- Successfully signed into Jenny’s mailbox without MFA enforcement (Security Defaults disabled in prior setup).
- Performed additional sign-in attempts into Jenny's mailbox from a local machine to simulate impossible travel behavior.
- Successfully authenticated into Jenny’s mailbox from multiple geographic locations.
- Established remote access to the Windows 11 VM using RDP with Jenny’s compromised credentials.
- Modified the hosts file to map the Windows 11 system hostname.
- Used advanced RDP settings:
    - “Use a web account to sign in to the remote computer”
- Connected using hostname-based RDP access to simulate attacker persistence and access.

📌 Refer to the below screenshots:

<img width="703" height="380" alt="image" src="https://github.com/user-attachments/assets/2dd8257a-e69d-4ea8-87bd-81f587949861" />
<img width="635" height="373" alt="image" src="https://github.com/user-attachments/assets/c271fea5-ac51-4302-9ca7-67cdff2e8557" />
<img width="806" height="430" alt="image" src="https://github.com/user-attachments/assets/73b9e693-b9d0-4567-a864-d688c52af4ab" />
<img width="797" height="443" alt="image" src="https://github.com/user-attachments/assets/9222f877-5df4-4df7-aa41-9bdd988c6295" />
<img width="803" height="422" alt="image" src="https://github.com/user-attachments/assets/47a0fde4-bec0-45a1-a66c-d7fb9a73de69" />
<img width="801" height="409" alt="image" src="https://github.com/user-attachments/assets/acd92f84-1a62-461d-ae0c-e489821a9f36" />
<img width="800" height="517" alt="image" src="https://github.com/user-attachments/assets/0f196026-a216-4a98-9627-0b2188d5dcaf" />
<img width="802" height="512" alt="image" src="https://github.com/user-attachments/assets/2b2a18f0-090d-494a-907d-5e438a195788" />

### STEP 3: Compromising Endpoints (Endpoint Threat Simulation)
- On the Windows 11 endpoint (Jenny’s machine), PowerShell was used to simulate attacker activity.
- Executed a script to deploy and run Mimikatz, simulating credential dumping behavior.
- Verified execution by locating artifacts in the %TEMP% directory.
- Ran Mimikatz to simulate extraction of credentials from LSASS memory.
- Executed Atomic Red Team technique T1059.001 (PowerShell execution simulation).
- Microsoft Defender for Endpoint generated alerts under Incidents & Alerts.
- Verified detection and correlation in the Microsoft Defender XDR portal.

📌 Refer to the below screenshots:

<img width="798" height="423" alt="image" src="https://github.com/user-attachments/assets/7e2e3f8e-40cf-4fa4-8e08-aa5ac2819523" />
<img width="798" height="510" alt="image" src="https://github.com/user-attachments/assets/81c8c9cc-b31d-4ce5-a370-49a4efc6ad8a" />
<img width="705" height="515" alt="image" src="https://github.com/user-attachments/assets/331677f8-d677-46ef-83fc-49d91c1be5aa" />
<img width="705" height="401" alt="image" src="https://github.com/user-attachments/assets/ddf0c441-a6b7-4d65-a75b-2ba8a3df1cf9" />
<img width="704" height="391" alt="image" src="https://github.com/user-attachments/assets/fdf179f9-2061-43a9-a702-6c77e56c94b2" />
<img width="704" height="390" alt="image" src="https://github.com/user-attachments/assets/7700d3ec-cff4-45ec-8dc3-6cce5b4cb805" />

### Attack Flow Summary:
- Phishing email delivered → malicious URL clicked → credential capture simulated
- Captured credentials used for login → risky sign-ins → impossible travel detection simulated
- RDP access gained → PowerShell execution → credential dumping simulation → lateral movement behavior

## SOC Investigation Report: Phishing-Led Multi-Stage Attack (Email → Identity → Endpoint)

### Incident Overview:
- Alert Name: Potential human-operated malicious activity (Hands-on-keyboard attack)
- Incident Name: Account compromise with post-exploitation endpoint activity
- First Activity: 22-Jun-2026 – 10:52 PM (UTC +04:00)
- Last Activity: 22-Jun-2026 – 11:44 PM (UTC +04:00)
- Affected Endpoint: Windows11
- User: jenny
- Severity: High
- Detection Source: Microsoft Defender for Endpoint

Microsoft Defender for Endpoint detected a high-severity, human-operated attack following a phishing-led credential compromise. The incident spanned multiple security layers including email compromise, identity misuse, and endpoint-level execution activity.

The attack chain progressed from phishing email interaction to credential theft, followed by suspicious sign-ins (including impossible travel indicators), and culminated in endpoint-based hands-on-keyboard activity involving credential dumping and lateral movement attempts.

### Indicators of Compromise (IOCs):
- Endpoint Artifacts:
    - mimikatz.exe (PID: 13544)
    - mimidrv.sys
    - powershell.exe (PID: 5356)
    - lsass.exe (PID: 800) interaction observed
    - explorer.exe (suspicious behavior)
- Device / System Artifacts:
        - WINDOWS11$ (machine account)
- Network / Internal Activity: 
        - 192.168.126.1
        - 192.168.126.156

### MITRE ATT&CK Techniques:
- T1003 – OS Credential Dumping
- T1555 – Credentials from Password Stores
- T1021.001 – Remote Desktop Protocol
- T1105 – Ingress Tool Transfer
- T1219 – Remote Access Tools
- T1059.001 – PowerShell (Execution observed during endpoint activity)

### Investigation Summary:
- Microsoft Defender for Endpoint generated a high-severity alert indicating potential human-operated malicious activity on the Windows11 endpoint associated with user jenny.
- The investigation revealed that the attack originated from a phishing email containing a malicious URL. The user interacted with the email, resulting in credential compromise.
- Shortly after, a successful sign-in was observed from Amsterdam, indicating unauthorized access and triggering an impossible travel alert under Microsoft Entra ID Identity Protection.
- The attacker then leveraged the compromised credentials to gain access to the environment and perform hands-on-keyboard activity on the Windows11 endpoint.
- Endpoint telemetry confirmed execution of credential dumping tools (Mimikatz), PowerShell activity, and interaction with the LSASS process. These behaviors are strongly associated with post-exploitation credential theft and lateral movement preparation.
- Microsoft Defender correlated email, identity, and endpoint signals, confirming a full phishing-led compromise lifecycle. Automated attack disruption actions were triggered, including account containment, RDP blocking, and quarantine of malicious artifacts.

📌 Refer to the below screenshots:(follow the sequence from left to right)

<img width="330" height="230" alt="image" src="https://github.com/user-attachments/assets/e9bc6e39-d2d5-45ba-a89f-16a2e4afdb8f" /> <img width="330" height="230" alt="image" src="https://github.com/user-attachments/assets/c1ce939d-9d73-4199-a7e2-cb83daf3ab71" /> <img width="330" height="230" alt="image" src="https://github.com/user-attachments/assets/cb6a35d9-2217-41f4-a72d-ef22cb974d8a" />
<img width="330" height="230" alt="image" src="https://github.com/user-attachments/assets/1e547214-9a17-4f07-9c1c-58b469b7747c" /> <img width="330" height="230" alt="image" src="https://github.com/user-attachments/assets/49238c3c-6ffb-498d-9888-115b0b8b0812" /> <img width="330" height="230" alt="image" src="https://github.com/user-attachments/assets/6dc0a9d2-4be0-4243-abe4-74fc5f36a4b8" />
<img width="330" height="230" alt="image" src="https://github.com/user-attachments/assets/8536d983-96cd-469f-a9cc-d14a00d5361a" /> <img width="330" height="230" alt="image" src="https://github.com/user-attachments/assets/866c07e6-995f-4caf-9fb4-1ad97bcce418" /> <img width="330" height="230" alt="image" src="https://github.com/user-attachments/assets/0ab79f01-1d2b-4d4d-9d54-16444dd403a6" />
<img width="330" height="230" alt="image" src="https://github.com/user-attachments/assets/2e02d13f-7a92-4aa7-92d3-efabe730b696" /> <img width="330" height="230" alt="image" src="https://github.com/user-attachments/assets/d65ab40a-45eb-4ae9-b3dd-fa8738a6d725" /> <img width="330" height="230" alt="image" src="https://github.com/user-attachments/assets/dcfefee4-b5dc-4eb0-b79e-c6be251a7e6b" />














### Correlation Analysis (Attack Chain):
- Phishing Email delivered to user jenny
- User clicked malicious URL (DocuSign-style credential harvester simulation)
- Credentials were compromised
- Suspicious sign-in detected from Amsterdam (impossible travel)
- Unauthorized mailbox access observed
- Attacker gained access to Windows11 endpoint via RDP
- Hands-on-keyboard activity initiated
- Mimikatz executed for credential dumping
- PowerShell used for execution and post-compromise actions
- LSASS memory interaction observed
- Lateral movement attempts via RDP identified and blocked
- Defender triggered automated containment and quarantines

### Timeline of Events: 
- 10:07 PM – Phishing email delivered to user mailbox
- 10:10 PM – Malicious URL clicked by user
- 10:39 PM – Suspicious login from Amsterdam detected (impossible travel)
- 10:52 PM – First endpoint detection (HOK alert generated)
- 11:07 PM – Incident containment initiated (Defender response)
- 11:17 PM – Lateral movement via RDP blocked
- 11:44 PM – Last observed malicious activity
- Post 11:44 PM – Multiple quarantine actions executed

### Triage (5W1H Analysis):

#### Who:
- User: jenny
- Endpoint: Windows11
- Machine Account: WINDOWS11$
- Detection Source: Microsoft Defender for Endpoint

#### What:
- High-severity “Potential human-operated malicious activity” alert
- Phishing-led credential compromise
- Endpoint execution of credential dumping and PowerShell activity
- Lateral movement attempts via RDP

#### When:
- Initial compromise: 10:07 PM
- Endpoint activity: 10:52 PM – 11:44 PM (22-Jun-2026)

#### Where:
- Windows11 endpoint
- External login observed from Amsterdam
- Internal network: 192.168.126.1 / 192.168.126.156

#### Why:
- Initial access gained via phishing email containing malicious URL
- Credentials were stolen and reused for unauthorized access

#### How:
- User interaction with phishing link led to credential compromise
- Attacker used stolen credentials to access mailbox and endpoint
- Executed Mimikatz, PowerShell, and LSASS interaction for credential theft
- Attempted lateral movement via RDP
- Defender correlated multi-layer telemetry and triggered automated containment

### Threat Hunting KQL Queries:
- Looked for other users received the email with URL “docusign[.]com”.
```KQL Query:
            EmailUrlInfo
            | where Url contains "docusign[.]com"
            | project Timestamp, NetworkMessageId, Url
            | join kind=inner (
                EmailEvents
                | project NetworkMessageId, RecipientEmailAddress, Subject
            ) on NetworkMessageId
            | order by Timestamp desc
```

<img width="703" height="347" alt="image" src="https://github.com/user-attachments/assets/553cdb69-4370-40d5-b2dc-fee50ebb0827" />

- Find users who received the email with subject "Invoice is ready for viewing"
```KQL Query:
            EmailEvents
            | where Subject contains "Invoice is ready for viewing"
            | project Timestamp, RecipientEmailAddress, SenderFromAddress, Subject
            | order by Timestamp desc
```

<img width="704" height="350" alt="image" src="https://github.com/user-attachments/assets/a4343543-3274-4f94-bbdf-f830f37652c8" />

- Looked for suspicious sign-ins from foreign countries:
```KQL Query:
            SigninLogs
            | where LocationDetails.countryOrRegion != "AE"
            | project TimeGenerated, Identity, Location, AppDisplayName
            | order by TimeGenerated desc
```

<img width="704" height="350" alt="image" src="https://github.com/user-attachments/assets/90ce734f-6fa5-4cd3-8913-171f16973ff0" />

- Checked for lateral movement attempts using RDP:
```KQL Query:
            DeviceNetworkEvents
            | where RemotePort == 3389
            | project Timestamp, DeviceName, InitiatingProcessAccountName, RemoteIP
            | order by Timestamp desc
```

<img width="703" height="350" alt="image" src="https://github.com/user-attachments/assets/b3bbac61-b5d7-47c9-976e-fcd0fef8f8e8" />

- Searched for suspicious remote logons:
```KQL Query:
            DeviceLogonEvents
            | where LogonType == "RemoteInteractive"
            | project Timestamp, DeviceName, AccountName, RemoteIP
            | order by Timestamp desc
```

<img width="704" height="349" alt="image" src="https://github.com/user-attachments/assets/69f2dbb7-148c-4549-bcc1-0a2faac78166" />

- Checked for PowerShell activity after the compromise:
```KQL Query:
            DeviceProcessEvents
            | where FileName =~ "powershell.exe"
            | project Timestamp, DeviceName, AccountName, ProcessCommandLine
            | order by Timestamp desc
```

<img width="704" height="349" alt="image" src="https://github.com/user-attachments/assets/a1d7d054-4b17-4a18-b036-c4e46a1fdd72" />

- Searched for additional users triggering similar alerts:
```KQL Query:
            AlertInfo
            | where Title contains "Potential human-operated malicious activity"
            | project Timestamp, Title, Severity, ServiceSource
            | order by Timestamp desc
```

<img width="703" height="344" alt="image" src="https://github.com/user-attachments/assets/0198b816-c9fa-40ef-aa2b-f1643484591d" />

### Response Actions:
- Reset compromised user credentials (Jenny)
- Revoked all active sessions and authentication tokens
- Reviewed mailbox rules, forwarding, and delegation settings
- Investigated sign-in logs for anomalous activity
- Contained compromised user account via Microsoft Defender
- Blocked RDP-based lateral movement attempts
- Quarantined malicious files and artifacts via Defender automation
- Conducted endpoint and identity impact assessment
- Invalidated compromised sessions and enforced remediation

### Recommendations:
- Enforce Multi-Factor Authentication (MFA) across all accounts
- Implement Conditional Access policies for risky sign-ins and geolocation anomalies
- Strengthen phishing awareness training for end users
- Monitor and alert on impossible travel scenarios
- Maintain automated EDR containment and response configurations
- Conduct continuous threat hunting for credential dumping behavior
- Review and harden email security controls (Safe Links, Anti-Phishing, Safe Attachments)

### Lessons Learned:
- Phishing remains the primary and most effective initial access vector
- Credential theft enables rapid cross-border attacker access
- Endpoint telemetry is critical for detecting post-compromise behavior
- LSASS interaction and PowerShell execution are key detection signals
- Hands-on-keyboard attacks evolve quickly and require rapid containment
- Correlation across email, identity, and endpoint layers is essential for full visibility
- Automated response significantly reduces attacker dwell time and impact
- Lateral movement attempts often follow successful credential compromise

