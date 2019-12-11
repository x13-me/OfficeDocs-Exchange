---
localization_priority: Normal
description: 'Summary: Learn about permissions that are required to perform tasks to configure various components of Exchange Server 2016 or Exchange Server 2019.'
ms.topic: reference
author: mattpennathe3rd
ms.author: v-mapenn
ms.assetid: 3646a4e8-36b2-41fb-89a4-79b0963fcb11
ms.date: 7/5/2018
ms.reviewer:
title: Exchange infrastructure and PowerShell permissions
ms.collection: exchange-server
audience: ITPro
ms.prod: exchange-server-it-pro
manager: serdars

---

# Exchange infrastructure and PowerShell permissions

The permissions required to perform tasks to configure various components of Exchange Server depend on the procedure being performed or the cmdlet you want to run. See each of the sections in this topic for more information about their respective features.

To find out what permissions you need to perform the procedure or run the cmdlet, do the following:

1. In the table below, find the feature that is most related to the procedure you want to perform or the cmdlet you want to run.

2. Next, look at the permissions required for the feature. You must be assigned one of those role groups, an equivalent custom role group, or an equivalent management role. You can also click on a role group to see its management roles. If a feature lists more than one role group, you only need to be assigned one of the role groups to use the feature. For more information about role groups and management roles, see [Understanding Role Based Access Control](https://technet.microsoft.com/library/dd298183.aspx).

3. Now, run the **Get-ManagementRoleAssignment** cmdlet to look at the role groups or management roles assigned to you to see if you have the permissions that are necessary to manage the feature.

    > [!NOTE]
    > You must be assigned the Role Management management role to run the **Get-ManagementRoleAssignment** cmdlet. If you don't have permissions to run the **Get-ManagementRoleAssignment** cmdlet, ask your Exchange administrator to retrieve the role groups or management roles assigned to you.

If you want to delegate the ability to manage a feature to another user, see [Delegate role assignments](https://docs.microsoft.com/exchange/delegate-role-assignments-exchange-2013-help).

> [!NOTE]
> Some features may require that you have local administrator permissions on the server you want to manage. To manage these features, you must be a member of the Local Administrators group on that server.

## Exchange infrastructure permissions

The following table lists the permissions required to perform tasks that configure general Exchange settings.

Users who are assigned the View-Only Management role group can view the configuration of the features in the following table. For more information, see [View-only Organization Management](https://technet.microsoft.com/library/dd351130.aspx).

|**Feature**|**Permissions required**|
|:-----|:-----|
|Administrator audit logging|[Organization Management](https://docs.microsoft.com/exchange/organization-management-exchange-2013-help) <br/> [Records Management](https://technet.microsoft.com/library/0e0c95ce-6109-4591-b86d-c6cfd44d21f5.aspx)|
|Exchange admin center configuration settings|[View-Only Organization Management](https://technet.microsoft.com/library/c514c6d0-0157-4c52-9ec6-441d9a30f3df.aspx)|
|Exchange admin center connectivity|[Organization Management](https://docs.microsoft.com/exchange/organization-management-exchange-2013-help) <br/> [Server Management](https://technet.microsoft.com/library/30cbc4de-adb3-42e8-922f-7661095bdb8c.aspx)|
|Exchange server configuration settings|[Organization Management](https://docs.microsoft.com/exchange/organization-management-exchange-2013-help) <br/> [Server Management](https://technet.microsoft.com/library/30cbc4de-adb3-42e8-922f-7661095bdb8c.aspx)|
|Exchange Help settings|[Organization Management](https://docs.microsoft.com/exchange/organization-management-exchange-2013-help)|
|Message categories|[Organization Management](https://docs.microsoft.com/exchange/organization-management-exchange-2013-help) <br/> [Hygiene Management](https://docs.microsoft.com/exchange/hygiene-management-exchange-2013-help) <br/> [Recipient Management](https://technet.microsoft.com/library/669d602e-68e3-41f9-a455-b942d212d130.aspx) <br/> [Help Desk](https://docs.microsoft.com/exchange/help-desk-exchange-2013-help)|
|Product key|[Organization Management](https://docs.microsoft.com/exchange/organization-management-exchange-2013-help)|
|Test system health|[Organization Management](https://docs.microsoft.com/exchange/organization-management-exchange-2013-help) <br/> [Server Management](https://technet.microsoft.com/library/30cbc4de-adb3-42e8-922f-7661095bdb8c.aspx)|
|View-only administrator audit logging|[Organization Management](https://docs.microsoft.com/exchange/organization-management-exchange-2013-help) <br/> [Records Management](https://technet.microsoft.com/library/0e0c95ce-6109-4591-b86d-c6cfd44d21f5.aspx) <br/> **Note**: You can also manually assign the View-Only Audit Logs management role to a management role group. For more information, see [View-Only Audit Logs](https://technet.microsoft.com/library/9298fe59-0a16-4a09-bdb8-514d1cea6e2f.aspx).|
|Write to audit log|Users that are members of any role group or assigned any management role can write to the administrator audit log.|

## Exchange PowerShell infrastructure permissions

The following table lists the permissions required to perform tasks that configure features that control how the Exchange Management Shell runs.

Users who are assigned the View-Only Management role group can view the configuration of the features in the following table. For more information, see [View-only Organization Management](https://technet.microsoft.com/library/dd351130.aspx).

|**Feature**|**Permissions required**|
|:-----|:-----|
|Active Directory Domain Services server settings|[Organization Management](https://docs.microsoft.com/exchange/organization-management-exchange-2013-help) <br/> [Server Management](https://technet.microsoft.com/library/30cbc4de-adb3-42e8-922f-7661095bdb8c.aspx) <br/> [Recipient Management](https://technet.microsoft.com/library/669d602e-68e3-41f9-a455-b942d212d130.aspx) <br/> [UM Management](https://technet.microsoft.com/library/c91f0387-615c-4a1d-87d4-133ddac1e407.aspx)|
|Cmdlet extension agents|[Organization Management](https://docs.microsoft.com/exchange/organization-management-exchange-2013-help)|
|PowerShell virtual directories|[Organization Management](https://docs.microsoft.com/exchange/organization-management-exchange-2013-help) <br/> [Server Management](https://technet.microsoft.com/library/30cbc4de-adb3-42e8-922f-7661095bdb8c.aspx)|
|PowerShell and WinRM installation|Local Server Administrator|
|Remote PowerShell|[Organization Management](https://docs.microsoft.com/exchange/organization-management-exchange-2013-help)|

## Federation and certificates permissions

The following table lists permissions required for performing tasks related to federation trusts, OAuth configuration, certificate management, and hybrid deployment configuration.

Users who are assigned the View-Only Management role group can view the configuration of the features in the following table. For more information, see [View-only Organization Management](https://technet.microsoft.com/library/dd351130.aspx).

|**Feature**|**Permissions required**|
|:-----|:-----|
|Certificate management|[Organization Management](https://docs.microsoft.com/exchange/organization-management-exchange-2013-help) <br/> [Server Management](https://technet.microsoft.com/library/30cbc4de-adb3-42e8-922f-7661095bdb8c.aspx)|
|Federation trusts, OAuth|[Organization Management](https://docs.microsoft.com/exchange/organization-management-exchange-2013-help)|
|Test federation trusts, OAuth|[Organization Management](https://docs.microsoft.com/exchange/organization-management-exchange-2013-help) <br/> [View-Only Organization Management](https://technet.microsoft.com/library/c514c6d0-0157-4c52-9ec6-441d9a30f3df.aspx) <br/> [Server Management](https://technet.microsoft.com/library/30cbc4de-adb3-42e8-922f-7661095bdb8c.aspx)|
|Hybrid deployment configuration|[Organization Management](https://docs.microsoft.com/exchange/organization-management-exchange-2013-help)|
|Intra-Organization connectors|[Organization Management](https://docs.microsoft.com/exchange/organization-management-exchange-2013-help) <br/> [Recipient Management](https://technet.microsoft.com/library/669d602e-68e3-41f9-a455-b942d212d130.aspx) <br/> [Records Management](https://technet.microsoft.com/library/0e0c95ce-6109-4591-b86d-c6cfd44d21f5.aspx)|
