---
title: "Duplicate Microsoft Exchange System Objects container exists in Active Directory [AdInitErrorRule]"
ms.author: dstrome
author: dstrome
manager: serdars
ms.date: 7/22/2015
ms.audience: Developer
ms.topic: reference
f1_keywords:
- 'ms.exch.setupreadiness.AdInitErrorRule'
ms.prod: exchange-server-it-pro
localization_priority: Normal
ms.assetid: cd0f45ab-89de-4653-b50d-c1157c2329d5
description: "Microsoft Exchange Server 2016 Setup can't continue because it found a duplicate Microsoft Exchange System Objects container in Active Directory Domain Naming context. When Setup finds a duplicate Microsoft Exchange System Objects container, you must delete the duplicate container before Setup can continue. When a duplicate Microsoft Exchange System Objects container exists, you can't solve the problem by running DomainPrep again. You must identify and delete the duplicate Microsoft Exchange System Objects container."
---

# Duplicate Microsoft Exchange System Objects container exists in Active Directory [AdInitErrorRule]

Microsoft Exchange Server 2016 Setup can't continue because it found a duplicate Microsoft Exchange System Objects container in Active Directory Domain Naming context. When Setup finds a duplicate Microsoft Exchange System Objects container, you must delete the duplicate container before Setup can continue. When a duplicate Microsoft Exchange System Objects container exists, you can't solve the problem by running **DomainPrep** again. You must identify and delete the duplicate Microsoft Exchange System Objects container.
  
To resolve this issue, do the following:
  
1. Log on to the domain controller with administrative credentials.
    
2. In **Administrative Tools**, click **Active Directory Users and Computers**.
    
3. In the **Active Directory Users and Computers** management console pane, click **View** from the toolbar menu and then select **Advanced Features**.
    
4. Locate the duplicate Microsoft Exchange System Objects container.
    
5. Verify the duplicate Microsoft Exchange System Objects container doesn't contain valid Active Directory objects.
    
6. Right-click the duplicate Microsoft Exchange System Objects container, and then click **Delete**.
    
7. Confirm the deletion by clicking **Yes** in the Active Directory dialog box.
    
> [!NOTE]
> If you want the change to be replicated immediately, you must manually initiate replication between domain controllers.
  
Having problems? Ask for help in the Exchange forums. Visit the forums at: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkId=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkId=267542), or [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkId=285351).
