---
title: "Perform a Google Workspace migration"
ms.author: jhendr
author: msdmaguire
manager: serdars
audience: Admin
ms.topic: conceptual
ms.service: exchange-online
localization_priority: Normal
search.appverid: MET150
f1.keywords:
- NOCSH
description: Instructions for migrating from Google Workspace to Microsoft 365 or Office 365 in stages by migrating users in batches.
ms.custom: seo-marvel-apr2020
---

# Perform a Google Workspace (formerly G Suite) migration

You can migrate the following functionalities from Google Workspace to Microsoft 365 or Office 365:
- Mail
- Calendar
- Contacts

You can migrate batches of users from Google Workspace to Microsoft 365 or Office 365, allowing a migration project to be done in stages. This migration requires that you provision all of your users who will be migrated as mail-enabled users outside of the migration process. You must specify a list of users to migrate for each batch.

All of the procedures in this article assume that your Microsoft 365 or Office 365 domain has already been verified and your TXT records have been set up. For more information, see [Set up your domain (host-specific instructions)](/microsoft-365/admin/get-help-with-domains/set-up-your-domain-host-specific-instructions).

   > [!NOTE]
   > Google Workspace migration is not currently available for Office 365 US Government GCC High or DoD.

## Migration modalities

You can migrate from Google Workspace using the following modalities:
- [Automated - through the New Exchange Admin Center](automated-migration-neweac.md)
- [Manual - through the New Exchange Admin Center as well as Classic Exchange Admin Center](manual-gspace-migration-overview.md)
- [PowerShell](perform-gspace-migration-powershell.md)

## Migration limitations

> [!NOTE]
> The largest single email message that can be migrated is based on the transport configuration for your configuration. The default limit is 35 MB. To increase this limit, see [Office 365 now supports larger email messages](https://www.microsoft.com/en-us/microsoft-365/blog/2015/04/15/office-365-now-supports-larger-email-messages-up-to-150-mb/).

Throughput limitations for contacts and calendars completely depend on the quota restrictions for your tenant's service account on the Google Workspace side.

Other migration limitations are described in the following table:

<br>

****

|Data type|Limitations|
|---|---|
|Mail|Vacation settings, Automatic reply settings|
|Meeting rooms|Room bookings will not be migrated|
|Calendar|Shared calendars, cloud attachments, Google Hangout links, and event colors will not be migrated|
|Contacts|A maximum of three email addresses per contact are migrated over|
|Contacts|Gmail tags, contact URLs, and custom tags will not be migrated|
|

> [!TIP]
> If you will be [starting your migration batch with Exchange Online Powershell](perform-gspace-migration-powershell.md), as described later in this article, you can use the `-ExcludeFolder` parameter to prevent certain folders from being migrated. This will reduce the amount of data in your migration, as well as the size of a user's new Exchange Online mailbox. You can identify folders you don't want to migrate by name, and you can also identify Gmail labels that apply to multiple messages in order to exclude those messages from the migration. For more information on using `-ExcludeFolder`, see [New-MigrationBatch](/powershell/module/exchange/new-migrationbatch).
