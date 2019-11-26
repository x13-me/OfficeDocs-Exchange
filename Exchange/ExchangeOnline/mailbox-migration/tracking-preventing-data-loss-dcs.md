---
localization_priority: Normal
description: 'Summary: Tracking and preventing migration data loss with DataConsistencyScore'
ms.topic: overview
author: mattpennathe3rd
ms.author: v-mapenn
ms.assetid: 
ms.date: 11/22/2019
ms.reviewer: 
title: Tracking and Preventing Migration Data Loss
ms.collection: exchange-server
audience: ITPro
ms.prod: exchange-server-it-pro
manager: serdars

---

# Tracking and Preventing migration data loss

When migrating your Exchange environment to the cloud, there might be instances of data corruption in your environment that causes data loss during migration. The migration process tracks and reports on any instances of data loss by generating a **DataConsistencyScore**.

## Migration and DataConsistencyScore

When you attempt a migration, any instances of corruption in your Exchange data store will count towards the **DataConsistencyScore**. This score is then used to determine whether an Exchange migration will complete successfully or if intervention is needed.

There are 4 possible grades that are derived from the **DataConsistencyScore**.

|Grade|Description|
|---|---|
|**Perfect**| No instances of data loss noted during migration. The migration will succeed.|
|**Good**| At least 1 instance of data loss noted, but the loss was not impactful. For example, if only metadata or folder permissions were lost during migration. The migration will succeed.|
|**Investigate**|Significant, but relatively minor data loss was detected. The migration requires approval in order to succeed.|
|**Poor**|Major data loss was detected. The migration cannot complete unless you contact Microsoft Support for assistance.|

## How the DataConsistencyScore is calculated

There are various thresholds used to determine the DataConsistencyScore. Microsoft is constantly tuning these thresholds to insure that problematic data loss does not occur during migrations. The details of these thresholds are not presented to Exchange administrators so that they are not bothered with unnecessary information.

For batches, the DataConsistencyScore is equal to the worst DataConsistencyScore of any user within that batch. This behavior helps administrators know immediately whether there is any data loss that should be investigated.

## Guidance for grades of Investigate or Poor

If the migration receives a grade of **Investigate**, you can approve skipped items manually to allow the migration to succeed.

If you are using batches, then run:

```
Set-MigrationBatch -ApproveSkippedItems or Set-MigrationUser -ApproveSkippedItems
```

If you are using MoveRequests directly, then run:

```
Set-MoveRequest -SkippedItemApprovalTime $([DateTime]::UtcNow)
```

If the migration has failed with a grade of **Poor**, it is possible to force the migration to succeed, but this is not recommended. Please contact Microsoft Support for assistance.

## How to opt in or opt out of using DataConsistencyScore

As of late 2019, the [BadItemLimit parameter](https://docs.microsoft.com/powershell/module/exchange/move-and-migration/new-moverequest) is still available as an option. You can specify a value for the BadItemLimit parameter when using cmdlets or you can fill in the BadItemLimit box in the EAC UI. When you specify a BadItemLimit, the old migration method is used and the DataConsistencyScore is not calculated.

If the BadItemLimit parameter is not specified or if the box in the Exchange Admin Center wizard is left blank, then the new migration method and DataConsistencyScore are used.

> NOTE:
> The BadItemLimit parameter is deprecated and will be removed at a future date.