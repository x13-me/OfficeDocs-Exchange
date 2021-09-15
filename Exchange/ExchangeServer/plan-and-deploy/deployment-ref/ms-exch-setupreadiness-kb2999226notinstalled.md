---
ms.localizationpriority: medium
monikerRange: exchserver-2016
description: IIS URL Rewrite Module not installed 
ms.topic: reference
author: joannehendrickson
ms.custom:
- ms-exch-setupreadiness-KB2999226NotInstalled
ms.author: jhendr
ms.reviewer: 
title: IIS URL Rewrite Module not installed 
ms.collection: exchange-server
f1.keywords:
- CSH
audience: ITPro
ms.prod: exchange-server-it-pro
manager: serdars

---
## Update for Universal C Runtime in Windows (KB2999226) not installed  

Microsoft Exchange Server 2016 Setup can't continue because the local computer requires a software update. You'll need to install this update before Exchange 2019 (2016) Setup can continue. 

The Setup of Exchange 2016 CU22 and above requires an Update for Universal C Runtime in Windows (KB2999226) to be installed on the computer before installation can continue. 

1. Download and install: [Universal C Runtime in Windows (KB2999226)](https://support.microsoft.com/en-us/topic/update-for-universal-c-runtime-in-windows-c0514201-7fe6-95a3-b0a5-287930f3560c)  
2. Select **retry** on the **Readiness Checks page**.



>[!Note]
>If this update requires a reboot to complete installation, you'll need to exit Exchange 2016 setup, reboot, and then start setup again. 

**Having problems?** Ask for help in the Exchange forums. Visit the forums at: [Exchange Server](https://social.technet.microsoft.com/forums/office/home?category=exchangeserver)