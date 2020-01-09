---
localization_priority: Normal
ms.author: v-mapenn
manager: serdars
ms.topic: article
author: mattpennathe3rd
ms.service: exchange-online
ms.reviewer: 
ms.collection: 
- exchange-online
description: 'Summary: This article describes how to restore a public folder that was previously deleted in Exchange Online'
audience: ITPro
title: Restore a deleted public folder

---

# Restore a deleted public folder

 **Summary**: This article describes how to restore a public folder in Exchange Online that was previously deleted.

The public folders deleted by users or administrators are stored in the public folder dumpster located in `\NON_IPM_SUBTREE\DUMPSTER_ROOT`. The folders are preserved here until the time retention period is over. Any folders preserved in the public folder dumpster can be restored using EXO PowerShell. Restoring the public folder will restore all the sub-folders and items present in the folder.

> [!NOTE]
> The folders in the dumpster are permanently deleted after the retention period is over. Such folders cannot be restored.

## What do you need to know before you begin?

The user restoring the public folder must have the “Public Folders” role assigned. This role is assigned by default to users present in the “Organization Management” role group.

## Restore a deleted public folder

1. Connect to EXO PowerShell for Exchange Online.

1. List the public folders present in the public folder dumpster.

    The following command lists all non-system public folders in the dumpster:

    ```PowerShell
    Get-PublicFolder \NON_IPM_SUBTREE\DUMPSTER_ROOT -Recurse |?{$_.FolderClass -ne "$null"}
    ```

    You can also search for specific folders. For example, the following command searches for a deleted public folder that was named Marketing.

    ```PowerShell
    Get-PublicFolder \NON_IPM_SUBTREE\DUMPSTER_ROOT -Recurse |?{$_.Name -like "Marketing"}
    ```

1. Use the following command to restore the desired public folder:

    ```PowerShell
    Set-PublicFolder -Identity “Full path of folder to be restored” -Path “Parent folder path where folder needs to be restored”
    ```

    Example 1:

    To restore a public folder named `PF1`, located under the root of the public folder tree:

    ```PowerShell
    Set-PublicFolder -Identity \NON_IPM_SUBTREE\DUMPSTER_ROOT\DUMPSTER_EXTEND\RESERVED_1\RESERVED_1\9f32c468-4bc2-42aa-b979-16a057394b2f\PF1 -Path \
    ```

### Restore a secific subfolder

Deleting a folder also deletes all of its subfolders. Likewise, restoring a folder also restores all of its subfolders.

Example 2:

You can restore a specific subfolder. The following command restores `Subfolder1` under `\Parent1`:

```PowerShell
$pf=Get-PublicFolder \NON_IPM_SUBTREE\DUMPSTER_ROOT -Recurse |?{$_.Name -eq "Subfolder1"};Set-PublicFolder $pf.identity -Path \Parent1
```

### Restore a public calendar folder

When deleting a public calendar folder, a user sees the following options:

![Delete calendar dialog box](..\..\media\delete-public-calendar-folder.png)

If the user selected “Yes”, the items were deleted. In this case, if you restore the folder, the public folder will be restored, but the items cannot be recovered.

> [!NOTE]
> Using Outlook to restore deleted public folders is not recommended because it truncates the public folder name and retains only the first name of the public folder. This issue is under investigation and this article will be updated when there is a fix available.