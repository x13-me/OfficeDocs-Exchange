---
title: "Completion of migration batch in Classic EAC in Exchange Online"
ms.author: v-aiyengar
author: AshaIyengar21
manager: serdars
audience: Admin
ms.topic: conceptual
ms.service: exchange-online
localization_priority: Normal
search.appverid: MET150
f1.keywords:
- NOCSH
description: Instructions for completion of migration batch in Classic EAC.
ms.custom: seo-marvel-jun2021
---

# Completion of migration batch in Classic EAC in Exchange Online

In Classic EAC, when the migration batch has reached the state of **Synced**, it needs to be completed.

> [!NOTE]
> When the batch starts, all the users to be migrated will be converted from MailUsers to Mailboxes. The Microsoft 365 or Office 365 Exchange license must be assigned only after this moment. You have 30 days to assign the license.

To complete the migration:

1. Under **Start the batch**, fill in the names or aliases of anyone who should be notified about the batch progress. Then select how you want to begin and complete the batch. When done, click **new**.

    ![start the batch.](../media/gsuite-mig-17-eac-start.png)

1. After the batch status changes from **Syncing** to **Synced**, you need to complete the batch. 

    ![batch syncing.](../media/gsuite-mig-18-eac-syncing.png)

The batch status will then be **Completed**.

During completion, another incremental sync is run to copy any changes that have been made to the Google Workspace mailbox. Additionally, during completion, the forwarding address that routes mail from Microsoft 365 or Office 365 to Google Workspace is removed, and a forwarding address that routes mail from Google Workspace to Microsoft 365 or Office 365 is added. This ensures that any messages received by migrated users at their Google Workspace mailboxes will be sent to their new Microsoft 365 or Office 365 address. Similarly, if any user who has not yet been migrated receives a message at their Microsoft 365 or Office 365 address, the message will get routed to their Google Workspace mailbox.
