---
title: "Cannot write to the Exchange organization container [GlobalServerInstall]"
ms.author: dstrome
author: dstrome
manager: serdars
ms.date: 7/22/2015
ms.audience: Developer
ms.topic: reference
f1_keywords:
- 'ms.exch.setupreadiness.GlobalServerInstall'
ms.prod: exchange-server-it-pro
localization_priority: Normal
ms.assetid: 17c4667b-7db1-4e0a-b824-1f6d51d980a9
description: "Microsoft Exchange Server 2016 Setup can't continue because the logged-on user doesn't have the account permissions that are required to write to the organization container in the Active Directory directory service."
---

# Cannot write to the Exchange organization container [GlobalServerInstall]

Microsoft Exchange Server 2016 Setup can't continue because the logged-on user doesn't have the account permissions that are required to write to the organization container in the Active Directory directory service.
  
Setup requires that the user who is logged on when Exchange 2016 is installed has permission to create and modify objects in Active Directory. If you're running Exchange 2016 Setup in your organization for the first time, the account you use must be a member of the Schema Admins and Enterprise Admins groups. These permissions are required because Active Directory is prepared for Exchange 2016 the first time Setup is run. After Active Directory is prepared, the account you use to install additional Exchange 2016 servers must be a member of the Organization Management management role group.
  
To resolve this issue, grant the logged-on user the appropriate permissions, or log on with an account that has those permissions and run Exchange 2016 Setup again.
  
> [!IMPORTANT]
> Cross-forest installation of Exchange 2016 isn't supported. Use an account that is a member of the Active Directory forest where you're installing Exchange 2016.
  
Having problems? Ask for help in the Exchange forums. Visit the forums at: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkId=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkId=267542), or [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkId=285351).
  

  

