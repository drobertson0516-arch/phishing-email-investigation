# Phishing Email Investigation & Account Compromise

## Project Overview

This project documents a simulated SOC investigation of a credential-phishing campaign impersonating Microsoft 365.

The investigation began with a user-reported phishing email and expanded into campaign scoping, URL analysis, authentication analysis, and post-compromise mailbox investigation. The evidence ultimately identified one confirmed Microsoft 365 account compromise involving credential theft, MFA request generation, unauthorized account access, creation of an email forwarding rule, and information exposure.

The incident was assessed as **High severity** and required account containment, credential remediation, session revocation, mailbox investigation, and additional follow-up to determine the impact of exposed information.

> **Training Disclaimer:** This is a synthetic cybersecurity portfolio project. All organizations, employees, domains, IP addresses, email messages, and security events are fictional.

## Investigation Objectives
- Analyze the reported phishing email for suspicious indicators.
- Review email authentication results and sender information.
- Analyze the embedded URL and credential-harvesting behavior.
- Determine the scope of the phishing campaign.
- Identify recipients who interacted with the malicious link.
- Investigate authentication activity associated with submitted credentials.
- Determine whether a Microsoft 365 account was compromised.
- Review post-compromise mailbox activity and information exposure.
- Map observed attacker behavior to the MITRE ATT&CK framework.
- Recommend containment, remediation, and follow-up actions.

## Key Findings
- 12 employees received the phishing email.
- 1 employee reported the message as phishing.
- 2 employees clicked the phishing URL.
- 1 employee submitted credentials to the fraudulent login page.
- Multiple MFA requests were generated after the credential submission.
- The employee denied two MFA requests before approving a third.
- An unfamiliar IP address successfully authenticated to the Microsoft 365 account after the MFA approval.
- An unauthorized inbox forwarding rule was created.
- 7 emails were opened during the unauthorized session.
- 1 customer invoice PDF was downloaded.
- 2 emails were forwarded to an external address.
- A password-reset link for an internal expense application was opened.
- No successful unauthorized login to the expense application was identified.
- No additional compromised Microsoft 365 accounts were identified at the time of the investigation.

## MITRE ATT&CK Mapping
- **T1566.002 — Spearphishing Link:** The phishing email contained a link directing recipients to a fraudulent Microsoft 365 login page designed to collect credentials.
- **T1621 — Multi-Factor Authentication Request Generation:** Multiple MFA requests were generated after credential submission. Two were denied before a third was approved.
- **T1114.003 — Email Forwarding Rule:** After the account was compromised, an unauthorized inbox rule was created to forward incoming email to an external address.

## Incident Response

The compromised account was contained through account disabling, password reset, and active-session revocation. The unauthorized forwarding rule was preserved as evidence and removed.

Additional response actions included reviewing mailbox activity, investigating the second employee who clicked the phishing URL, securing the internal expense application account, removing the phishing message from affected mailboxes, and blocking identified malicious indicators where appropriate.

## Skills Demonstrated
- Phishing email analysis
- Email header analysis
- Malicious URL analysis
- Credential-phishing identification
- Authentication log analysis
- MFA fatigue recognition
- Incident scoping
- Microsoft 365 account-compromise analysis
- Mailbox investigation
- MITRE ATT&CK mapping
- Incident severity assessment
- Containment and response planning
- Evidence-based incident documentation
- Technical and executive communication

## Project Documentation

- [Phishing Email Evidence](evidence/phishing-email.md)
- [Investigation Notes](analysis/investigation-notes.md)
- [Incident Report](report/phishing-email-incident-report.pdf)

## Key Lessons

This project reinforced that phishing investigations should extend beyond the initial email. A successful credential-phishing attack may lead to additional authentication activity, MFA abuse, unauthorized mailbox access, persistence mechanisms, and information exposure.

The investigation also demonstrated the importance of separating confirmed evidence from assumptions, distinguishing incident severity from containment status, and validating the full scope and impact of an account compromise before closing an incident.
