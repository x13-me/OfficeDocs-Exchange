---
localization_priority: Normal
description: Learn about the changes to Modern Dynamic distribution groups.
ms.topic: article
author: JoanneHendrickson
f1.keywords:
- CSH
ms.custom:
- Microsoft.Exchange.Management.SnapIn.Esm.Recipients.CreateDynamicGroupWizardForm.CreateDynamicGroupInformationWizardPage
ms.author: jhendr
ms.assetid: 8ef85d0a-41df-4b5c-b8e7-ca8d09c048ca
ms.reviewer: 
title: Manage dynamic distribution group
ms.collection: 
- exchange-online
- M365-email-calendar
audience: ITPro
ms.service: exchange-online
manager: serdars

---
# Modern Dynamic Distribution Groups

>[!Important]
>This is feature is currently in private preview.

## Modern Dynamic Distribution Groups 

Dynamic Distribution Groups (DDGs) are changing to bring a more reliable, predictable, and better performing experience. The new change will reduce mail delivery latency, improve service reliability, and allow you to see the members of a DDG before sending a message. 

**What has changed?**
Before, DDGs were resolved only when mail was sent, and as a result the actual recipient list was unknown to the sender. 

Now the membership list will be stored for each DDG and the membership list will be updated every 24 hours. You'll know exactly to whom the message is being sent, and it also addresses potential compliance issues for our customers. By storing the calculated list of members on the DDG object, messages can be delivered more quickly and our service will have greater reliability. 


## DDG behavior changes

|Change|Old behavior|New behavior|
|:-----|:-----|:-----|
|Creation|DDGs could be used instantly after creation since the filters were evaluated at runtime. |Users will have to wait up to 2 hours for the initial membership list to be calculated |
Modification |DDGs with new modified filters could be used instantly after creation since the filters are evaluated at runtime. |Users will have to wait up to 2 hours for the membership list to be recalculated and for the links to be updated.|
|Membership list “freshness” |The list of members was up to date in real time.|The list of members for each DDG is refreshed every 24 hours.|

>[!Important]
>There may be a period where the list of members is stale. For example, if a member has left a department that was used as a filter for the DDG, they may still receive mail from the DDG for the next 24 hours before the list is refreshed. 
>
> **Exchange Transport Rules** (ETRs) are also impacted by this change.  As the membership list used for ETRs will also be refreshed every 24 hours, the membership list used may be stale during the refresh period .
 
## How to view members of a DDG

View members belonging to any DDG using the following cmdlet, where *DynamicDistributionGroupIdentity* is the name, alias, or email address of the DDG. 

```PowerShell

Get-DynamicDistributionGroupMember -Identity <DynamicDistributionGroupIdentity> 

```

This PowerShell cmdlet returns the calculated list of members stored on the Dynamic Distribution Group object. 
To learn more, see: [Get-DynamicDistributionGroupMember](https://docs.microsoft.com/en-us/powershell/module/exchange/get-dynamicdistributiongroupmember?view=exchange-ps#inputs). 

>[!Note]
> Do not follow the old procedures for viewing the members of a Dynamic Distribution Group at <View members of a dynamic distribution group | Microsoft Docs>. The instructions found in that article only evaluates the users in your organization that satisfy the filters specified in your Dynamic Distribution Group at that time.  It does not return the calculated list of members stored on the group object. 

## How to refresh a DDG’s membership list 

If your DDG membership list is not updated after the 24-hour refresh period, you can force a membership list refresh.  Use the following cmdlet, where *DynamicDistributionGroupIdentity* is the name, alias, or email address of the DDG.

```PowerShell
Set-DynamicDistributionGroup -Identity <DynamicDistributionGroupIdentity> -ForceMembershipRefresh 

``` 

>[!Note]
> This cmdlet can only be run after more than 1 hour has passed since the last membership refresh.
 
## Support 

If you further assistance, contact the [Modern DDG Support team](modernddgsupport@service.microsoft.com).

