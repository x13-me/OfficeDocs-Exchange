---
title: "Mailbox plans in Exchange Online"
ms.author: chrisda
author: chrisda
manager: serdars
ms.date: 
ms.audience: ITPro
ms.topic: article
ms.service: exchange-online
localization_priority: Normal
ms.assetid: 
description: "Admins can learn about mailbox plans in Exchange Online."
---

# Mailbox plans in Exchange Online

A mailbox plan is a template that automatically configures certain mailbox properties on new mailboxes. Mailbox plans correspond to Office 365 license types. The only way to change the mailbox plan of an existing mailbox is to assign a different license to the user.

When you modify a mailbox plan, existing mailboxes aren't updated with the new settings. But, you can change the same settings directly on mailboxes.

The following table describes the mailbox plans that you're likely to see in Exchange Online.

|**Subscription**|**Mailbox plan display name**|
|:-----|:-----|
|Exchange Online Kiosk|ExchangeOnlineDeskless|
|Office 365 Enterprise E1 <br/><br/> Exchange Online Plan 1|ExchangeOnline|
|Office 365 Enterprise E3 <br/><br/> Office 365 Enterprise E5 <br/><br/> Exchange Online Plan 2|ExchangeOnlineEnterprise|
|Office 365 Business Essentials|ExchangeOnlineEssentials|

**Notes**:

- The availability of a mailbox plan is determined by your selections when you enroll in Office 365. A subscription can include multiple mailbox plans.

- The name value of the mailbox plan is appended with `-<GUID>` (for example, `ExchangeOnlineEnterprise-44107b46-a8c4-4573-a7ba-bb004fde4d58`).

The following table describes the mailbox settings that are controlled by mailbox plans.

|**Setting**|**Default value**|**Cmdlet**|**Description**|
|:-----|:-----|:-----|:-----|
|_ActiveSyncEnabled_|True|**Set-CasMailboxPlan**|Enables or disables Exchange ActiveSync (EAS) access to mailboxes.|
|_ImapEnabled_|True|**Set-CasMailboxPlan**|Enables or disables IMAP4 access to mailboxes.|
|_IssueWarningQuota_|Varies by license|**Set-MailboxPlan**|The user receives a warning message when their mailbox reaches the specified size. <br/><br/> For more information, see [Capacity alerts](https://docs.microsoft.com/office365/servicedescriptions/exchange-online-service-description/exchange-online-limits#capacity-alerts).|
|_MaxReceiveSize_|Varies by license|**Set-MailboxPlan**|The maximum total message size that can be received by the mailbox. This value is roughly 33% larger than the actual message size to account for Base64 encoding. <br/><br/> For more information, see [Message limits across Office 365 options](https://docs.microsoft.com/office365/servicedescriptions/exchange-online-service-description/exchange-online-limits#message-limits-across-office-365-options).|
|_MaxSendSize_|Varies by license|**Set-MailboxPlan**|The maximum total message size that can be sent from the mailbox. This value is roughly 33% larger than the actual message size to account for Base64 encoding. <br/><br/> For more information, see [Message limits across Office 365 options](https://docs.microsoft.com/office365/servicedescriptions/exchange-online-service-description/exchange-online-limits#message-limits-across-office-365-options).|
|_OwaMailboxPolicy_|OwaMailboxPolicy-Default|**Set-CasMailboxPlan**||
|_PopEnabled_|True|**Set-CasMailboxPlan**|Enables or disables IMAP4 access to mailboxes.|
|_ProhibitSendQuota_|Varies by license|**Set-MailboxPlan**|The user receives a warning message and they can't send messages when their mailbox reaches the specified size (which must be greater than the _IssueWarningQuota_ value). <br/><br/> For more information, see [Capacity alerts](https://docs.microsoft.com/office365/servicedescriptions/exchange-online-service-description/exchange-online-limits#capacity-alerts).|
|_ProhibitSendReceiveQuota_|Varies by license|**Set-MailboxPlan**|The user receives a warning message and they can't send or receive messages when their mailbox reaches the specified size (which must be greater than the _ProhibitSendQuota_ value). <br/><br/> For more information, see [Capacity alerts](https://docs.microsoft.com/office365/servicedescriptions/exchange-online-service-description/exchange-online-limits#capacity-alerts).|
|_RetainDeletedItemsFor_|`14.00:00:00` (14 days)|**Set-MailboxPlan**||
|_RetentionPolicy_|Default MRM Policy|**Set-MailboxPlan**||
|_RoleAssignmentPolicy_|Default Role Assignment Policy|**Set-MailboxPlan**||

## What do you need to know before you begin?

- Estimated time to complete each procedure: 2 minutes.

- You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Mailbox settings" entry in the [Feature permissions in Exchange Online](../../permissions-exo/feature-permissions.md) topic.

- You can only use Exchange Online PowerShell to perform the procedures in this topic. To connect to Exchange Online PowerShell, see [Connect to Exchange Online PowerShell](https://docs.microsoft.com/powershell/exchange/exchange-online/connect-to-exchange-online-powershell/connect-to-exchange-online-powershell).
    
> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at [Exchange Online](https://go.microsoft.com/fwlink/p/?linkId=267542) or [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkId=285351).

## Use Exchange Online PowerShell to view mailbox plans

This example returns a summary list of all mailbox plans:

```
Get-MailboxPlan
```

```
Get-CasMailboxPlan
```

This example returns the values of the modifiable properties in all mailbox plans:

```
Get-MailboxPlan | Format-List DisplayName,IsDefault,Max*Size,IssueWarningQuota,Prohibit*Quota,RetainDeletedItemsFor,RetentionPolicy,RoleAssignmentPolicy
```

```
Get-CasMailboxPlan | Format-List DisplayName,ActiveSyncEnabled,ImapEnabled,PopEnabled,OwaMailboxPolicy
```

This example returns detailed information for the mailbox plan named ExchangeOnlineEnterprise.

```
Get-MailboxPlan -Identity ExchangeOnlineEnterprise | Format-List
```

```
Get-CasMailboxPlan -Identity ExchangeOnlineEnterprise | Format-List
```

This example returns the mailbox plan that's assigned to the user named Suk-Jae Yoo.

```
Get-Mailbox -Identity "Suk-Jae Yoo" | Format-List MailboxPlan
```

For detailed syntax and parameter information, see [Get-MailboxPlan](https://docs.microsoft.com/powershell/module/exchange/mailboxes/get-mailboxplan) and [Get-CasMailboxPlan](https://docs.microsoft.com/powershell/module/exchange/client-access/get-casmailboxplan).

## Use Exchange Online PowerShell to specify the default mailbox plan

The default mailbox plan is used as a template for new mailboxes that you create or enable. To see the current default mailbox plan in your organization, run the following command:



To specify the default mailbox plan, use the following syntax:

```
Set-MailboxPlan -Identity <MailboxPlanIdentity> -IsDefault
```

This example specifies the mailbox plan with the display name ExchangeOnline as the default mailbox plan.

```
Set-MailboxPlan -Identity ExchangeOnline -IsDefault
```

For detailed syntax and parameter information, see [Set-MailboxPlan](https://docs.microsoft.com/powershell/module/exchange/mailboxes/set-mailboxplan).

## How do you know this worked?

To verify that you've successfully specified the default mailbox plan, use any of the following steps: 

- In Exchange Online PowerShell, run the following command to verify the property values:

   ```
   Get-MailboxPlan | Format-Table -Auto DisplayName,IsDefault
   ```

- Create a new mailbox and verify the license that corresponds to the default mailbox plan is selected by default. For more information, see [Create user mailboxes in Exchange Online](../create-user-mailboxes.md).

## Use Exchange Online PowerShell to modify mailbox plans

To modify a mailbox plan, use the following syntax:

```
Set-MailboxPlan -Identity <MailboxPlanIdentity> [-MaxReceiveSize <Size>] [-MaxSendSize <Size>] [-IssueWarningQuota <Size>] [-ProhibitSendQuota <Size>] [-ProhibitSendReceiveQuota <Size>] [-RetainDeletedItemsFor <TimeSpan>] [-RetentionPolicy <RetentionPolicyIdentity>] [-RoleAssignmentPolicy <RoleAssignmentPolicyIdentity>]
```

```
Set-CASMailboxPlan -Identity <MailboxPlanIdentity> [-ActiveSyncEnabled <$true | $false>] [-ImapEnabled <$true | $false>] [-PopEnabled <$true | $false>] [-OwaMailboxPolicy <PolicyIdentity>]
```

This example modifies the mailbox plan named ExchangeOnlineEnterprise to use the retention policy named Contoso Retention Policy.

```
Set-MailboxPlan -Identity -RetentionPolicy "Contoso Retention Policy"
```

This example disables Exchange ActiveSync, POP3, and IMAP4 access to mailboxes in all mailbox plans.

```
Get-CASMailboxPlan | Set-CASMailboxPlan -Identity ExchangeOnlineEnterprise -ActiveSyncEnabled $false -ImapEnabled $false -PopEnabled $false
```

For detailed syntax and parameter information, see [Set-MailboxPlan](https://docs.microsoft.com/powershell/module/exchange/mailboxes/set-mailboxplan) and [Set-CasMailboxPlan](https://docs.microsoft.com/powershell/module/exchange/client-access/set-casmailboxplan).

