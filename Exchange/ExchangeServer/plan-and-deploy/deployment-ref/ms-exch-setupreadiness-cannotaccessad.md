---
title: "Active Directory does not exist or cannot be contacted [CannotAccessAD]"
ms.author: dstrome
author: dstrome
manager: serdars
ms.date: 12/20/2016
ms.audience: Developer
ms.topic: reference
f1_keywords:
- 'ms.exch.setupreadiness.CannotAccessAD'
ms.prod: exchange-server-it-pro
localization_priority: Normal
ms.assetid: 56adb6fe-ecb8-4a7f-b440-89aa401c28b7
description: "Microsoft Exchange Server 2016 Setup can't continue because it can't contact a valid Active Directory directory service site. Setup requires that the server you're installing Exchange on is able to locate the configuration naming context in Active Directory."
---

# Active Directory does not exist or cannot be contacted [CannotAccessAD]

Microsoft Exchange Server 2016 Setup can't continue because it can't contact a valid Active Directory directory service site. Setup requires that the server you're installing Exchange on is able to locate the configuration naming context in Active Directory.
  
To resolve this issue, verify that the user account running Exchange Setup is an Active Directory user and then run Setup again. If this doesn't resolve the issue, follow the guidance about using the dcdiag.exe and repadmin.exe support tools from the topics below to further diagnose the problem.
  
For more information about Active Directory troubleshooting and configuration for Exchange, see the following topics:
  
- [Prepare Active Directory and domains](../../plan-and-deploy/prepare-ad-and-domains.md)
    
- [Troubleshooting Active Directory Domain Services](https://go.microsoft.com/fwlink/p/?LinkId=272144)
    
- [Configuring a Computer for Troubleshooting](https://go.microsoft.com/fwlink/p/?LinkId=272141)
    
- [Troubleshooting Active Directory Replication Problems](https://go.microsoft.com/fwlink/p/?LinkId=272142)
    
- [Monitoring and Troubleshooting Active Directory Replication Using Repadmin](https://go.microsoft.com/fwlink/p/?LinkId=272143)
    
Having problems? Ask for help in the Exchange forums. Visit the forums at: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkId=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkId=267542), or [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkId=285351).
