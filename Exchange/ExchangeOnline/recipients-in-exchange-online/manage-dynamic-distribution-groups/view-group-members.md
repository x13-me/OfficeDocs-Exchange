---
ms.localizationpriority: medium
description: Dynamic distribution groups are distribution groups whose membership is based on specific recipient filters rather than a defined set of recipients. Microsoft Exchange provides precanned filters to make it easier to create recipient filters for dynamic distribution groups. A precanned filter is a commonly used filter that you can use to meet a variety of recipient-filtering criteria. You can specify the recipient types you want to include in a dynamic distribution group. Additionally, you can also specify a list of conditions that the recipients must meet. You can use Exchange Online PowerShell to preview the list of recipients for a dynamic distribution group that uses precanned filters.
ms.topic: article
author: JoanneHendrickson
ms.author: jhendr
ms.assetid: 40b100c6-864e-4c82-9f98-08dd5c83e378
ms.reviewer: 
f1.keywords:
- NOCSH
title: View members of a dynamic distribution group in Exchange Online
ms.collection: 
- exchange-online
- M365-email-calendar
audience: ITPro
ms.service: exchange-online
manager: serdars

---

# View members of a dynamic distribution group in Exchange Online

Dynamic distribution groups are distribution groups whose membership is periodically calculated based on specific recipient properties that are used as filters (precanned filters for custom filters). For more information, see [Manage dynamic distribution groups](manage-dynamic-distribution-groups.md).

You can use Exchange Online PowerShell to view the list of recipients for a dynamic distribution group. You can't view members of a dynamic distribution in the Exchange admin center (EAC).

## What do you need to know before you begin?

- Estimated time to complete: 2 minutes.

- You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Recipients" entry in the [Feature permissions in Exchange Online](../../permissions-exo/feature-permissions.md) topic.

- For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts for the Exchange admin center](../../accessibility/keyboard-shortcuts-in-admin-center.md).

> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at [Exchange Online](https://social.technet.microsoft.com/forums/msonline/home?forum=onlineservicesexchange) or [Exchange Online Protection](https://social.technet.microsoft.com/forums/forefront/home?forum=FOPE).

## Use Exchange Online PowerShell to preview the list of members of a dynamic distribution group
<a name="Shell"> </a>

This example returns the list of members for the dynamic distribution group named Full Time Employees.

```PowerShell
$FTE = Get-DynamicDistributionGroup "Full Time Employees"
Get-Recipient -RecipientPreviewFilter $FTE.RecipientFilter -OrganizationalUnit $FTE.RecipientContainer
```

This example displays the list of users and email addresses for the same group if it has more than 1,000 members.

```PowerShell
$FTE = Get-DynamicDistributionGroup "Full Time Employees"
Get-Recipient -ResultSize Unlimited -RecipientPreviewFilter $FTE.RecipientFilter -OrganizationalUnit $FTE.RecipientContainer | Format-Table Name,Primary*
```

For detailed syntax and parameter information, see [Get-DynamicDistributionGroupMember](/powershell/module/exchange/get-dynamicdistributiongroupmember).

## How do you know this worked?

To verify that you've successfully viewed the members of a dynamic distribution group, run **Get-DynamicDistributionGroupMember** to view the list of group members. For example, if you created a new user mailbox with properties that match the recipient filter for the dynamic distribution group, this new mailbox should be displayed in the list of group members.
