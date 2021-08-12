---
localization_priority: Normal
description: Modern Dynamic distribution groups are mail-enabled Active Directory group objects that are created to expedite the mass sending of email messages and other information within a Microsoft Exchange organization.
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

We’re modernizing Dynamic Distribution Groups (DDGs) to bring you a more reliable, more predictable, and better performing experience. We’re making changes that will reduce mail delivery latency, improve service reliability, and allow you to see the members of a DDG. 

What has changed?  
Instead of calculating group membership in real time, we will be storing the membership list for each Dynamic Distribution Group. This membership list will get updated once every 24 hours. 
Previously,  DDGs were resolved only upon being sent, and as a result the actual recipient list is unknown to the sender. This change lets you know the who the message is being sent to and addresses potential compliance issues for our customers. 

By storing the calculated list of members on the Dynamic Distribution Group object, we can deliver messages more quickly and our service will have greatly improved reliability. 


## Changes to DDG behavior 

|Change|Old behavior|New behavior|
|:-----|:-----|:-----|
|Creation|DDGs could be used instantly after creation since the filters were evaluated at runtime. | DDGs are not available for use for up to 2 hours for the initial membership calculation and for the links to be materialized. |
Modification |DDGs with new modified filters could be used instantly after creation since the filters are evaluated at runtime. |Users will have to wait up to 2 hours for the membership list to be recalculated and for the links to be updated.|
|Membership list “freshness” |The list of members was up-to-date in real-time.|The list of members for each DDG is refreshed every 24 hours. The servicelet that expands DDGs worldwide and updates the links runs every 24 hours for each DDG. |

>[!Important]
>There may be a period where the list of members is stale. For example, if a member has left a department that was used as a filter for the DDG, they may still receive mail from the DDG for the next 24 hours before the list is refreshed. 
>
> **Exchange Transport Rules** (ETRs) are also impacted by this change.  As the membership list used for ETRs will also be refreshed every 24 hours, the membership list used may be stale during the refresh period .
 
## How to view members of a DDG

View members belonging to any DDG using the following syntax, where *DynamicDistributionGroupIdentity* is the name, alias, or email address of the DDG. 

```PowerShell

Get-DynamicDistributionGroupMember -Identity <DynamicDistributionGroupIdentity> 

```


This PowerShell cmdlet returns the calculated list of members stored on the Dynamic Distribution Group object. 
For more information, please visit Get-DynamicDistributionGroupMember (ExchangePowerShell) | Microsoft Docs. 

>[!Note]
> Do not follow the old procedures for viewing the members of a Dynamic Distribution Group at <View members of a dynamic distribution group | Microsoft Docs>. The instructions found in that article only evaluates the users in your organization that satisfy the filters specified in your Dynamic Distribution Group at that time.  It does not return the calculated list of members stored on the group object. 

## How to refresh a DDG’s membership list 

If you’re experiencing problems with the Dynamic Distribution Group’s membership list not being updated properly after the 24-hour refresh period, you can force a membership list refresh via the following syntax: 

```PowerShell
Set-DynamicDistributionGroup -Identity <DynamicDistributionGroupIdentity> -ForceMembershipRefresh 

``` 

Where *DynamicDistributionGroupIdentity* is the name, alias, or email address of the dynamic distribution group. 

Limitations 
•	You can only run this cmdlet if the most recent membership refresh was performed more than 1 hour ago. 
 
## Support 

If you further assistance, please contact the [Modern DDG Support team](modernddgsupport@service.microsoft.com).

