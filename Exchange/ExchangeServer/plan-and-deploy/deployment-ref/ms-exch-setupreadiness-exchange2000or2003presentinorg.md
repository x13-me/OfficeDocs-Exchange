---
title: "Can't install Exchange 2016 in a forest that contains Exchange 2000 or Exchange 2003 servers. [Exchange2000or2003PresentInOrg]"
ms.author: dstrome
author: dstrome
manager: serdars
ms.date: 4/19/2018
ms.audience: ITPro
ms.topic: reference
f1_keywords:
- 'ms.exch.setupreadiness.Exchange2000or2003PresentInOrg'
ms.prod: exchange-server-it-pro
localization_priority: Normal
ms.assetid: a115b182-cbd2-4d31-aa0e-375240939301
description: "Microsoft Exchange Server 2016 can't continue because one or more computers are running Exchange 2007 or older were found in the Active Directory forest. Before you can install Exchange 2016, all computers running Exchange 2007 or older must be removed from the forest. Mailboxes, public folders, and all other Exchange objects or components must be upgraded to the latest release of Exchange Server 2010."
---

# Can't install Exchange 2016 in a forest that contains Exchange 2000 or Exchange 2003 servers. [Exchange2000or2003PresentInOrg]

Microsoft Exchange Server 2016 can't continue because one or more computers are running Exchange 2007 or older were found in the Active Directory forest. Before you can install Exchange 2016, all computers running Exchange 2007 or older must be removed from the forest. Mailboxes, public folders, and all other Exchange objects or components must be upgraded to the latest release of Exchange Server 2010.
  
The path you need to follow to install Exchange 2016 in your organization depends on the version of Exchange you currently have installed in your forest. See the following table for more information.
  
|**If you have the following installed in your organization**|**You must take this path to upgrade to Exchange 2016**|
|:-----|:-----|
|Exchange 2000  <br/> |1. Install Exchange 2007 into your Exchange 2000 organization.  <br/> 2. Configure Exchange 2007 and Exchange 2000 coexistence.  <br/> 3. Migrate Exchange 2000 mailboxes, public folders, and other components to Exchange 2007.  <br/> 4. Decommission and remove all Exchange 2000 servers.  <br/> 5. Install Exchange 2013 into your Exchange 2007 organization.  <br/> 6. Configure Exchange 2013 and Exchange 2007 coexistence.  <br/> 7. Migrate Exchange 2007 mailboxes, public folders, and other components to Exchange 2013.  <br/> 8. Decommission and remove all Exchange 2007 servers.  <br/> 9. Install Exchange 2016 into your Exchange 2013 organization.  <br/> 10. Configure Exchange 2016 and Exchange 2013 coexistence.  <br/> 11. Migrate Exchange 2013 mailboxes, public folders, and other components to Exchange 2016.  <br/> 12. Decommission and remove all Exchange 2013 servers.  <br/> |
|Exchange 2003  <br/> |1. Install Exchange 2010 into your Exchange 2003 organization.  <br/> 2. Configure Exchange 2010 and Exchange 2003 coexistence.  <br/> 3. Migrate Exchange 2003 mailboxes, public folders, and other components to Exchange 2010.  <br/> 4. Decommission and remove all Exchange 2003 servers.  <br/> 5. Install Exchange 2016 into your Exchange 2010 organization.  <br/> 6. Configure Exchange 2016 and Exchange 2010 coexistence.  <br/> 7. Migrate Exchange 2010 mailboxes, public folders, and other components to Exchange 2016.  <br/> 8. Decommission and remove all Exchange 2010 servers.  <br/> |
|Exchange 2007  <br/> |1. Install Exchange 2013 into your Exchange 2007 organization.  <br/> 2. Configure Exchange 2013 and Exchange 2007 coexistence.  <br/> 3. Migrate Exchange 2007 mailboxes, public folders, and other components to Exchange 2013.  <br/> 4. Decommission and remove all Exchange 2007 servers.  <br/> 5. Install Exchange 2016 into your Exchange 2013 organization.  <br/> 6. Configure Exchange 2016 and Exchange 2013 coexistence.  <br/> 7. Migrate Exchange 2013 mailboxes, public folders, and other components to Exchange 2016.  <br/> 8. Decommission and remove all Exchange 2013 servers.  <br/> |
   
When upgrading to Exchange 2010 or later, you can use the Exchange Deployment Assistant to help you complete your deployment. For more information, see the following links:
  
- [Exchange 2010 Deployment Assistant](https://go.microsoft.com/fwlink/p/?LinkId=171086)
    
- [Exchange 2013 Deployment Assistant](https://go.microsoft.com/fwlink/p/?LinkId=277105)
    
Having problems? Ask for help in the Exchange forums. Visit the forums at: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkId=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkId=267542), or [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkId=285351).
  

  

