---
ms.localizationpriority: medium
ms.author: serdars
manager: serdars
ms.topic: article
author: msdmaguire
ms.prod: exchange-server-it-pro
ms.assetid: 1d800576-957d-4916-ae2a-55c08ca75be1
ms.reviewer:
ms.collection:
- Strat_EX_EXOBlocker
- exchange-server
description: 'Summary: How to move your Exchange Server public folders to Microsoft 365 Groups.'
f1.keywords:
- NOCSH
audience: ITPro
title: Use batch migration to migrate Exchange Server public folders to Microsoft 365 Groups

---

# Use batch migration to migrate Exchange Server public folders to Microsoft 365 Groups

Through a process known as *batch migration*, you can move some or all of your Exchange Server public folders to Microsoft 365 Groups. Groups is a new collaboration offering from Microsoft that offers certain advantages over public folders. For more information about the features and benefits of Groups, see [Migrate your public folders to Microsoft 365 Groups](migrate-to-microsoft-365-groups.md).

This article contains the step-by-step procedures for performing the actual batch migration of your Exchange Server public folders.

## What do you need to know before you begin?

Verify that you meet all of the following conditions as you prepare your migration:

- We recommend that you read this article in its entirety, as downtime is required for some steps.

- Public folders must be hosted on **Exchange 2016 CU4** or later servers.

- In Exchange Online, you need to be a member of the Organization Management role group. This role group is different from the permissions that are assigned to you when you subscribe to Microsoft 365, Office 365, or Exchange Online. For details about how to enable the Organization Management role group, see [Manage role groups](../../permissions/role-groups.md).

- In Exchange Server, you need to be a member of the Organization Management or Server Management role groups. For details, see [Add Members to a Role Group](/previous-versions/office/exchange-server-2010/dd638143(v=exchg.141)).

- We recommend that you move user mailboxes to Microsoft 365 or Office 365 for those users who need access to Microsoft 365 Groups. For more information, see [Ways to migrate multiple email accounts to Microsoft 365 or Office 365](../../../ExchangeOnline/mailbox-migration/mailbox-migration.md).

- MRS Proxy needs to be enabled on at least one Exchange server, and that server must also host public folder mailboxes. For details, see [Enable the MRS Proxy endpoint for remote moves](../../architecture/mailbox-servers/mrs-proxy-endpoint.md).

- You can't use the Exchange admin center (EAC) to do the procedures in this article. On Exchange server, you need to use the Exchange Management Shell. In Exchange Online, you need to use Exchange Online PowerShell. For more information, see [Connect to Exchange Online PowerShell](/powershell/exchange/connect-to-exchange-online-powershell).

- Currently, you can only Calendar public folders and Mail public folders to Microsoft 365 Groups. Migrating other types of public folders is not supported. Also, the target Groups need to exist in Microsoft 365 or Office 365 before the migration.

- The batch migration process only copies messages and calendar items from public folders to Microsoft 365 Groups. It doesn't copy other properties that are associated with public folder (for example, policies, rules, and permissions).

- Microsoft 365 Groups come with a 50 GB mailbox. Verify that public folder data to be migrated is less than 50 GB. Leave additional storage space for future content. The maximum size that we recommend for public folder migration is 25 GB.

- This migration is not an "all or nothing". You can pick and choose specific public folders to migrate. If the migrated public folder has sub-folders, those sub-folders are not automatically included in the migration. You need to explicitly include any sub-folders that you want to migrate. The migration allows you to map a maximum two sub-folders to a single Microsoft 365 Group mailbox.

- During the migration, existing public folders are not modified or otherwise affected by the migration. After you do the steps in the [Step 6: Lock the public folders (downtime required)](#step-6-lock-the-public-folders-downtime-required) section, users must use the target Microsoft 365 Groups instead of the original public folders that were migrated.

- You must use a single migration batch to migrate all of your public folder data. Exchange allows creating one migration batch at a time. If you attempt to create more than one migration batch simultaneously, you'll receive an error.

## Step 1: Get the scripts

The batch migration to Microsoft 365 groups requires running a number of scripts at different points in the migration, as described below in this article. Download the scripts and their supporting files [from this location](https://www.microsoft.com/download/details.aspx?id=55985). After all the scripts and files are downloaded, save them to the same location, such as `c:\PFtoGroups\Scripts`.

Before proceeding, verify you have downloaded and saved all of the following scripts and files:

> [!NOTE]
> Make sure to save all scripts and files to the same location.

- **AddMembersToGroups.ps1**: Adds members and owners to Microsoft 365 Groups based on permissions on the source public folders.

- **AddMembersToGroups.strings.psd1**: A support file used by the `AddMembersToGroups.ps1` script.

- **LockAndSavePublicFolderProperties.ps1**. Makes public folders read-only to prevent modifications during the migration. Transfers the mail-related public folder properties, and redirects mail sent to migrated mail-enabled public folders to the target Groups. Backs up the permission entries and the mail properties before modifying them.

- **LockAndSavePublicFolderProperties.strings.psd1**: A support file used by the `LockAndSavePublicFolderProperties.ps1` script.

- **UnlockAndRestorePublicFolderProperties.ps1**: Restores access rights and mail properties of the public folders using backup files that are created by `LockandSavePublicFolderProperties.ps1`.

- **UnlockAndRestorePublicFolderProperties.strings.psd1**: A support file used by the `UnlockAndRestorePublicFolderProperties.ps1` script.

- **WriteLog.ps1**: Enables the preceding three scripts to write logs.

- **RetryScriptBlock.ps1**. Enables the `AddMembersToGroups`, `LockAndSavePublicFolderProperties`, and `UnlockAndRestorePublicFolderProperties` scripts to retry certain actions in the event of transient errors.

For details about `AddMembersToGroups.ps1`, `LockAndSavePublicFolderProperties.ps1`, and `UnlockAndRestorePublicFolderProperties.ps1`, see [Migration scripts](#migration-scripts) later in this article.

## Step 2: Prepare for the migration

The following steps are necessary to prepare your organization for the migration:

1. Make a list of Mail and Calender public folders that you want to migrate to Microsoft 365 Groups.

2. Make a list of the target Microsoft 365 Groups for each migrated public folder. You can create new Groups or use existing Groups.

   If the permissions of the public folder is set to **Author** or above, the target Microsoft 365 Group should have the **Public** privacy setting. However, users will still need to join the Group to see the public group under the **Groups** node in Outlook.

   For more information, see [Learn about Microsoft 365 Groups](https://support.microsoft.com/office/b565caa1-5c40-40ef-9915-60fdb2d97fa2)

3. Rename any public folders that contain a backslash (**\\**) in their name. Otherwise, those public folders may not get migrated correctly.

4. The migration feature named **PAW** must be enabled for your Microsoft 365 or Office 365 organization. To verify that **PAW** is enabled, run the following command in Exchange Online PowerShell:

   ```PowerShell
   Get-MigrationConfig
   ```

   If the output of the **Features** property contains the value**PAW**, the feature is enabled and you can continue to [Step 3: Create the .csv file](#step-3-create-the-csv-file).

   Existing public folder migration batches or user migration batches in any state will prevent PAW from being enabled. Complete and remove any existing migration batches until no results are returned by the `Get-MigrationBatch` cmdlet. The removal of existing migrations aren't immediately reflected in the output of `Get-MigrationConfig` cmdlet.

   After you remove all existing batches, PAW should automatically enable itself.

   After you complete this step, you can create new user migration batches.

## Step 3: Create the .csv file

Create a .csv file, which will provide input for one of the migration scripts.

The .csv file needs the following columns:

- **FolderPath**: Path of the public folder to be migrated.
- **TargetGroupMailbox**: SMTP address of the target Microsoft 365 Group. You can run the following command to see the primary SMTP address.

  ```PowerShell
  Get-UnifiedGroup -Identity <alias of the group> | Format-Table PrimarySmtpAddress
  ```

An example .csv contains the following information:

```CSV
"FolderPath","TargetGroupMailbox"
"\Sales","sales@contoso.onmicrosoft.com"
"\Sales\APAC","apacsales@contoso.onmicrosoft.com"
"\Sales\EMEA","emeasales@contoso.onmicrosoft.com"
```

You can merge a Mail public folder and a Calendar public folder into the same Microsoft 365 Group. Otherwise, a single migration batch doesn't support any other scenarios for merging multiple public folders into the same Group. Run multiple migration batches one after another to map multiple public folders to the same Microsoft 365 Group. You can have up to 500 entries in each migration batch.

## Step 4: Start the migration request

In this step, you gather information from your Exchange environment, and then you use that information in Exchange Online PowerShell to create a migration batch. After that, you start the migration.

1. Find the MRS proxy server endpoint in Exchange 2016 or Exchange 2019. You'll need this information later when you run the migration request.

2. In Exchange Online PowerShell, use the information that was returned above in step 1 to run the following commands. The variables in these commands will be the values from step 1.

   1. Store the the credentials of an on-premises Exchange administrator in the variable named `$Source_Credential`.

      ```PowerShell
      $Source_Credential = Get-Credential
      ```

      Enter the username in the format: `<source_domain>\<Account>`.

   2. Use the MRS proxy server information from your Exchange Server environment as described in the previous step, and save that value to the variable named `$Source_RemoteServer`.

      ```PowerShell
      $Source_RemoteServer = "<MRS proxy endpoint>"
      ```

3. In Exchange Online PowerShell, run the following command to create a migration endpoint:

   ```PowerShell
   $PfEndpoint = New-MigrationEndpoint -PublicFolderToUnifiedGroup -Name PFToGroupEndpoint -RemoteServer $Source_RemoteServer -Credentials $Source_Credential
   ```

4. Run the following command to create a new public folder to Microsoft 365 Group migration batch:

   ```PowerShell
   New-MigrationBatch -Name PublicFolderToGroupMigration -CSVData ([System.IO.File]::ReadAllBytes('<path to .csv file>')) -PublicFolderToUnifiedGroup -SourceEndpoint  $PfEndpoint.Identity [-NotificationEmails <email addresses for migration notifications>] [-AutoStart]
   ```

   - **CSVData**: The .csv file previously created in [Step 3: Create the .csv file](#step-3-create-the-csv-file). Be sure to use the full path to this file. If you moved the filed, be sure to use the new location.
   - **NotificationEmails**: An optional parameter that sets the email addresses for notifications about the status and progress of the migration.
   - **AutoStart**: An optional switch that starts the migration batch as soon as you create it.
   - **PublicFolderToUnifiedGroup**: Indicates that this a public folder to Microsoft 365 Groups migration.

5. This step is required only if you didn't use the `AutoStart` switch in the previous command.

   Start the migration by running the following command in Exchange Online PowerShell:

   ```PowerShell
   Start-MigrationBatch PublicFolderToGroupMigration
   ```

Although you create the migration in Exchange Online PowerShell, you can view and manage the migration in the Exchange admin center (EAC) on the **Migration** page.

In Exchange Online PowerShell, you view the progress of the migration with the [Get-MigrationBatch](/powershell/module/exchange/get-migrationbatch) and [Get-MigrationUser](/powershell/module/exchange/get-migrationuser) cmdlets.

To view the **Migration** page in the EAC, do the following steps:

1. In the EAC at <https://admin.exchange.microsoft.com>, go the **Recipients** \> **Migration**.
2. Select the migration request.
3. In the **Details** pane, select **View Details**.

When the batch status is **Completed**, you can continue to [Step 5: Add members to Microsoft 365 groups from public folders](#step-5-add-members-to-microsoft-365-groups-from-public-folders).

## Step 5: Add members to Microsoft 365 groups from public folders

You can add members to the target Microsoft 365 Group. To add members to the group based on the public folder's permission entries, you need running the `AddMembersToGroups.ps1` script on the Exchange server as described in this section.

You need to synchronize user mailboxes to Exchange Online to add members to the Microsoft 365 group based on permission entries. To see which public folder permissions are eligible, see the [Migration scripts](#migration-scripts) section later in this article.

```PowerShell
.\AddMembersToGroups.ps1 -MappingCsv <path to .csv file> -BackupDir "<path to backup directory>" -ArePublicFoldersOnPremises $true -Credential (Get-Credential)
```

- **MappingCsv**: The .csv file that you created above in [Step 3: Create the .csv file](#step-3-create-the-csv-file). Be sure to provide the full path to this file. If you moved the file, be sure to use the new location.
- **BackupDir**: The folder where the migration log files are stored.
- **ArePublicFoldersOnPremises**: Indicates whether public folders are located in Exchange server or in Exchange Online.
- **Credential**: The Exchange Online username and password.

After you add users to a Microsoft 365 Group, they can use it.

## Step 6: Lock the public folders (downtime required)

After you've migrated the majority of public folder data to Microsoft 365 Groups, you can run the `LockAndSavePublicFolderProperties.ps1` script on the Exchange server. This step ensures that no new data is added to public folders before the migration has completed.

> [!NOTE]
> For mail-enabled pubic folders, the script copies some properties to the target Microsoft 365 Groups (for example, email addresses) and then mail-disables the mail-enabled public folders. After you run the script, mail that sent to those public folders is redirected to the target Microsoft 365 Groups. For details, see the [Migration scripts](#migration-scripts) section later in this article.

```PowerShell
.\LockAndSavePublicFolderProperties.ps1 -MappingCsv <path to .csv file> -BackupDir "<path to backup directory>" -ArePublicFoldersOnPremises $true -Credential (Get-Credential)
```

- **MappingCsv**: The .csv file that you created in [Step 3: Create the .csv file](#step-3-create-the-csv-file). Be sure to provide the full path to this file. If you moved the file, be sure to use the new location.
- **BackupDir**: The folder where the backup files for permission entries, mail-enabled public folder properties, and migration log files are stored. You can use these backup files if you need to roll back to public folders.
- **ArePublicFoldersOnPremises**: Indicate whether public folders are located in Exchange server or in Exchange Online.
- **Credential**: The Exchange Online username and password.

## Step 7: Finalize the public folder to Microsoft 365 Groups migration

After you've locked your public folders, you need to perform the migration again. This step is required for a final incremental copy of your data.

1. Before you run the migration again, you need to remove the existing batch migration by running the following command, which you can do by running the following command:

   ```PowerShell
   Remove-MigrationBatch -Identity "<name of migration batch>"
   ```

2. Create a new batch with the same .csv file by running the following commands:

   ```PowerShell
   New-MigrationBatch -Name PublicFolderToGroupMigration -CSVData ([System.IO.File]::ReadAllBytes('<path to .csv file>')) -PublicFolderToUnifiedGroup -SourceEndpoint $PfEndpoint.Identity [-NotificationEmails <email addresses for migration notifications>] [-AutoStart]
   ```

   ```PowerShell
   Start-MigrationBatch PublicFolderToGroupMigration
   ```

   - **CSVData**: The .csv file that you created in [Step 3: Create the .csv file](#step-3-create-the-csv-file). Be sure to provide the full path to this file. If you moved the file, be sure to use the new location.
   - **NotificationEmails**: An optional parameter that sets the email addresses for notifications about the status and progress of the migration.
   - **AutoStart**: An optional switch that starts the migration batch as soon as you create it.

After you finish this step, the status value of the migration batch is **Completed**. Verify that all data has been copied to Microsoft 365 Groups. At that point, if you're satisfied with the Microsoft 365 Groups experience, you can begin deleting the migrated public folders from your Exchange Server environment.

> [!IMPORTANT]
> While there are supported procedures for rolling back your migration and returning to public folders, roll-back isn't possible after you delete the source public folders. For more information, see the [How do I roll back to public folders from Microsoft 365 Groups?](#how-do-i-roll-back-to-public-folders-from-microsoft-365-groups) section in this article.

## Known issues

The following known issues can occur during a typical public folder to Microsoft 365 Groups migration:

- The script that transfers SMTP address from mail-enabled public folders to Microsoft 365 or Office 365 groups only adds the addresses as secondary email addresses in Exchange Online. Because of this, if you have Exchange Online Protection (EOP) or Centralized Mail Flow setup in your environment, will have issues sending email to the groups (to the secondary email addresses) post-migration.

- If the .csv mapping file has an entry with invalid public folder path, the migration batch displays as **Completed** without throwing an error, and no further data is copied.

## Migration scripts

For your reference, this section provides in-depth descriptions for three of the migration scripts and the tasks they execute in your Exchange environment. You can download all scripts and supporting files [from this location](https://www.microsoft.com/download/details.aspx?id=55985).

### AddMembersToGroups.ps1

This script will read the permissions of the public folders being migrated and then add members and owners to Microsoft 365 groups as follows:

- Users with the following permission roles will be added as members to a group in Microsoft 365 or Office 365. **Permission roles**: Owner, PublishingEditor, Editor, PublishingAuthor, Author

- In addition to the above, users with the following minimum access rights will also be added as members to a group in Microsoft 365 or Office 365. **Access rights**: ReadItems, CreateItems, FolderVisible, EditOwnedItems, DeleteOwnedItems

- Users with access right "Owner" will be added as owners to a group and users with other eligible access rights will be added as members.

- Security groups cannot be added as members of Microsoft 365 groups. Therefore they will be expanded, and then the individual users will be added as members or owners to the groups based on the access rights of the security group.

- When users in security groups that have access rights over a public folder have themselves explicit permissions over the same public folder, explicit permissions will be given preference. For example, consider a case in which a security group called "SG1" has members User1 and User2. Permission entries for the public folder "PF1" are as follows:

    SG1: Author in PF1

    User1: Owner in PF1

    In this case, User1 will be added as an owner to the Microsoft 365 group.

- When the default permission of a public folder being migrated is 'Author' or above, the script will suggest setting the corresponding group's privacy setting as 'Public'.

This script can be run even after the lock-down of public folders, with parameter the `ArePublicFoldersLocked` set to ` $true `. In this scenario, the script will read permissions from the back up file created during lock-down.

### LockAndSavePublicFolderProperties.ps1

This script makes the public folders being migrated read-only. When mail-enabled public folders are migrated, they will first be mail-disabled and their SMTP addresses will be added to the respective Microsoft 365 groups. Then the permission entries will be modified to make them read-only. A back up of the mail properties of mail-enabled public folders, as well as the permission entries of all the public folders, will be copied, before performing any modification on them.

 If there are multiple migration batches, a separate backup directory should be used with each mapping .csv file.

The following mail properties will be stored, along with respective mail-enabled public folders and Microsoft 365 groups:

- PrimarySMTPAddress

- EmailAddresses

- ExternalEmailAddress

- EmailAddressPolicyEnabled

- GrantSendOnBehalfTo

- SendAs Trustee list

The above mail properties will be stored in a .csv file, which can be used in the roll back process (if you want to return to using public folders, see [How do I roll back to public folders from Microsoft 365 Groups?](#how-do-i-roll-back-to-public-folders-from-microsoft-365-groups) for more information). A snapshot of the mail-enabled public folders' properties will also be stored in a file called PfMailProperties.csv. This file is not necessary for the roll back process, but can still be used for your reference.

The following mail properties will be migrated to target groups as part of lock down:

- PrimarySMTPAddress

- EmailAddresses

- SendAs Trustee list

- GrantSendOnBehalfTo

The script ensures that the PrimarySMTPAddress and EmailAddresses of migrating mail-enabled public folders will be added as secondary SMTP addresses of the corresponding Microsoft 365 groups. Also, SendAs and SendOnBehalfTo permissions of users on mail-enabled public folders will be given equivalent permission in the corresponding target groups.

### Access rights allowed

Only the following access rights will be allowed for users to ensure that the public folders are made read-only for all users. These are stored in **ListOfAccessRightsAllowed**:

- ReadItems

- CreateSubfolders

- FolderContact

- FolderVisible

The permission entries will be modified as follows:

|**Before lock down**|**After lock down**|
|:-----|:-----|
|None|None|
|AvailabilityOnly|AvailabilityOnly|
|LimitedDetails|LimitedDetails|
|Contributor|FolderVisible|
|Reviewer|ReadItems, FolderVisible|
|NonEditingAuthor|ReadItems, FolderVisible|
|Aughor|ReadItems, FolderVisible|
|Editor|ReadItems, FolderVisible|
|PublishingAuthor|ReadItems, CreateSubfolders, FolderVisible|
|PublishingEditor|ReadItems, CreateSubfolders, FolderVisible|
|Owner|ReadItems, CreateSubfolders, FolderContact, FolderVisible|

- Access rights for users without read permissions will be left untouched, and they will continue to be blocked from read rights.

- For users with custom roles, all the access rights that are not in **ListOfAccessRightsAllowed** will be removed. In the event that the users don't have any access rights from the allowed list after filtering, these users' access right will be set to 'None'.

There might be an interruption in sending emails to mail-enabled public folders during the time between when the folders are mail-disabled and their SMTP addresses are added to Microsoft 365 Groups.

### UnlockAndRestorePublicFolderProperties.ps1

This script will re-assign permissions back to public folders, based on the back up file taken during public folder lock-down. This script will also mail-enable public folders that had been mail-disabled, after it removes the folders' SMTP addresses from their respective Microsoft 365 groups. There might be slight downtime during this process.

## How do I roll back to public folders from Microsoft 365 Groups?
<a name="rollback"> </a>

In the event that you change your mind and want to return to using public folders after using Microsoft 365 Groups, the command listed below will restore your environment to the state it was pre-migration. A roll back can be performed as long as the backup files exist and as long as you didn't delete the public folders post-migration.

On your Exchange 2016 or Exchange 2019 server, run the following command. In this command:

- **BackupDir** is the directory where the backup files for permission entries, MEPF properties, and migration log files will be stored. Make sure you use the same location you specified in *Step 6: Lock down the public folders to cut-over (public folder downtime required)*.

- **ArePublicFoldersOnPremises** is a parameter to indicate whether public folders are located on-premises or in Exchange Online.

- **Credential** is the Exchange Online username and password.

```PowerShell
.\UnlockAndRestorePublicFolderProperties.ps1 -BackupDir <path to backup directory> -ArePublicFoldersOnPremises $true -Credential (Get-Credential)
```

Be aware that any items added to the Microsoft 365 group, or any edit operations performed in the groups, are not copied back to your public folders. Therefore there will be data loss, assuming new data was added while the public folder was a group.

Note also that it's not possible to restore a subset of public folders, which means all of the public folders there were migrated should be restored.

The corresponding Microsoft 365 groups won't be deleted as part of the roll back process. You must clean or delete those groups manually.
