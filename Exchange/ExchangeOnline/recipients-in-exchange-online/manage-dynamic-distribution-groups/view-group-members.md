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

To view the members of a DDG, replace \<DDGIdentity\> with the name, alias, or email address of the DDG and run the following command in [Exchange Online PowerShell](/powershell/exchange/connect-to-exchange-online-powershell). The command returns the calculated list of members that's stored on the dynamic distribution group object.

```PowerShell
Get-DynamicDistributionGroupMember -Identity <DDGIdentity>
```

For detailed parameter and syntax information, see [Get-DynamicDistributionGroupMember](/powershell/module/exchange/get-dynamicdistributiongroupmember).

> [!NOTE]
> Don't use the old procedure for viewing members of a DDG as described in [View members of a dynamic distribution group in Exchange Online](/exchange/recipients-in-exchange-online/manage-dynamic-distribution-groups/view-group-members). The old procedure returns all users that satisfy the DDG filters at the time you run the command. The old procedure does not return the calculated list of members that are stored on the DDG object.

## Refresh the membership of a DDG

If your DDG membership list isn't updated after the next 24-hour refresh interval, you can force a membership refresh by replacing \<DDGIdentity\> with the name, alias, or email address of the DDG and running the following command in [Exchange Online PowerShell](/powershell/exchange/connect-to-exchange-online-powershell):

```PowerShell
Set-DynamicDistributionGroup -Identity <DDGIdentity> -ForceMembershipRefresh
```

For detailed syntax and parameter information, see [Set-DynamicDistributionGroup](/powershell/module/exchange/set-dynamicdistributiongroup)

> [!NOTE]
> You can run the refresh command only after more than one hour has passed since the last membership refresh.


Dynamic distribution groups are distribution groups whose membership is periodically calculated based on specific recipient properties that are used as filters (precanned filters for custom filters). For more information, see [Manage dynamic distribution groups](manage-dynamic-distribution-groups.md).

You can use Exchange Online PowerShell to view the list of recipients for a dynamic distribution group. You can't view members of a dynamic distribution in the Exchange admin center (EAC).

## What do you need to know before you begin?

- Estimated time to complete: 2 minutes.

- You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Recipients" entry in the [Feature permissions in Exchange Online](../../permissions-exo/feature-permissions.md) topic.

- For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts for the Exchange admin center](../../accessibility/keyboard-shortcuts-in-admin-center.md).

> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at [Exchange Online](https://social.technet.microsoft.com/forums/msonline/home?forum=onlineservicesexchange) or [Exchange Online Protection](https://social.technet.microsoft.com/forums/forefront/home?forum=FOPE).

