---
title: "Can't install Exchange 2016 in a forest that contains Exchange 2000 or Exchange 2003 servers. [Exchange2000or2003PresentInOrg]"
ms.author: chrisda
author: chrisda
manager: serdars
ms.date: 8/3/2018
ms.audience: ITPro
ms.topic: reference
f1_keywords:
- 'ms.exch.setupreadiness.Exchange2000or2003PresentInOrg'
ms.prod: exchange-server-it-pro
localization_priority: Normal
ms.assetid: a115b182-cbd2-4d31-aa0e-375240939301
description: "Exchange Server 2016 or Exchange Server 2019 Setup can't continue because an older version of Exchange that isn't supported for coexistence was found in the Active Directory forest."
---

# Can't install Exchange 2016 in a forest that contains Exchange 2000 or Exchange 2003 servers. [Exchange2000or2003PresentInOrg]

Exchange Setup can't continue because a version of Exchange that's too old for coexistence with the version that you're installing was found in the Active Directory forest. Before you can continue, you need to eliminate all unsupported versions of Exchange from your forest, which might require that you to upgrade to an interim version of Exchange first.
  
The upgrade path that you need to follow depends on your current verision of Exchange. The upgrade paths are described in the following table:

>[!NOTE]
>When you need to upgrade to an interim version of Exchange, you need to migrate all mailboxes, public folders and other components onto the interim version of Exchange before you decomission and remove the earlier Exchange servers.
  
|**Current Exchange version**|**Latest Exchange version for coexistence**|**Upgrade path summary**|
|:-----|:-----|:-----|
|Exchange 2000|Exchange 2007|• Exchange 2000 \> Exchange 2007 \> Exchange 2013 \> Exchange 2016. <br/> or <br/>• Exchange 2000 \> Exchange 2007 \> Exchange 2013 \> Exchange 2019|
|Exchange 2003|Exchange 2010|• Exchange 2003 \> Exchange 2010 \>  Exchange 2016. <br/> or <br/>• Exchange 2003 \> Exchange 2010 \> Exchange 2016 \> Exchange 2019.|
|Exchange 2007|Exchange 2013|• Exchange 2007 \> Exchange 2013 \> Exchange 2016. <br/> or <br/>• Exchange 2007 \> Exchange 2013 \> Exchange 2019.|
|Exchange 2010|Exchange 2016|• Exchange 2010 \> Exchange 2016. <br/> or <br/>•  Exchange 2010 \> Exchange 2016 \> Exchange 2019.
   
In Exchange 2010 or later, you can use the Exchange Deployment Assistant to help you complete your deployment. For more information, see [Exchange Deployment Assistant](https://docs.microsoft.com/exchange/exchange-deployment-assistant)

Having problems? Ask for help in the Exchange forums. Visit the forums at: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkId=60612).
