---
title: "Installing Exchange on a domain controller is not recommended [WarningInstallExchangeRolesOnDomainController]"
ms.author: dstrome
author: dstrome
manager: serdars
ms.date: 7/22/2015
ms.audience: Developer
ms.topic: reference
f1_keywords:
- 'ms.exch.setupreadiness.WarningInstallExchangeRolesOnDomainController'
ms.prod: exchange-server-it-pro
localization_priority: Normal
ms.assetid: 48922de2-a68c-4092-96a5-d38c8e5f49f5
description: "Microsoft Exchange Server 2016 Setup has detected that the computer you're attempting to install Exchange 2016 on is an Active Directory domain controller. Installing Exchange 2016 on a domain controller isn't recommended."
---

# Installing Exchange on a domain controller is not recommended [WarningInstallExchangeRolesOnDomainController]

Microsoft Exchange Server 2016 Setup has detected that the computer you're attempting to install Exchange 2016 on is an Active Directory domain controller. Installing Exchange 2016 on a domain controller isn't recommended.
  
If you install Exchange 2016 on a domain controller, be aware of the following issues:
  
- Configuring Exchange 2016 for Active Directory split permissions isn't supported.
    
- The Exchange Trusted Subsystem universal security group (USG) is added to the Domain Admins group when Exchange is installed on a domain controller. When this occurs, all Exchange servers in the domain are granted domain administrator rights in that domain.
    
- Exchange Server and Active Directory are both resource-intensive applications. There are performance implications to be considered when both are running on the same computer.
    
- You must make sure that the domain controller Exchange 2016 is installed on is a global catalog server.
    
- Exchange services may not start correctly when the domain controller is also a global catalog server.
    
- System shutdown will take considerably longer if Exchange services aren't stopped before shutting down or restarting the server.
    
- Demoting a domain controller to a member server isn't supported.
    
- Running Exchange 2016 on a clustered node that is also an Active Directory domain controller isn't supported.
    
We recommend that you install Exchange 2016 on a member server.
  
Having problems? Ask for help in the Exchange forums. Visit the forums at: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkId=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkId=267542), or [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkId=285351).
