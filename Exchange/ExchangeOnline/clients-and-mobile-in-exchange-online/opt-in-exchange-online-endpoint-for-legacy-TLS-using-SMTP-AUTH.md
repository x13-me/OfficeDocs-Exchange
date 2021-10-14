---
ms.localizationpriority: medium
description: Learn how to opt-in to Exchange Online endpoint for legacy TLS clients using SMTP AUTH.
ms.topic: overview
author: joannehendrickson
ms.author: jhendr
ms.reviewer:
title: Opt-in to Exchange Online endpoint for legacy TLS clients using SMTP AUTH in Exchange Online
ms.collection:
- exchange-online
- M365-email-calendar
audience: ITPro
ms.service: exchange-online
f1.keywords:
- NOCSH
manager: serdars

---

# Opt-in to Exchange Online endpoint for legacy TLS clients using SMTP AUTH

Exchange Online no longer supports use of TLS1.0 and TLS1.1 in the service as of October 2020. This is due to security and compliance requirements for our service. While no longer supported, our servers still allow clients to use those older versions of TLS when connecting to the SMTP AUTH endpoint (smtp.office365.com).

In 2022, we plan to completely disable those older TLS versions to secure our customers and meet those security and compliance requirements. However, due to significant usage, we've created an opt-in endpoint that legacy clients can use with TLS1.0 and TLS1.1.

## Configuring the new endpoint

If customers have SMTP AUTH clients that only support older TLS versions, they need to be configured to use the new endpoint:

- `smtp-legacy.office365.com`

To use this less secure endpoint, admins need to enable the following setting:

- The value `$true` for the _AllowLegacyTLSClients_ parameter on the **Set-TransportConfig** cmdlet.

Make sure that the mailbox is configured to allow sending using SMTP AUTH. For more info, visit: [Enable or disable authenticated client SMTP submission (SMTP AUTH) in Exchange Online](/exchange/clients-and-mobile-in-exchange-online/authenticated-client-smtp-submission)

## Opt-in to legacy client endpoint

You can only opt-in (or opt-out) for your organization by using [Exchange Online PowerShell](/powershell/exchange/connect-to-exchange-online-powershell).

To opt-in, run the following command:

```PowerShell
Set-TransportConfig -AllowLegacyTLSClients $true
```

To view the current status of the property, run the following command in Exchange Online PowerShell:

```powershell
Get-TransportConfig | Format-List AllowLegacyTLSClients
```
