---
title: "Role assignment policies in Exchange Online"
ms.author: chrisda
author: chrisda
manager: serdars
ms.date: 
ms.audience: ITPro
ms.topic: article
ms.service: exchange-online
localization_priority: Normal
ms.assetid: 
description: "Admins can learn about mailbox plans and how view, modify, and set the default mailbox plan in Exchange Online."
---

# Role assignment policies in Exchange Online

A role assignment policy is a collection of one or more end-user roles that enable users to manage their mailbox settings and distribution groups in Exchange Online. End-users roles are part of the role based access control (RBAC) permissions model in Exchange Online. You can assign different role assignment policies to different users to allow or prevent specific self-management features in Exchange Online.

In Exchange Online, a default role assignment policy named Default Role Assignment Policy is specified by the mailbox plan that's assigned to users when their account is licensed. For more information about mailbox plans, see [Mailbox plans in Exchange Online](../recipients-in-exchange-online/manage-user-mailboxes/mailbox-plans.md).

Role assignment polices are how end-user roles (as opposed to management roles) are assigned to users in Exchange Online. There are several ways you can use role assignment policies to assign permissions to users:

- **New users**:

   - Change the end-user roles that are assigned to the default role assignment policy.

   - Create a custom role assignment policy and set it as the default.

   - Specify a custom role assignment policy in the mailbox plan. For more information, see [Use Exchange Online PowerShell to modify mailbox plans](../recipients-in-exchange-online/manage-user-mailboxes/mailbox-plans.md#use-exchange-online-powershell-to-modify-mailbox-plans).

- **Existing users**:

   - Assign a different license to the user. This will apply the settings of the different mailbox plan, which you can modify to specify a different role assignment policy.

   - Manually assign a custom role assignment policy to mailboxes.

The available end-user roles are described in the following table:

|**Role**|**Assigned to Default Role Assignment Policy by default?**|**Description**|
|:-----|:-----|:-----|
|My Custom Apps|Yes|Install custom apps.|
|My Marketplace Apps|Yes|Install marketplace apps.|
|My ReadWriteMailbox Apps|Yes|Install apps with ReadWriteMailbox permissions.|
|MyBaseOptions|Yes|Required for users to access options in Outlook on the web from their own mailbox.|
|MyContactInformation|Yes|Edit their address and telephone number in the global address list (GAL). <br/><br/> This role contains the following child roles: <br/>• **MyAddressInformation**: Change all elements of their mailing address, work telephone number, and fax number. <br/>• **MyMobileInformation**: Change their mobile phone and pager numbers. <br/>• **MyPersonalInformation**: Change their home telephone number and web page. <br/><br/> If you think this role gives users too much power, you can remove the role from the role assignment policy, and assign one or more of the child roles.|
|MyDistributionGroupMembership|Yes|Join or leave existing distribution groups (if the group is configured to let them do that).|
|MyDistributionGroups|Yes|Create new distribution groups, delete groups they own, modify groups they own, and manage group membership for groups they own|
|MyMailboxDelegation|No|Allows users to grant send on behalf of permissions to other users on their mailbox. Messages clearly show the sender in the From field (\<Sender\> on behalf of \<Mailbox\>), but replies are delivered to the mailbox, not the sender.|
|MyMailSubscriptions|Yes|Connected accounts were removed from Outlook on the web in November, 2018. For more information, see [Connected accounts is no longer supported in Outlook on the web](https://support.office.com/article/5cc526bf-e928-4a99-8b9f-5e089df7d887).|
|MyProfileInformation|Yes|Edit their first name, middle initial, last name, and display name in the GAL. <br/><br/> This role contains the following child roles: <br/>• **MyDisplayName**: Change their display name. <br/>• **MyName**: Change their first name, middle initial, last name and Notes property. <br/><br/> If you think this role gives users too much power, you can remove the role from the role assignment policy, and assign one of the child roles.|
|MyRetentionPolicies|Yes|Allows users to add personal tags that aren't part of their assigned retention policy.<sup>*</sup>|
|MyTeamMailboxes|Yes|Allowed user to create and connect to site mailboxes in SharePoint Online. Site mailboxes were discontinued in favor of Office 365 groups in September, 2017. For more information, see [Use Office 365 Groups instead of Site Mailboxes](https://support.office.com/article/737d6b1f-67cc-41fe-8db8-f2d09dd1673b).|
|MyTextMessaging|Yes|Enable text message notifications for meetings and new email messages.<sup>*</sup>|
|MyVoiceMail|Yes|Update their voice mail settings.<sup>*</sup>|

<sup>*</sup>This feature isn't available in all regions or organizations.

## Procedures for mailbox plans

### What do you need to know before you begin?

- Estimated time to complete each procedure: 2 minutes.

- The procedures in this topic require the Role Management RBAC role in Exchange Online. Typically, you get this permission via membership in the Organization Management role group (the Office 365 Global administrator role). For more information, see [Manage role groups in Exchange Online](role-groups.md).

- To open the Exchange admin center (EAC), see [Exchange admin center in Exchange Online](../exchange-admin-center.md). To connect to Exchange Online PowerShell, see [Connect to Exchange Online PowerShell](https://docs.microsoft.com/powershell/exchange/exchange-online/connect-to-exchange-online-powershell/connect-to-exchange-online-powershell).
    
> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at [Exchange Online](https://go.microsoft.com/fwlink/p/?linkId=267542) or [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkId=285351).