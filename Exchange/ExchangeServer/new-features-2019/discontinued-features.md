---
title: "What's discontinued in Exchange 2019"
ms.author: dmaguire
author: msdmaguire
manager: scotv
ms.date: 7/27/2018
ms.audience: ITPro
ms.topic: overview
ms.prod: exchange-server-it-pro
localization_priority: Priority
ms.assetid: 
description: "This topic discusses the components, features, or functionality that have been removed, discontinued, or replaced in Exchange 2019."
---

# What's discontinued in Exchange 2019

This topic discusses the components, features, and functionality that's been removed, discontinued, or replaced in Exchange 2019.

## Discontinued features from Exchange 2016 to Exchange 2019

This section lists the Exchange 2016 features that are no longer available in Exchange 2019.

### Architecture

|**Feature**|**Comments and mitigation**|
|:-----|:-----|
|Unified Messaging (UM)|Unified Messaging has been removed from Exchange 2019. We recommend that Exchange 2019 organizations transition to Skype for Business Cloud Voice Mail.|

## Discontinued features from Exchange 2013 to Exchange 2019

This section lists the Exchange 2013 features that are no longer available in Exchange 2019.

### Architecture

|**Feature**|**Comments and mitigation**|
|:-----|:-----|
|Unified Messaging (UM)|Unified Messaging has been removed from Exchange 2019. We recommend that Exchange 2019 organizations transition to Skype for Business Cloud Voice Mail.|
|Client Access server role|The Client Access server role has been replaced by Client Access services that run on the Mailbox server role. The Mailbox server role now performs all functionality that was previously included with the Client Access server role. For more information about the new Mailbox server role, see [Exchange Server architecture](../architecture/architecture.md).|
|MAPI/CDO library|The MAPI/CDO library has been replaced by Exchange Web Services (EWS), Exchange ActiveSync (EAS), and Representational State Transfer (REST)<sup>\*</sup> APIs. If an application uses the MAPI/CDO library, it needs to move to EWS, EAS, or the REST APIs to communicate with Exchange 2019.|
 
<sup>\*</sup> REST APIs will be included in a future release of Exchange 2019.

## De-emphasized features in Exchange 2019

The following features are being de-emphasized in Exchange 2019 and may not be included in future versions of Exchange.

- Third-party replication APIs

- RPC over HTTP

- Database availability group (DAG) support for failover cluster administrative access points
