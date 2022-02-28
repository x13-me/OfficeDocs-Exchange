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
> The current settings might not reflect the settings used for past reply-all storms if the current settings were changed during or after those storms occurred. Changing the settings while a storm is happening, might not apply those settings to that specific storm, but will apply to future storms.

Beneath the current settings, is the time/date range drop-down from which you can select to view from 3 hours to 90 days of data (with the last 3 hours as default). 

The overview section shows these two charts: 

 - **Detected reply-all storm messages**
 - **Messages blocked**

**Detected reply-all storm messages** shows the number of reply-all messages for a particular message thread that were detected during the preceding time-interval. For example, in the chart above the five reply-all messages for the "Happy Thanksgiving" thread shown at 3pm were detected between 2:45 and 3pm. Reply-all messages sent before a reply-all storm are identified and won't get blocked. Yet, they're included as part of the **Detected reply-all storm messages** chart values, as are the blocked messages.

> [!NOTE]
> This chart displays data only for declared reply-all storms where at least one reply-all message has been blocked. It can't be used to track potential storms before they're declared a reply-all storm.

The **Messages blocked** chart includes a subset of the messages shown in the **Detected reply-all storm messages** chart. It shows the number of reply-all messages blocked during the *Blocked duration hours* time frame.

Selecting any one of the reply-all storm names in either chart will pop up a side panel showing specific details about the selected reply-all storm, as shown below. 

![Reply-all report](../../media/reply-all-storm-protection-report-current-settings.png)

The reply-all storm details panel includes the following information about the storm:

|**Item**|**Description**|
|:-----|:-----|
|**Subject**|The message subject of the initial message.|
|**Original Sender**|The sender of the first message in the conversation thread.|
|**Start Date/Time**|When the first reply-all message was sent.|
|**Total Messages**|The total number of messages in the conversation thread (includes the first message).|
|**Blocked Messages**|The total number of messages blocked by the feature. This is always lower than the total messages in the storm, and in some cases it might be lower than expected based on the feature settings. It can take from a few seconds to a few minutes to synchronize the block enforcement notification to all relevant servers in the service, and during that time a few reply-alls could still get through before blocking kicks-in.|
|**Block Start Time**|Time when message blocking started.|
|**Message ID**|The Message ID of the first message in the conversation thread.|
|**Reply-all senders**|Users who sent (or tried to send) a reply-all to the thread. Includes whether or not the message they sent was allowed through or blocked.|

The final section of the main report page, **Reply-all storm details**, shows a table of all the reply-all storms shown in the above charts for the selected time/date range. It also includes the key details about each of the following:

 - **Start and end dates/Times**
 - **Subject**
 - **Original Sender**
 - **Total Messages**
 - **Blocked Messages**
 - **Message ID**

Click **Export** to export the displayed results to a .csv file. 

## See also

For more information about other mail flow reports, see [Mail flow reports in the modern EAC](/exchange/monitoring/mail-flow-reports/mail-flow-reports).



 
