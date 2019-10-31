---
localization_priority: Normal
description:
ms.topic: conceptual
author: chrisda
ms.author: chrisda
ms.assetid:
ms.date:
ms.reviewer:
title: Enable or disable SMTP AUTH
ms.collection:
- exchange-online
- M365-email-calendar
audience: ITPro
ms.service: exchange-online
manager: serdars

---

# Enable or disable authenticated client SMTP submission (SMTP AUTH) in Exchange Online

The SMTP AUTH (also known as SMTP client submission) is widely supported legacy protocol that is used mostly by third party devices or software to send automated emails. Modern email clients such as Outlook rarely use this protocol anymore. The drawback of SMTP AUTH is that is does not support Modern Auth mechanisms and clients only need a username and password to send emails. This makes it a popular choice for attackers to send spam or phishing messages using compromised credentials.

As a result, it is good practice to disable SMTP AUTH for all but a few mailboxes that need it. This reduces the attack vector and helps secures your organization from abuse or harm. Enabling or disabling SMTP AUTH for your organization can be done using two settings:

- A tenant-wide setting to enable or disable SMTP AUTH

- A per-mailbox setting that overrides the tenant-wide setting

By combining these two settings, you can disable SMTP AUTH for your organization, while granting exceptions for a small number of mailboxes where SMTP AUTH is the only option for devices such as multi-function printers or software applications that need to send emails. Note these settings only apply to Office 365 hosted mailboxes.

## Tenant-wide setting

Note: The tenant setting is only available via Powershell cmdlet.

The setting *SmtpClientAuthenticationDisabled* is in the Transport configuration

Get-TransportConfig provides the current state of the setting.

The *SmtpClientAuthenticationDisabled* parameter has the following values:

- $true: SMTP AUTH client submission is disabled.

- $false: SMTP AUTH client submission is enabled. This is the default value

| **Action**                                                | **Command**                                                    |
| --------------------------------------------------------- | -------------------------------------------------------------- |
| Disable SMTP AUTH client submissions for an entire tenant | Set-TransportConfig -*SmtpClientAuthenticationDisabled $true*  |
| Enable SMTP AUTH client submissions for an entire tenant  | Set-TransportConfig -*SmtpClientAuthenticationDisabled $false* |

## Mailbox setting

To override the tenant-wide setting, you can enable individual mailboxes using the setting SmtpClientAuthenticationDisabled in CASMailbox or via the UI setting.

The Powershell commands are as follows:

| **Action**                              | **Command**                                                                     |
| --------------------------------------- | ------------------------------------------------------------------------------- |
| Enable the SMTP CS protocol for a user  | Set-CasMailbox *UserName@DomainName* –SmtpClientAuthenticationDisabled *$false* |
| Disable the SMTP CS protocol for a user | Set-CasMailbox UserName@DomainName –SmtpClientAuthenticationDisabled *$true*    |

The UI setting can be found for a given mailbox in the *Admin Portal* under *Users -\> Active Users*. After selecting a user, navigate to the *Mail* tab, and then select *Managed Email Apps*. SMTP AUTH client submission can be enabled or disabled by toggling the checkbox next to *Authenticated SMTP*.
