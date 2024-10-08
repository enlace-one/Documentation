# The Basics About DMARC, DKIM, and SPF

## Basics - Definitions

**Sender Policy Framework (SPF)**: Says what IPs are allowed to send for this domain.

**DomainKeys Identified Mail (DKIM)**: Verified the email came from domain specified using signatures.

**Domain-based Message Authentication, Reporting, and Conformance (DMARC)**: Says what to do with emails that fail the above checks.

## Basics - Diagram
Access this link to see the most updated version: [Canva](https://www.canva.com/design/DAGS70X--Bs/DUmDxfXvxUq2B9UZrjnN1g/view?utm_content=DAGS70X--Bs&utm_campaign=designshare&utm_medium=link&utm_source=editor)
![DMARC Flow](https://github.com/user-attachments/assets/19141c39-b3ba-43dd-a77a-bd65bcd87cd7)

## Basics - Authentication Checks
So what exactly are the authentication checks? 

Take the below email. 

### Basics - Auth - Sample Email
Return-Path: <jane@**dundermifflin.com**> **(1)**
Delivered-To: <michael@saber.com>
Authentication-Results: mail.dundermifflin.com;
    spf=pass (saber.com: domain of jane@dundermifflin.com designates 1.2.3.4 as a permitted sender) smtp.mailfrom=jane@dundermifflin.com;
    dkim=pass header.i=dundermifflin.com
DKIM-Signature: v=1; a=rsa-sha256; c=relaxed/relaxed; d=**dundermifflin.com**; **(2)** h=From:To:Subject:Date:Message-ID; s=default; bh=abc123...; b=def456...
Date: Mon, 7 Oct 2024 16:30:00 -0400
From: Jane Doe <jane@**dundermifflin.com**> **(3)**
To: Michael Scott <michael@saber.com>
Subject: Meeting Reminder
Message-ID: <1234567890@dundermifflin.com>

1. The "Return-Path domain" is used for SPF
2. The "DKIM Signature domain" is used for DKIM
3. The "From domain" is used for

# Advanced

## Advanced - Example Records

### Advanced - Records - DMARC
```
v=DMARC1; p=reject; rua=mailto:dmarc-reports@example.com; ruf=mailto:forensic-reports@example.com; fo=1; adkim=s; aspf=s; pct=100;
```
v=DMARC1: Specifies the DMARC version.

p=reject: Instructs the receiving server to reject emails that fail DMARC.

rua: Where aggregate reports should be sent.

ruf: Where forensic reports should be sent.

fo=1: Requests detailed forensic reports for every failed email.

adkim=s: Align DKIM checks strictly with the domain in the "From" header.

aspf=s: Align SPF checks strictly with the domain in the "From" header.

pct=100: Apply the DMARC policy to 100% of messages.

### Advanced - Records - DKIM
```
v=DKIM1; k=rsa; p=MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAzDOjHRhvPDAF...
```
v=DKIM1: Specifies the DKIM version.

k=rsa: Specifies the key type (RSA).

p=<public key>: The public key used for verification, in Base64 format.

The domain used in the Host field (default._domainkey.example.com) is a combination of:
- default: The selector you use in your DKIM setup.
- _domainkey: Specifies that this is a DKIM record.
- example.com: Your domain.

### Advanced - Records - SPF
```
v=spf1 ip4:192.0.2.0/24 ip6:2001:db8::/32 include:mailgun.org ~all
```
v=spf1: Specifies the SPF version.

ip4:192.0.2.0/24: Authorizes this IPv4 address range to send emails.

ip6:2001:db8::/32: Authorizes this IPv6 address range to send emails.

include:mailgun.org: Authorizes Mailgun (third-party email service) to send emails for this domain.

~all: Soft fail for any server not listed in the SPF record. Other options:
- -all: Hard fail (reject).
- +all: Allow any server (not recommended).

# Frequently Asked Questions (FAQs)

## What happens if the SPF policy is not set but DMARC is p=quarantine or p=reject? 
If the email passes DKIM, then it should pass DMARC and be delivered.

IF the email fails DKIM, then the SPF will count as a fail and it will fail DMARC.

## What happens when spf=pass, dkim=pass but dmarc=fail? 
DMARC fails likely due to alignment. 

## What does neutral DKIM mean?
No signature in the email or the receiver did not do a lookup.
