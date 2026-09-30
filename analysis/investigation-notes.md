# Investigation Notes

## Incident Overview

A phishing campaign impersonating Microsoft 365 targeted 12 employees at Northstar Financial Services. The message warned recipients that their Microsoft 365 passwords would expire and pressured them to verify their credentials within 30 minutes.

One employee reported the email as phishing. Investigation of the campaign identified two employees who clicked the embedded link and one employee who submitted credentials.

> **Training Note:** This investigation is a synthetic cybersecurity portfolio exercise. All organizations, employees, domains, IP addresses, email messages, and security events are fictional.

---

## 1. Initial Email Analysis

Several indicators suggested that the email was not a legitimate Microsoft 365 notification:

- The sender domain used `micros0ft` with a zero instead of the letter "o," indicating a lookalike domain.
- The message created urgency by claiming the account would be suspended and requiring action within 30 minutes.
- The embedded link directed the user to an external domain rather than an identified Microsoft domain.
- SPF authentication failed.
- DMARC authentication failed.
- DKIM was not present.

These indicators justified further investigation of the sender and embedded URL.

---

## 2. URL Analysis

The embedded URL directed users to:

`https://microsoft-accountverify.example/login`

Analysis showed that:

- The domain was only three days old.
- No Microsoft affiliation was identified.
- The page imitated a Microsoft 365 sign-in page.
- The page requested an email address and password.
- Submitted credentials were sent to the external domain.
- No existing threat-intelligence reputation data was available for the domain.

The absence of reputation data was not treated as evidence that the domain was safe. The combination of Microsoft impersonation and credential collection supported classification of the URL as malicious.

### Classification

**Malicious — Credential Phishing**

---

## 3. Campaign Scope

Investigation identified:

- 12 phishing emails delivered
- 1 phishing report
- 2 recipients who clicked the URL
- 1 recipient who submitted credentials
- 1 confirmed compromised Microsoft 365 account

The employee who reported the message did not click the link.

One additional employee clicked the URL but had no detected credential submission. Their account activity should still be reviewed as a precaution.

---

## 4. Account Compromise Analysis

The employee who submitted credentials subsequently received multiple MFA authentication requests.

Authentication activity showed:

- 09:58:41 — MFA challenge denied
- 09:59:13 — MFA challenge denied
- 10:02:52 — MFA challenge approved
- 10:03:01 — Successful authentication from unfamiliar IP `198.51.100.24`
- 10:07:16 — Unauthorized inbox forwarding rule created

The employee reported rejecting the first two MFA requests but approving the third because they believed Microsoft required confirmation.

The repeated authentication prompts followed by an approved request are consistent with **MFA fatigue**, also known as MFA bombing or MFA push spam.

This activity is different from password spraying. Password spraying attempts a small number of passwords against multiple accounts, while this activity involved repeated MFA requests directed at a user after credentials had already been obtained.

---

## 5. Mailbox Investigation

The unauthorized Microsoft 365 session lasted from approximately 10:03 AM to 10:19 AM.

During the session:

- 7 emails were opened.
- Internal employee communications were accessed.
- A customer invoice was accessed and downloaded.
- 2 emails were forwarded to an external address.
- A password-reset email for an internal expense application was accessed.
- The password-reset link was opened.

No successful unauthorized login to the expense application was identified.

No additional compromised Microsoft 365 accounts were identified at the time of the investigation.

The evidence confirms unauthorized mailbox access and information exposure. The opened password-reset link represents a potential risk to the expense application, but the available evidence does not establish that the attacker successfully accessed that application.

---

## 6. MITRE ATT&CK Mapping

### T1566.002 — Spearphishing Link

The phishing email contained a malicious link directing recipients to a fraudulent Microsoft 365 login page designed to collect credentials.

### T1621 — Multi-Factor Authentication Request Generation

Multiple MFA requests were generated after credentials were submitted. Two requests were denied before a third request was approved, followed by a successful authentication from an unfamiliar IP address.

### T1114.003 — Email Forwarding Rule

After gaining access to the Microsoft 365 account, an unauthorized inbox forwarding rule was created to forward incoming messages to an external address.

---

## 7. Severity Assessment

**Severity: High**

The incident was classified as High severity because the investigation confirmed:

- Credential theft
- Successful unauthorized Microsoft 365 authentication
- MFA request generation followed by user approval
- Unauthorized mailbox access
- Creation of an external forwarding rule
- Access to internal communications
- Download of a customer invoice
- External forwarding of two emails

The incident was not reduced in severity simply because containment actions were initiated. Severity reflects the impact and risk of the incident, while containment describes the current response status.

---

## 8. Containment and Response

Recommended and completed response actions included:

- Disable or lock the compromised account.
- Reset the compromised password.
- Revoke active sessions and authentication tokens.
- Review the MFA activity and secure the employee's authentication methods.
- Preserve the unauthorized forwarding rule as evidence before removing it.
- Remove the unauthorized forwarding rule.
- Review the compromised mailbox for unauthorized activity.
- Quarantine or remove the phishing message from affected mailboxes.
- Block identified malicious sender, domain, URL, and related indicators where appropriate.
- Review the second employee who clicked the phishing URL for additional signs of compromise.
- Invalidate the expense-application password-reset link and secure the associated account.
- Notify appropriate security, management, privacy, legal/compliance, and data owners according to organizational incident-response procedures.
- Provide phishing and MFA-awareness training after immediate containment and investigation activities are complete.

---

## 9. Analyst Conclusion

A credential-phishing campaign impersonating Microsoft 365 targeted 12 employees and directed recipients to a fraudulent credential-harvesting page. Two employees clicked the phishing link, and one employee submitted credentials and subsequently approved an MFA request, after which an unfamiliar source IP successfully authenticated to the employee's Microsoft 365 account.

During the unauthorized session, the attacker accessed mailbox contents, created an external forwarding rule, downloaded a customer invoice, forwarded two emails externally, and opened a password-reset link associated with an internal expense application.

Security contained the compromised account by disabling access, initiating a password reset, revoking active sessions, and preserving and removing the unauthorized forwarding rule.

The incident remains **High severity**, with investigation continuing to determine the sensitivity and impact of the exposed information and whether any additional access occurred.

---

## Key Lessons

This investigation demonstrated the importance of:

- Evaluating multiple phishing indicators rather than relying on a single indicator.
- Treating missing threat-intelligence reputation as unknown rather than safe.
- Distinguishing credential phishing from subsequent account-compromise activity.
- Recognizing MFA fatigue as a post-credential-theft technique.
- Separating confirmed evidence from assumptions.
- Separating incident severity from containment status.
- Investigating post-compromise mailbox activity to determine the actual impact of an incident.
- Documenting both confirmed impact and areas requiring additional investigation.
