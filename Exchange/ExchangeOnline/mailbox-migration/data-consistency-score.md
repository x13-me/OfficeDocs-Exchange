---
localization_priority: Normal
description: 'Summary: Learn about the DCS migration'
ms.topic: overview
author: mattpennathe3rd
ms.author: v-mapenn
ms.assetid: 
ms.date: 11/22/2018
ms.reviewer: 
title: DCS Migration
ms.collection: exchange-server
audience: ITPro
ms.prod: exchange-server-it-pro
manager: serdars

---

# Migrating to the cloud

When migrating your Exchange environment to the cloud, there might be instances of data corruption in your environment that causes data loss during migration. To track and report on any instances of data loss, the migration process uses what is called the **DataConsistencyScore**. 

## The DataConsistencyScore

When you attempt a migration, any instances of corruption in your Exchange data store will count towards the **DataConsistencyScore**. This score is then used to determine whether an Exchange migration will complete successfully or if intervention is needed.

## Description of 4 categories (per migration or user level)

There are 4 possible grades that are derived from the **DataConsistencyScore**.

- **Perfect** There were on instances of data loss noted during migration. The migration will succeed.

- **Good** There was at least 1 instance of data corruption noted, but the corruption was not impactful. For example, if any metadata or folder permissions were lost during migration. The migration will succeed.

- **Investigate** A notable amount of data loss was detected, but only to a relatively minor extent. The migration requires approval in order to succeed.

- **Poor** Major data loss was detected. The migration will fail.

## How are my batches scored?

*There are notes about this in OneNote, but how much should be published to users?*

## Guidance or recommendations for migrations that fall under Investigate or Poor

If the migration receives a grade of **Investigate**, you can approve skipped items manually to allow the migration to succeed.

If you are using batches, then run:

```
Set-MigrationBatch -ApproveSkippedItems or Set-MigrationUser -ApproveSkippedItems
```

If you are using direct requests, then run:

```
Set-*Request -SkippedItemApprovalTime $([DateTime]::UtcNow)
```

If the migration has failed with a grade of **Poor**, it is possible to force the migration to succeed, but this is not recommended. Please contact Microsoft Support for assistance.

## How do I opt in or out of the feature

*There was discussion of overriding using BadItemLimit, but later discussion suggested this is not supported. What should go here?*