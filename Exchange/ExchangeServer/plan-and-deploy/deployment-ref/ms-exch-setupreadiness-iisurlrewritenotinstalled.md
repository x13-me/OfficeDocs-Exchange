---
ms.localizationpriority: medium
monikerRange: exchserver-2016
description: IIS URL Rewrite Module not installed 
ms.topic: reference
author: joannehendrickson
ms.custom:
- ms.exch.setupreadiness.ForestLevelNotWin2003Native
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
# IIS URL Rewrite Module not installed  

Microsoft Exchange Server 2016 Setup can't continue because the local computer requires an additional software. You'll need to install this software before Exchange 2019 (2016) Setup can continue. 

The Setup of Exchange 2019 CU11 (2016 CU22) and above requires IIS URL Rewrite Module 2.1 to be installed on the computer before installation can continue. 

Download and install the URL Rewrite Module version 2.1 (use x64 installer of desired language from the following URL), and then click retry on the Readiness Checks page. 

IIS URL Rewrite Module 

>[!Note]
>If this update requires a reboot to complete installation, you'll need to exit the Exchange 2016 setup, reboot, and then start Setup again. 

 
>[!Important]
>After the Setup is complete, if the URL Rewrite Module is uninstalled it may lead to unresponsive ECP/OWA. 

#### Having problems?
Ask for help in the Exchange forums. Visit the forums at: [Exchange Server](https://social.technet.microsoft.com/forums/office/home?category=exchangeserver). 