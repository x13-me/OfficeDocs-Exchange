---
title: "Reply-all storm protection report in the new EAC in Exchange Online"
f1.keywords:
- NOCSH
ms.author: v-bshilpa
author: Benny-54
manager: serders
audience: ITPro
ms.topic: article
ms.service: exchange-online
ms.localizationpriority: medium
ms.assetid:
description: "Admins can learn how to use the Reply-all storm protection report in the new Exchange admin center to identify and troubleshoot mail flow in your email domains."
---

# Reply-all storm protection report in the new Exchange admin center in Exchange Online

The Reply-all storm protection report in the new Exchange admin center (new EAC) **Reports** > **Mail flow** section displays information about detected reply-all storms in your organization and the reply-all messages that were blocked. 

> [!NOTE]
> For more information on permissions that are required to use this report, see [Permissions required to view mail flow reports](/exchange/monitoring/mail-flow-reports/mail-flow-reports#permissions-required-to-view-mail-flow-reports).

![Reply-all storm protection report1](../../media/reply-all-storm-protection-report.png)

The top of the report shows the current settings used by Reply-all Storm Protection for detecting and blocking reply-all messages during a reply-all storm.

 - Minimum recipients
 
 - Minimum reply-alls
 
 - Block duration hours
 
> [!NOTE]
> The current settings might not reflect the settings used for reply-all storms in the past if the current settings were changed during or after those storms occurred. Changing the settings while a storm is happening might not apply those settings to the current storm.

Beneath the current settings is the time/date range drop-down from which you can select to view from 3 hours to 90 days of data (with the last 3 hours as default). 

The overview section shows these two charts: 

 - **Detected reply-all storm messages**

 - **Messages blocked**

**Detected reply-all storm messages** shows the number of reply-all messages for a particular message thread were detected during the preceding time-interval. For example, in the chart above the 5 reply-all messages for the "Happy Thanksgiving" thread shown at 3pm were detected between 2:45 and 3pm. Reply-all messages sent before a reply-all storm is identified won't get blocked. But they are included as part of the **Detected reply-all storm messages** chart values, as are the blocked messages.

> [!NOTE]
> This chart displays data only for declared reply-all storms where at least one reply-all message has been blocked. It can't be used to track potential storms before they're declared a reply-all storm, or view "near" storms that never exceeded the detection thresholds.

The **Messages blocked** chart includes a sub-set of the messages shown in the **Detected reply-all storm messages** chart. It shows the number of reply-all messages blocked during the *Blocked duration hours* time frame.

Selecting any one of the reply-all storm names in either chart will pop-up a side panel showing specific details about the selected reply-all storm, as shown below. 

![Reply-all report](../../media/reply-all-storm-protection-report-current-settings.md.png)

The reply-all storm panel includes the following information about the storm:

|**Item**|**Description**|
|:-----|:-----|
|**Subject**|The message subject of the initial message.|
|**Original Sender**|The sender of the first message in the conversation thread.|
|**Start Date/Time**|When the first reply-all message was sent.|
|**Total Messages**|The total number of messages in the conversation thread (includes the first message ).|
|**Blocked Messages**|The total number of messages blocked by the feature. This is always lower than the total messages in the storm. Due to the time required to synchronize the block enforcement notification to all relevant servers in the service, this number can also be a bit lower than expected as a few reply-alls might get sent before the senders' servers start to block them. |
|**Block Start Time**|Time of the first message block.|
|**Message ID**|The Message ID of the first message in the conversation thread.|
|**Reply-all senders**|Users who sent (or tried to send) a reply-all to the thread. Includes whether or not the message they sent was allowed through or blocked.|

The final section of the main report page, **Reply-all storm details**, shows a table of all the reply-all storms as shown in the above charts. It also incudes the  key details about each of the following:

 - **Start and end dates/Times**

 - **Subject**

 - **Original Sender**

 - **Total Messages**

 - **Blocked Messages**

 - **Message ID**

Click **Export** to export the displayed results to a .csv file. 

## See also

For more information about other mail flow reports, see [Mail flow reports in the modern EAC](/exchange/monitoring/mail-flow-reports/mail-flow-reports).



 
