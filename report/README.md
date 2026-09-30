# Incident Report

This folder contains the formal incident report for the **Phishing Email Investigation** cybersecurity portfolio project.

## Report

**Phishing Email Investigation & Account Compromise**

The report documents the investigation of a synthetic credential-phishing campaign impersonating Microsoft 365 that resulted in one confirmed account compromise.

The investigation includes:

- Phishing email and header analysis
- Malicious URL analysis
- Campaign scoping
- Credential-phishing identification
- MFA fatigue analysis
- Microsoft 365 account-compromise investigation
- Mailbox activity analysis
- Incident timeline development
- MITRE ATT&CK mapping
- Severity assessment
- Containment and response actions
- Remediation recommendations
- Analyst conclusions

## Key Findings
The phishing campaign targeted 12 employees. Two recipients clicked the phishing link, and one employee submitted credentials.

Following credential submission, repeated MFA requests were generated. The employee denied two requests before approving a third. An unfamiliar source IP subsequently authenticated to the Microsoft 365 account.

Post-compromise investigation identified unauthorized mailbox access, creation of an external forwarding rule, seven opened emails, one downloaded customer invoice, and two emails forwarded externally.

The incident was classified as **High severity** because credential theft, unauthorized account access, and information exposure were confirmed.

## MITRE ATT&CK

- **T1566.002 — Spearphishing Link**
- **T1621 — Multi-Factor Authentication Request Generation**
- **T1114.003 — Email Forwarding Rule**

- ## Training Disclaimer

This project is a synthetic cybersecurity portfolio exercise. All organizations, employees, domains, IP addresses, email messages, and security events are fictional.
