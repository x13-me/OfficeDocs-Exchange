---
title: "Clean up or delete items from the Recoverable Items folder in Exchange Online"
ms.author: markjjo
author: markjjo
manager: laurawi
ms.date: 
ms.audience: ITPro
ms.topic: article
ms.prod: exchange-server-it-pro
localization_priority: Normal
ms.assetid: 82c310f8-de2f-46f2-8e1a-edb6055d6e69
description: "Summary: Admins can learn how to clean up or delete items from the Recoverable Items folder in Exchange Online."
---

# Clean up or delete items from the Recoverable Items folder in Exchange Online

The Recoverable Items folder (known in earlier versions of Exchange as *the dumpster*) exists to protect from accidental or malicious deletions and to facilitate discovery efforts commonly undertaken before or during litigation or investigations.

How you clean up a user's Recoverable Items folder depends on whether the mailbox is placed on In-Place Hold or Litigation Hold, or had single item recovery enabled:

- If a mailbox isn't placed on In-Place Hold or Litigation Hold or doesn't have single item recovery enabled, you can simply delete items from the Recoverable Items folder. After items are deleted, you can't use single item recovery to recover them.

- If the mailbox is placed on In-Place Hold or Litigation Hold or has single item recovery enabled, you'll want to preserve the mailbox data until the hold is removed or single item recovery is disabled. In this case, you need to perform more detailed steps to clean up the Recoverable Items folder.

To learn more about In-Place Hold and Litigation Hold, see [In-Place Hold and Litigation Hold in Exchange Online](../in-place-and-litigation-holds.md). To learn more about single item recovery, see [Single item recovery](recoverable-items-folder.md#single-item-recovery).

## What do you need to know before you begin?

- By default, the Mailbox Import Export role isn't assigned to any role groups in Exchange Online. To use any cmdlets that require the Mailbox Import Export role, you need to add the role to a role group. For more information, see [Manage role groups in Exchange Online](../../permissions-exo/role-groups.md)|

- Because incorrectly cleaning up the Recoverable Items folder can result in data loss, it's important that you're familiar with the Recoverable Items folder and the impact of removing its contents. Before performing this procedure, we recommend that you review the information in [Recoverable Items folder in Exchange Online](recoverable-items-folder.md).

- You can only use Exchange Online PowerShell to perform the procedures in this topic. To connect to Exchange Online PowerShell, see [Connect to Exchange Online PowerShell](https://docs.microsoft.com/powershell/exchange/exchange-online/connect-to-exchange-online-powershell/connect-to-exchange-online-powershell).

> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at: [Exchange Online](https://go.microsoft.com/fwlink/p/?linkId=267542) or [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkId=285351).

## Use Exchange Online PowerShell to delete items from the Recoverable Items folder for mailboxes that aren't placed on hold or don't have single item recovery enabled

This example permanently deletes items from the user Gurinder Singh's Recoverable Items folder and also copies the items to the GurinderSingh-RecoverableItems folder in the Discovery Search Mailbox (a discovery mailbox created by Exchange Setup).

```
Search-Mailbox -Identity "Gurinder Singh" -SearchDumpsterOnly -TargetMailbox "Discovery Search Mailbox" -TargetFolder "GurinderSingh-RecoverableItems" -DeleteContent
```

> [!NOTE]
> To delete items from the mailbox without copying them to another mailbox, use the preceding command without the _TargetMailbox_ and _TargetFolder_ parameters.

For detailed syntax and parameter information, see [Search-Mailbox](http://technet.microsoft.com/library/9ee3b02c-d343-4816-a583-a90b1fad4b26.aspx).

## Use Exchange Online PowerShell to clean up the Recoverable Items folder for mailboxes that are placed on hold or have single item recovery enabled

- If a mailbox reaches its Recoverable Items quota, we recommend that you raise the quota and not delete items from the folder.

- We recommend that you first copy data from the user's Recoverable Items folder to another mailbox before you delete messages. If you're deleting items due to storage constraints on one volume, you can copy items to a mailbox located on a volume that has adequate storage.

This procedure copies items from Gurinder Singh's Recoverable Items folder to the GurinderSingh-RecoverableItems folder in the Discovery Search Mailbox. Before you copy and delete items from the Recoverable Items folder, you should first perform several steps to make sure items aren't deleted from the Recoverable Items folder. After you copy items to a discovery or backup mailbox and clean up the folder, you can revert to the mailbox's previous settings.

1. Retrieve the following quota settings. Be sure to note the values so you can revert to these settings after cleaning up the Recoverable Items folder:

   - _RecoverableItemsQuota_

   - _RecoverableItemsWarningQuota_

   - _ProhibitSendQuota_

   - _ProhibitSendReceiveQuota_

   - _UseDatabaseQuotaDefaults_

   - _RetainDeletedItemsFor_

   - _UseDatabaseRetentionDefaults_

     > [!NOTE]
     > If the _UseDatabaseQuotaDefaults_ parameter is set to `$true`, the previous quota settings aren't applied. The corresponding quota settings configured on the mailbox database are applied, even if individual mailbox settings are populated.

   ```
   Get-Mailbox "Gurinder Singh" | Format-List RecoverableItemsQuota,RecoverableItemsWarningQuota,ProhibitSendQuota,ProhibitSendReceiveQuota,UseDatabaseQuotaDefaults,RetainDeletedItemsFor,UseDatabaseRetentionDefaults
   ```

2. Retrieve the mailbox access settings for the mailbox. Be sure to note these settings for later.

   ```
   Get-CASMailbox "Gurinder Singh" | Format-List EwsEnabled,ActiveSyncEnabled,MAPIEnabled,OWAEnabled,ImapEnabled,PopEnabled
   ```

3. Retrieve the current size of the Recoverable Items folder. Note the size so you can raise the quotas in Step 5.

   ```
   Get-MailboxFolderStatistics "Gurinder Singh" -FolderScope RecoverableItems | Format-List Name,FolderAndSubfolderSize
   ```

4. Disable client access to the mailbox to make sure no changes can be made to mailbox data for the duration of this procedure.

   ```
   Set-CASMailbox "Gurinder Singh" -EwsEnabled $false -ActiveSyncEnabled $false -MAPIEnabled $false -OWAEnabled $false -ImapEnabled $false -PopEnabled $false
   ```

5. To make sure no items are deleted from the Recoverable Items folder, increase the Recoverable Items quota, increase the Recoverable Items warning quota, and set the deleted item retention period to a value higher than the current size of the user's Recoverable Items folder. This is particularly important for preserving messages for mailboxes placed on In-Place Hold or Litigation Hold. We recommend raising these settings to twice their current size.

   ```
   Set-Mailbox "Gurinder Singh" -RecoverableItemsQuota 50Gb -RecoverableItemsWarningQuota 50Gb -RetainDeletedItemsFor 3650 -ProhibitSendQuota 50Gb -ProhibitSendRecieveQuota 50Gb -UseDatabaseQuotaDefaults $false -UseDatabaseRetentionDefaults $false
   ```

6. Disable single item recovery and remove the mailbox from Litigation Hold.

   ```
    Set-Mailbox "Gurinder Singh" -SingleItemRecoveryEnabled $false -LitigationHoldEnabled $false
  ```

    > [!IMPORTANT]
    > After you run this command, it may take up to one hour to disable single item recovery or Litigation Hold. We recommend that you perform the next step only after this period has elapsed.

7. Copy items from the Recoverable Items folder to a folder in the Discovery Search Mailbox and delete the contents from the source mailbox.

   ```
   Search-Mailbox -Identity "Gurinder Singh" -SearchDumpsterOnly -TargetMailbox "Discovery Search Mailbox" -TargetFolder "GurinderSingh-RecoverableItems" -DeleteContent
   ```

    If you need to delete only messages that match specified conditions, use the _SearchQuery_ parameter to specify the conditions. This example deletes messages that have the string "Your bank statement" in the **Subject** field.

   ```
   Search-Mailbox -Identity "Gurinder Singh" -SearchQuery "Subject:'Your bank statement'" -SearchDumpsterOnly -TargetMailbox "Discovery Search Mailbox" -TargetFolder "GurinderSingh-RecoverableItems" -DeleteContent
   ```

    > [!NOTE]
    > It isn't required to copy items to the Discovery Search Mailbox. You can copy messages to any mailbox. However, to prevent access to potentially sensitive mailbox data, we recommend copying messages to a mailbox that has access restricted to authorized records managers. By default, access to the default Discovery Search Mailbox is restricted to members of the Discovery Management role group. For details, see[In-Place eDiscovery in Exchange Online](../in-place-ediscovery/in-place-ediscovery.md).

8. If the mailbox was placed on Litigation Hold or had single item recovery enabled earlier, enable these features again.

   ```
   Set-Mailbox "Gurinder Singh" -SingleItemRecoveryEnabled $true -LitigationHoldEnabled $true
   ```

    > [!IMPORTANT]
    > After you run this command, it may take up to one hour to enable single item recovery or Litigation Hold. We recommend that you enable the Managed Folder Assistant and allow client access (Step 9) only after this period has elapsed.

9. Revert the following quotas to the values noted in Step 1:

   - _RecoverableItemsQuota_

   - _RecoverableItemsWarningQuota_

   - _ProhibitSendQuota_

   - _ProhibitSendReceiveQuota_

   - _UseDatabaseQuotaDefaults_

   - _RetainDeletedItemsFor_

   - _UseDatabaseRetentionDefaults_

    In this example, the mailbox is removed from retention hold, the deleted item retention period is reset to the default value of 14 days, and the Recoverable Items quota is configured to use the same value as the mailbox database. If the values you noted in Step 1 are different, you must use the preceding parameters to specify each value and set the _UseDatabaseQuotaDefaults_ parameter to `$false`. If the _RetainDeletedItemsFor_ _and UseDatabaseRetentionDefaults_ parameters were previously set to a different value, you must also revert them to the values noted in Step 1.

   ```
   Set-Mailbox "Gurinder Singh" -RetentionHoldEnabled $false -RetainDeletedItemsFor 14 -RecoverableItemsQuota unlimited -UseDatabaseQuotaDefaults $true
   ```

10. Enable client access.

   ```
    Set-CASMailbox -ActiveSyncEnabled $true -EwsEnabled $true -MAPIEnabled $true -OWAEnabled $true -ImapEnabled $true -PopEnabled $true
  ```

For detailed syntax and parameter information, see the following topics:

- [Get-Mailbox](http://technet.microsoft.com/library/8a5a6eb9-4a75-47f9-ae3b-a3ba251cf9a8.aspx)

- [Get-CASMailbox](http://technet.microsoft.com/library/d80a5990-9106-4eb8-bba8-b3975805c325.aspx)

- [Get-MailboxFolderStatistics](http://technet.microsoft.com/library/212ca564-435e-4af6-8673-5564732bf118.aspx)

- [Set-CASMailbox](http://technet.microsoft.com/library/ff7d4dc5-755e-4005-a0a3-631eed3f9b3b.aspx)

- [Set-Mailbox](http://technet.microsoft.com/library/a0d413b9-d949-4df6-ba96-ac0906dedae2.aspx)

- [Search-Mailbox](http://technet.microsoft.com/library/9ee3b02c-d343-4816-a583-a90b1fad4b26.aspx)

## How do you know this worked?

To verify that you've successfully cleaned up the Recoverable Items folder of a mailbox, use [Get-MailboxFolderStatistics](http://technet.microsoft.com/library/212ca564-435e-4af6-8673-5564732bf118.aspx) cmdlet the check the size of the Recoverable Items folder.

This example retrieves the size of the Recoverable Items folder and its subfolders and an item count in the folder and each subfolder.

```
Get-MailboxFolderStatistics -Identity "Gurinder Singh" -FolderScope RecoverableItems | Format-Table Name,FolderAndSubfolderSize,ItemsInFolderAndSubfolders -Auto
```
