---
title: "Fix email delivery issues for error code 5.7.23 in Exchange Online"
ms.author: dmaguire
author: msdmaguire
manager: serdars
ms.date: 5/25/2017
ms.reviewer: 
audience: Admin
ms.topic: troubleshooting
ms.service: o365-administration
localization_priority: Normal
ms.custom: 
search.appverid:
- BCS160
- MOE150
ms.assetid: 
description: "Learn how to fix email issues for error code 5.7.23 in Exchange Online (The message was rejected because of Sender Policy Framework violation)."
---

# Fix email delivery issues for error code 5.7.23 in Exchange Online

It's frustrating when you get an error after sending an email message. This topic describes what you can do if you see error code 550 5.7.23 in a non-delivery report (also known as an NDR, bounce message, delivery status notification, or DSN).

|||||
|:-----|:-----|:-----|:-----|
|![Email user icon](../../media/31425afd-41a9-435e-aa85-6886277c369b.png)|[I got this bounce message. How do fix it?](#i-got-this-bounce-message-how-do-i-fix-it)|![Email admin icon](../../media/3d4c569e-b819-4a29-86b1-4b9619cf2acf.png)|[I'm an email admin. How do I fix this?](#im-an-email-admin-how-do-i-fix-this)|

## I got this bounce message. How do I fix it?

Only an email admin in your Office 365 organization can fix this issue. Contact your email admin and refer them to this information so they can try to resolve the issue for you.

## I'm an email admin. How do I fix this?

This bounce message indicates an issue with email domain authentication and validation in your Office 365 organization:

- [Sender policy framework (SPF)](https://docs.microsoft.com/office365/securitycompliance/set-up-spf-in-office-365-to-help-prevent-spoofing)

- [DKIM](https://docs.microsoft.com/office365/securitycompliance/use-dkim-to-validate-outbound-email)

- [DMARC](https://docs.microsoft.com/office365/securitycompliance/use-dmarc-to-validate-email)

The **Diagnostic information for administrators** section in the bounce message will contain the original error message when Office 365 tried to send the message to the external email server or service.

To fix this issue, do the following steps:

- Check your Office 365 domain authentication settings (SPF, DKIM and DMARC records in DNS) at [???].

- Verify that the outbound message wasn't identified as spam by Office 365. Outbound spam is routed through the High Risk Delivery Pool of IP addresses, which likely won't be accepted by the destination email organization. [Wouldn't this be covered by 5.1.8?]

## Still need help with error code 550 5.7.23?

[![Get help from the Office 365 community forums](../../media/12a746cc-184b-4288-908c-f718ce9c4ba5.png)](https://go.microsoft.com/fwlink/p/?LinkId=518605)

[![Admins: Sign in and create a service request](../../media/10862798-181d-47a5-ae4f-3f8d5a2874d4.png)](https://go.microsoft.com/fwlink/p/?LinkId=519124)

[![Admins: Call Support](../../media/9f262e67-e8c9-4fc0-85c2-b3f4cfbc064e.png)](https://go.microsoft.com/fwlink/p/?LinkID=518322)

## See also

[Email non-delivery reports in Exchange Online](non-delivery-reports-in-exchange-online.md)
