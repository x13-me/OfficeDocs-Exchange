---
ms.localizationpriority: medium
ms.author: jhendr
manager: serdars
ms.topic: article
author: JoanneHendrickson
ms.service: exchange-online
ms.reviewer:
ms.collection:
- exchange-online
description: 'Summary: This article describes how to restore a public folder that was previously deleted in Exchange Online'
audience: ITPro
f1.keywords:
- NOCSH
title: Restore a deleted public folder in Exchange Online

---

# Restore a deleted public folder in Exchange Online

This article walks you through the steps to restore a deleted public folder in Exchange Online.

Public folders that have been deleted by users (using clients like Outlook) or admins (using administrative tools like PowerShell or the Exchange admin center) are normally stored in the public folder dumpster located in `\NON_IPM_SUBTREE\DUMPSTER_ROOT`. Deleted folders are preserved there until the retention period ends.

For the scenarios where [public folder contents are put on hold using retention policies](/microsoft-365/compliance/create-retention-policies), the folders that are removed from `\NON_IPM_SUBTREE\DUMPSTER_ROOT` are preserved under `\NON_IPM_SUBTREE\DiscoveryHolds` until the retention hold period ends.

You can restore folders that are preserved in the public folder dumpster or under the DiscoveryHolds folder using Exchange Online PowerShell. Restoring the public folder will restore all subfolders and items present in the folder.

In rare scenarios, you might also find folders under `\NON_IPM_SUBTREE\LOST_AND_FOUND`. [See this blog post](https://techcommunity.microsoft.com/t5/exchange-team-blog/introducing-public-folder-8220-lost-and-found-8221-functionality/ba-p/604043) for details on LOST_AND_FOUND and how to recover folders if you find them there.

> [!NOTE]
> The folders in the dumpster are permanently deleted after the retention period ends. After a public folder has been permanently deleted, you can't restore it, unless the folder is preserved under DiscoveryHolds by a retention policy.

## Permissions required

The user restoring the public folder must have the **Public Folders** role assigned to them. By default, this role is assigned to users present in the **Organization Management** role group.

## Restore a deleted public folder

1. [Connect to Exchange Online PowerShell](/powershell/exchange/connect-to-exchange-online-powershell).

1. Determine if the public folder you want to restore is in the public folder dumpster.

    The following command lists all non-system public folders in the dumpster:

    ```PowerShell
    Get-PublicFolder \NON_IPM_SUBTREE\DUMPSTER_ROOT -Recurse -ResultSize Unlimited | where {$_.FolderClass -ne "$null"}
    ```

    Alternatively, you can search for specific folders. For example, the following command searches for a deleted public folder named `Marketing`:

    ```PowerShell
    Get-PublicFolder \NON_IPM_SUBTREE\DUMPSTER_ROOT -Recurse -ResultSize Unlimited | where {$_.Name -like "Marketing"}
    ```

    Public folders under `\NON_IPM_SUBTREE\DiscoveryHolds` have a GUID appended to their name that you'll need to account for in your search.

    For example, the following command searches for a deleted public folder named `Sales`:

    ```PowerShell
    Get-PublicFolder \NON_IPM_SUBTREE\DiscoveryHolds -Recurse -ResultSize Unlimited | where {$_.Name -like "*Sales*"}
    ```

1. Use the following syntax to restore a public folder:

    ```PowerShell
    Set-PublicFolder -Identity "Full path of folder to be restored" -Path "Parent folder path where folder needs to be restored"
    ```

    For example, run the following command to restore a public folder named `PF1` to the root of the public folder tree:

    ```PowerShell
    Set-PublicFolder -Identity \NON_IPM_SUBTREE\DUMPSTER_ROOT\DUMPSTER_EXTEND\RESERVED_1\RESERVED_1\9f32c468-4bc2-42aa-b979-16a057394b2f\PF1 -Path \
    ```

    The following alternate example restores a public folder named `Sales` to the root of the public folder tree:

    ```PowerShell
    Set-PublicFolder -Identity \NON_IPM_SUBTREE\DiscoveryHolds\Sales_774d775c-da53-4ee7-869c-353c8a6e3265 -Path \
    ```

    If don't know the original path of the deleted folder, you can find the folder's original path before it was deleted.

    For example, the following commands reveal the original path of the deleted folder named `Marketing`:
    
    ```powershell    
    $folder = Get-PublicFolder \NON_IPM_SUBTREE\DUMPSTER_ROOT -Recurse -ResultSize Unlimited | where {$_.Name -like "Marketing"}; Get-PublicFolder (Get-PublicFolder $folder.ParentPath).DumpsterEntryId
    ```

### Restore a specific subfolder

Restoring a folder restores all of its subfolders, but you can also restore only one subfolder.

For example, the following commands restores `Subfolder1` under `\Parent1`:

```PowerShell
$pf = Get-PublicFolder \NON_IPM_SUBTREE\DUMPSTER_ROOT -Recurse | where {$_.Name -eq "Subfolder1"}; Set-PublicFolder $pf.identity -Path \Parent1
```

### Restore a public calendar folder

You can restore a public calendar folder using the same procedure as any other public folder, but there are special considerations.

When deleting a public calendar folder, a user sees the following options:

![Delete calendar dialog box.](../../media/delete-public-calendar-folder.png)

If the user selected "Yes", the items were deleted. In this case, you can restore the public folder, but the items cannot be recovered.

> [!NOTE]
> We don't recommend using Outlook to restore deleted public folders because Outlook truncates the public folder names. This issue is under investigation and this article will be updated when a fix is available.
