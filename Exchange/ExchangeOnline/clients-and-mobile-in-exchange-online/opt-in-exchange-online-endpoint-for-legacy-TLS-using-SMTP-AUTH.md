---
localization_priority: Normal
description: 'Learn how to opt-in to Exchange Online endpoint for legacy TLS clients using SMTP AUTH.'
ms.topic: overview
author: joannehendrickson
ms.author: jhendr
ms.reviewer: 
title: "Opt-in to Exchange Online endpoint for legacy TLS clients using SMTP AUTH"
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
 
As of October 2020, Exchange Online no longer supports the use of TLS1.0 and TLS1.1 due to our service's compliance requirements. While no longer supported, our servers still allow clients to use older versions of TLS when connecting with us. 

In 2022, we plan to completely disable the older TLS versions to secure our customers and meet compliance requirements. However, in response to significant usage, we've created an "opt-in" endpoint that legacy clients can use with TLS1.0 and TLS1.1. 
 
## Configuring the new endpoint

If you have SMTP AUTH clients that only support older TLS versions, they need to be configured to use the new endpoint:

- smtp-legacy.office365.com 
 
To use any of these endpoints, admins need to enable the following setting:

- The AllowLegacyTLSClients parameter on the Set-TransportConfig cmdlet.

Configure the affected mailbox to allow SMTP AUTH, if you haven't already done so. To learn more, see: [Enable or disable authenticated client SMTP submission (SMTP AUTH) in Exchange Online](/microsoft.com/exchange/clients-and-mobile-in-exchange-online/authenticated-client-smtp-submission)

 
 
## Opt-in to legacy clients’ endpoint 

You can only opt-in (or opt-out) for your organization by using [Exchange Online PowerShell](/powershell/exchange/connect-to-exchange-online-powershell).

To opt-in, run the following command:

```PowerShell
 
Set-TransportConfig -AllowLegacyTLSClients $true

```

## How do you know this procedure worked?

To confirm that the change has taken effect, send a message using the new endpoint. Only mailboxes for organizations with the setting enabled can send using that endpoint, whatever TLS version is used. 
