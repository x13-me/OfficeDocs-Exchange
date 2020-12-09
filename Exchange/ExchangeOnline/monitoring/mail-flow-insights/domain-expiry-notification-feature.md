---
title: "Domain expiring insight in the modern EAC"
f1.keywords:
ms.author: v-bshilpa
author: Benny-54
manager: serdars
audience: ITPro
ms.topic: article
ms.service: exchange-online
localization_priority: Normal
ms.assetid:
description: This notification feature monitors the accepted domains per tenant and sends email notification to tenant admin when any of the accepted domain is approaching expiry. 
ms.custom:
---

# Domain expiring insight in the modern EAC 

M365 customers can add their domain in system which is called Accepted domain. Once the Acceted domain is configured correctly, users in this domain can send and receive email. In order to keep a healthy mail flow, domain owned by customers should be active. Once domains expires, users configured under that domain will no longer receive emails. As these domains are owned by customers, Microsoft cannot manage these domains for customers. It is customer responsibility to monitor when a domain needs renewal. Often times, customers loose track of their domain expiry date and don’t renew it on time. This results in mail flow issue for their users as a result customers create support ticket to troubleshoot mailf flow issue and then realize the issue is due to their domain getting expired. 

Build a notification feature that monitors the accepted domains per tenant and sends email notification to tenant admin when any of the accepted domain is approaching expiry. Email warnings will be sent one a month starting 3 months before domain expire. Weekly during the last month. The notification scripts runs daily in the background. At any given point if it detects any domains that are expiring with in 90 days, 60 days or 30 days and less, it will trigger an alert. A single alert could have multiple domains for e.g. it may have one domain that is expiring in 90 days and another one that is expiring in 60 and so forth.


## Related articles

For more information, see [Mail flow insights in the modern Exchange admin center](mail-flow-insights.md).
