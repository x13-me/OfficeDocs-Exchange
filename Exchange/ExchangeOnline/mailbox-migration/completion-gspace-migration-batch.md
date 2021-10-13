---
title: Completion of migration batch in Exchange Online
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
description: Overview to completion of migration batch
ms.custom: seo-marvel-jun2021
---

# Completion of migration batch in Exchange Online

Based on whether you are using New EAC, Classic EAC, or PowerShell cmdlets to perform the migration, the completion process differs.

## Finalizing your migration

After you have successfully migrated all of your Google Workspace users to Microsoft 365 or Office 365, you can switch your primary MX record to point to Microsoft 365 or Office 365. The update to the MX record will propagate slowly, taking up to the length of time in the record's previous TTL (time to live). At this point, you are free to decommission your source Google Workspace tenant.
