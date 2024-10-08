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
Return-Path: <jane@dundermifflin.com> **(1)**
Delivered-To: <michael@saber.com>
Authentication-Results: mail.dundermifflin.com;
    spf=pass (saber.com: domain of jane@dundermifflin.com designates 1.2.3.4 as a permitted sender) smtp.mailfrom=jane@dundermifflin.com;
    dkim=pass header.i=dundermifflin.com
DKIM-Signature: v=1; a=rsa-sha256; c=relaxed/relaxed; d=dundermifflin.com; **(2)** h=From:To:Subject:Date:Message-ID; s=default; bh=abc123...; b=def456...
Date: Mon, 7 Oct 2024 16:30:00 -0400
From: Jane Doe <jane@dundermifflin.com> **(3)**
To: Michael Scott <michael@saber.com>
Subject: Meeting Reminder
Message-ID: <1234567890@dundermifflin.com>
