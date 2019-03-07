---
localization_priority: Normal
description: 'Summary: Learn about the default Client Access virtual directory settings on Mailbox servers in Exchange 2016 and Exchange 2019.'
ms.topic: article
author: msdmaguire
ms.author: dmaguire
ms.assetid: d2d89ce6-4721-4737-a325-fba5ad9422e0
ms.date: 7/5/2018
title: Default settings for Exchange virtual directories
ms.collection: exchange-server
ms.audience: ITPro
ms.prod: exchange-server-it-pro
manager: serdars

---

# Default settings for Exchange virtual directories

Exchange Server 2016 and Exchange Server 2019 automatically configure multiple Internet Information Services (IIS) virtual directories during the server installation. The tables in the following sections show the settings for the Client Access (frontend) services on Mailbox servers and the default IIS authentication and Secure Sockets Layer (SSL) settings.

## Client Access services (frontend) on Mailbox servers

The following table lists the default settings on an Exchange Mailbox server that's running Client Access services.

**Default Mailbox server running Client Access services IIS authentication and SSL settings**

|**Virtual directory**|**Authentication method**|**SSL settings**|**Management method**|
|:-----|:-----|:-----|:-----|
|Default website|Anonymous|Required|IIS management console|
|API¹|Anonymous authentication <br/> Windows authentication|SSL required <br/> Requires 128-bit encryption||
|aspnet_client|Anonymous authentication|SSL required <br/> Requires 128-bit encryption|IIS management console|
|Autodiscover|Anonymous authentication <br/> Basic authentication <br/> Windows authentication|SSL requiredRequires 128-bit encryption|EAC or Exchange Management Shell|
|ecp|Anonymous authentication <br/> Basic authentication|SSL required <br/> Requires 128-bit encryption|EAC or Exchange Management Shell|
|EWS|Anonymous authentication <br/> Windows authentication|SSL required <br/> Requires 128-bit encryption|EAC or Exchange Management Shell|
|MAPI|Windows authentication|SSL required <br/> Requires 128-bit encryption|EAC or Exchange Management Shell|
|Microsoft-Server-ActiveSync|Basic authentication|SSL required <br/> Requires 128-bit encryption|EAC or Exchange Management Shell|
|OAB|Windows authentication|SSL required <br/> Requires 128-bit encryption|EAC or Exchange Management Shell|
|owa|Basic authentication|SSL required <br/> Requires 128-bit encryption|EAC or Exchange Management Shell|
|PowerShell|By default, all authentication methods are disabled.|Not required|EAC or Exchange Management Shell|
|Rpc|Basic authentication <br/> Windows authentication|SSL required <br/> Requires 128-bit encryption|EAC or Exchange Management Shell|

¹The API virtual directory is available in Exchange 2016 CU3 or newer.

## Back End Virtual Directories on Mailbox server

The following table lists the default settings on a stand-alone Exchange Mailbox server.

**Default Mailbox server IIS authentication and SSL settings**

|**Virtual directory**|**Authentication method**|**SSL settings**|**Management method**|
|:-----|:-----|:-----|:-----|
|Exchange Back End|Anonymous authentication|SSL required <br/> Requires 128-bit encryption|This virtual directory should not be configured by the user.|
|API|Anonymous authentication <br/> Windows authentication|SSL required <br/> Requires 128-bit encryption|This virtual directory should not be configured by the user.|
|Autodiscover|Anonymous authentication <br/> Windows authentication|SSL requiredRequires 128-bit encryption|This virtual directory should not be configured by the user.|
|ecp|Anonymous authentication <br/> Windows authentication|SSL required <br/> Requires 128-bit encryption|This virtual directory should not be configured by the user.|
|EWS|Anonymous authentication <br/> Windows authentication|SSL required <br/> Requires 128-bit encryption|This virtual directory should not be configured by the user.|
|Microsoft-Server-ActiveSync|Basic authentication|SSL required <br/> Requires 128-bit encryption|This virtual directory should not be configured by the user.|
|OAB|Windows authentication|SSL required <br/> Requires 128-bit encryption|This virtual directory should not be configured by the user.|
|owa|Anonymous authentication <br/> Windows authentication|SSL required <br/> Requires 128-bit encryption|This virtual directory should not be configured by the user.|
|PowerShell|Windows authentication|SSL required <br/> Requires 128-bit encryption|This virtual directory should not be configured by the user.|
|Rpc|Windows authentication|Not required|This virtual directory should not be configured by the user.|
|RpcWithCert|Windows authentication|Not required|This virtual directory should not be configured by the user.|

## See also

[Virtual directory management](https://technet.microsoft.com/library/ff952752(v=exchg.150).aspx)

