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

The SMTP AUTH protocol is used by our customers' email clients to submit millions of email messages every day. Most of these clients are devices such as multi-function printers or applications that send automated email messages. Modern email clients (for example, Outlook) rarely use this protocol and instead use protocols that are secured by Modern Auth.

 SMTP AUTH (also known as authenticated SMTP client submission) is a standard (legacy) internet protocol that uses Basic authentication to send messages. By design, SMTP AUTH doesn’t support Modern Auth, and requires only a valid username and password to send messages. Attackers often use compromised accounts and SMTP AUTH to send large quantities of spam.

To reduce what attackers can do with compromised user credentials, we are taking steps to reduce access to Office 365 mailboxes by using SMTP AUTH. We’ll start by disabling SMTP AUTH for new tenants by default. Don’t worry; admins will sill be able to enable SMTP AUTH for specific mailboxes as needed.

Currently, all tenants have a setting to globally disable SMTP AUTH. Each mailbox also has a setting to override the global setting and enable SMTP AUTH. These two settings allow you to disable SMTP AUTH for most mailboxes, and enable it for a select few mailboxes.

Starting November 1, 2019, we’ll begin updating the global setting to disable SMTP AUTH for new Office 365 organizations. Admins for these new tenants will need to enable SMTP AUTH for any mailboxes that require it. Note that implementing this setting will take time, so new customers should not automatically assume that SMTP AUTH is disabled in their organization (admins can check the global setting to make sure).

The next step in early 2020 will be to disable SMTP AUTH for existing tenants who’ve never used it to send messages. Affected customers will receive targeted Message Center posts to let them know when this change is coming. Finally, the remaining customers who still have some mailboxes using SMTP AUTH will be addressed.

Until then, admins are free to take proactive steps to disable SMTP AUTH globally for their organization or for mailboxes that do not require it.

More details on the SMTP AUTH settings and how to determine what mailboxes are using SMTP AUTH can be found \<here\>.

Support article: Disabling SMTP AUTH client submission for your organization

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
