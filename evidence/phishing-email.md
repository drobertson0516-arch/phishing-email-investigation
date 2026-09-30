# Phishing Email Evidence

## Case Information

**Organization:** Northstar Financial Services  
**Incident Type:** Credential Phishing / Account Compromise  
**Date Observed:** September 29, 2026  
**Reported:** 9:18 AM  
**Initial Reporter:** Rachel Kim  

> **Training Note:** This is a synthetic cybersecurity portfolio exercise. All organizations, employees, domains, IP addresses, email messages, and security events in this project are fictional.

---

## Reported Email

**From:** Microsoft Security `<security-alert@micros0ft-support.com>`  
**To:** Rachel Kim `<rkim@northstarfinancial.com>`  
**Subject:** `URGENT: Your Microsoft 365 Password Expires Today`  
**Date:** September 29, 2026, 9:12 AM

### Email Body

> Dear Rachel,
>
> Your Microsoft 365 password will expire today. Failure to verify your account will result in immediate suspension of email and Microsoft Teams access.
>
> To prevent service interruption, please verify your credentials immediately:
>
> **Verify Microsoft 365 Account**
>
> This verification must be completed within **30 minutes**.
>
> Microsoft 365 Security Team

### Embedded Link

Visible text:

`Verify Microsoft 365 Account`

Actual destination:

`https://microsoft-accountverify.example/login`

For this synthetic exercise, `.example` represents a suspicious external domain and should not be visited.

---

## Email Headers

```text
Return-Path: <security-alert@micros0ft-support.com>
From: "Microsoft Security" <security-alert@micros0ft-support.com>
To: <rkim@northstarfinancial.com>
Subject: URGENT: Your Microsoft 365 Password Expires Today
Date: Tue, 29 Sep 2026 09:12:04 -0400
Message-ID: <847291@micros0ft-support.com>

Authentication-Results:
    spf=fail
    dkim=none
    dmarc=fail

Received:
    from mail.micros0ft-support.com (203.0.113.77)
    by mail.northstarfinancial.com
