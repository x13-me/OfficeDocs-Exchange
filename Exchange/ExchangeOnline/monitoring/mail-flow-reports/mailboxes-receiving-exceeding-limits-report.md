---
title: "Mailboxes exceeding receiving limits report in the new EAC"
f1.keywords:
ms.author: v-bshilpa
author: Benny-54
manager: serdars
audience: ITPro
ms.topic: article
ms.service: exchange-online
localization_priority: Normal
ms.assetid:
description:  
ms.custom:
---

# Mailboxes exceeding receiving limits report in the new EAC

The Mailboxes exceeding receiving limits report in the new Exchange Admin Center (new EAC) displays information on mailboxes that are receiving large volumes of messages in a short amount of time.

There are two sections to this report:

1. A chart that indicates when a mailbox exceeded their receiving limit (see Exchange Online limits), which means they can no longer receive mail until the limit is reset (that is 1 hour after the threshold is exceeded).

   1. Mailboxes will not receive any mail at all if the overall receiving limit is exceeded.
      
   2. Mailboxes will not receive any mail from a specific sender, if the mailbox has received too many messages from the sender.
      
2. And a chart that indicates when a mailbox is at risk, which means they haven’t exceeded their limit but are receiving large volumes of messages regularly.

3. A table that shows, in the selected time window:

   - The number of hours a mailbox as exceeded
   
   - The number of hours a mailbox is at risk
   
   - The maximum number of messages they received per hour
   
   - The top sender 
   
   - The percentage of mail that was spam
   
Changing the Time, Type filters, or searching for a mailbox, will change both the chart and the table. 

> [!NOTE]
> The default view is for the last 24 hours for all types. If no data is showing, that means you had no mailboxes exceeding the limit (or at risk) in the last 24 hours.

> [!NOTE]
> The chart is limited to showing the top 10 mailboxes. If you’d like to see more mailboxes, you’ll have to filter/search differently. 

[image]

1. Click **Export** to download the data as a csv.

2. Click **Share** to share the details with others. 

3. Select a mailbox address to view in detail the mailbox owner’s contact information. Contact the mailbox owner to understand why they are receiving so much email, so they can reduce their mail volume and have a better experience.

