---
title: "Completion of migration batch"
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
description: Instructions for migrating from Google Workspace to Microsoft 365 or Office 365 in stages by migrating users in batches.
ms.custom: seo-marvel-jun2021
---

# Completion of migration batch

Based on whether you are using New EAC, Classic EAC, or Powershell cmdlets to perform the migration, the completion process differs.

During completion, another incremental sync is run to copy any changes that have been made to the Google Workspace mailbox. Additionally, the forwarding address that routes mail from Office 365 to Google Workspace is removed, and a forwarding address that routes mail from Google Workspace to Office 365 is added.

> [!NOTE]
> Forwarding addresses are not needed when doing a cutover migration from Google Workspace to Exchange Online.

## Finalizing your migration

After you have successfully migrated all of your Google Workspace users to Microsoft 365 or Office 365, you can switch your primary MX record to point to Microsoft 365 or Office 365. The update to the MX record will propagate slowly, taking up to the length of time in the record's previous TTL (time to live). At this point, you are free to decommission your source Google Workspace tenant.