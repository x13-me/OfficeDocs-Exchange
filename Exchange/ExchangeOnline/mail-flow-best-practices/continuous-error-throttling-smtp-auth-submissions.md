---
ms.topic: article
author: Benny-54
ms.author: v-bshilpa
ms.reviewer: 
description: 'Learn how handle errors in for LOB applications and services that customers have configured to send out automated emails.'
title: Continuous error throttling for SMTP AUTH submissions 
ms.collection: 
- exchange-online
- M365-email-calendar
search.appverid:
audience: Admin
f1.keywords:
ms.custom: 
ms.service: exchange-online
manager: serdars
localization_priority: Priority

---

# Continuous error throttling for SMTP AUTH submissions 

Every day, our service sees millions of requests coming in to send emails via smtp.office365.com using the SMTP AUTH protocol. Many of these are for Line-of-Business (LOB) applications and services that customers have configured to send out automated emails.  

Many of these requests that we receive, result in an error which if sent by a user from Outlook can result in the user seeing an error message that they could immediately take action on to unblock sending emails. However, many automated email applications aren't designed well to handle errors. On the contrary, they ignore errors and send continuously believing that the error will correct itself. 

For some errors such as those involving involving **Send As** or **Mailbox Full**, the issue won't correct itself without human intervention. To protect our service from bombardment from these requests and to get the message to administrators that something is wrong with the mailbox or configuration, we're introducing continuous error throttling for SMTP AUTH.

The new errors that will be seen if throttling is hit are:

 - 550 5.2.251 Sender throttled due to continuous mailbox full errors.

 - 550 5.2.252 Sender throttled due to continuous send as denied errors.

 - 550 5.2.253 Sender throttled due to continuous invalid license errors.

 - 550 5.2.254 Sender throttled due to continuous too many recipients errors.

 - 550 5.2.255 Sender throttled due to continuous invalid recipients errors.

If Exchange Online sees too many errors during submissions for a mailbox related to the five issues covered, that mailbox will be throttled from sending using SMTP AUTH specifically for a period of time.  

In many of these cases, customers might fail to notice that anything is wrong and the forgotten application will continue trying to send to no avail. However, the mailbox could be configured to send out emails successfully with one application and misconfigured with another. In such a scenario, messages that were successfully sent will be blocked as well. Lastly, if a mailbox is left to reach its size limit, a previously working application will hit this new error and be throttled if it is ignored.

It's up to administrators or users to test these applications to make sure that they work when configured. If and when these errors are hit, they'll need to investigate the misconfiguration in cases such as **Send As** denied or correct new issues such as a mailbox becoming full. Investigating this will be on the client side. These messages are not accepted by Microsoft 365 so **Message Trace** is of no help here.  

After correcting the issue, the mailbox will begin working again after the throttling period expires in the same way that hitting the Recipient Rate Limit for a mailbox requires waiting for that throttling to elapse. The throttling period will be decided by Microsoft based on a number of factors.

If customers don't want to wait that long, they can switch to using another mailbox as long as the issue has been resolved. Support is unable to lift the throttling here.  
