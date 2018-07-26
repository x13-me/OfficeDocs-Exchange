---
title: "Installation on domain controllers is not supported with Active Directory split permissions [InstallOnDCInADSplitPermissionMode]"
ms.author: dstrome
author: dstrome
manager: serdars
ms.date: 7/22/2015
ms.audience: ITPro
ms.topic: reference
f1_keywords:
- 'ms.exch.setupreadiness.InstallOnDCInADSplitPermissionMode'
ms.prod: exchange-server-it-pro
localization_priority: Normal
ms.assetid: 977e3758-5e09-40a2-80c1-fe344b1d8a2a
description: "Microsoft Exchange Server 2016 Setup has detected that you're attempting to run Setup on an Active Directory domain controller and one of the following is true:"
---

# Installation on domain controllers is not supported with Active Directory split permissions [InstallOnDCInADSplitPermissionMode]

Microsoft Exchange Server 2016 Setup has detected that you're attempting to run Setup on an Active Directory domain controller and one of the following is true:
  
- The Exchange organization is already configured for Active Directory split permissions.
    
- You selected the Active Directory split permissions option in Exchange 2016 Setup.
    
The installation of Exchange 2016 on domain controllers isn't supported when the Exchange organization is configured for Active Directory split permissions.
  
If you want to install Exchange 2016 on a domain controller, you must configure the Exchange organization for Role Based Access Control (RBAC) split permissions or shared permissions.
  
> [!IMPORTANT]
> We don't recommend installing Exchange 2016 on Active Directory domain controllers. For more information, see [Installing Exchange on a domain controller is not recommended [WarningInstallExchangeRolesOnDomainController]](ms-exch-setupreadiness-warninginstallexchangerolesondomaincontroller.md).
  
If you want to continue using Active Directory split permissions, you must install Exchange 2016 on a member server.
  
For more information about split and shared permissions in Exchange 2016 , see the following topics:
  
[Understanding Split Permissions](http://technet.microsoft.com/library/2b709e15-63a2-4841-94bc-b289b71166d0.aspx)
  
[Configure Exchange 2013 for Split Permissions](http://technet.microsoft.com/library/8c74f893-a6f3-4869-8571-3bc0f662cc87.aspx)
  
[Configure Exchange 2013 for Shared Permissions](http://technet.microsoft.com/library/7d119977-b420-4b66-acf0-0a978b188cdd.aspx)
  
Having problems? Ask for help in the Exchange forums. Visit the forums at: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkId=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkId=267542), or [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkId=285351).
