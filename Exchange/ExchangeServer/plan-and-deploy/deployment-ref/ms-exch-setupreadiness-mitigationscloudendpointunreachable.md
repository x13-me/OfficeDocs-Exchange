---
ms.localizationpriority: medium
monikerRange: exchserver-2016
description:  Mitigations Cloud endpoint is not reachable
ms.topic: reference
author: joannehendrickson
ms.custom:
- ms-exch-setupreadiness-KB2999226NotInstalled
ms.author: jhendr
ms.reviewer: 
title: Mitigations Cloud endpoint is not reachable
ms.collection: exchange-server
f1.keywords:
- CSH
audience: ITPro
ms.prod: exchange-server-it-pro
manager: serdars
---
#  Mitigations loud endpoint is not reachable
Microsoft Exchange Server 2019 (2016) Setup displayed this warning because Setup failed to connect to Mitigation Service Cloud Endpoint from the local computer. 

The Setup of Exchange 2019 CU11 (2016 CU22) and higher version installs Emergency Mitigation (EM) Service which checks for available mitigations every hour before downloading and applying them. 

The functionality to check and download mitigations needs outbound connectivity to the Mitigation Service Cloud endpoint. Without this connectivity, the EM service can’t function which can pose a security risk. We recommend enabling connectivity with Mitigation Service Cloud endpoint to ensure the following endpoint is reachable from the computer on which Exchange Server is installed for EM service to function properly. 

|ID|Category|ER|Address|Ports|
|:-----|:-----|:-----|:-----|:-----|
||Required||officeclient.microsoft.com/*|443|

**Having problems?** Ask for help in the Exchange forums. Visit the forums at: [Exchange Server](https://social.technet.microsoft.com/forums/office/home?category=exchangeserver)