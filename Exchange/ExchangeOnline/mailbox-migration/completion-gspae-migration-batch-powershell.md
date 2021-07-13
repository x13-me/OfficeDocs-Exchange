---
title: "Completion of migration batch in PowerShell"
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
description: Instructions for completion of migration batch in PowerShell.
ms.custom: seo-marvel-jun2021
---

# Completion of migration batch in PowerShell

In PowerShell, when the migration batch has reached the state of **Synced**, it needs to be completed by running the `Complete-MigrationBatch` cmdlet.

> [!NOTE]
    > When the batch starts, all the users to be migrated will be converted from MailUsers to Mailboxes. The Microsoft 365 or Office 365 Exchange license must be assigned only after this moment. You have 30 days to assign the license.

During completion, another incremental sync is run to copy any changes that have been made to the Google Workspace mailbox. Additionally, the forwarding address that routes mail from Office 365 to Google Workspace is removed, and a forwarding address that routes mail from Google Workspace to Office 365 is added.

> [!NOTE]
> Forwarding addresses are not needed when doing a cutover migration from Google Workspace to Exchange Online.
