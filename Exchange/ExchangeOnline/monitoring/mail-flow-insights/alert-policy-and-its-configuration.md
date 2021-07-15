---
title: "Alert policy and its configuration"
f1.keywords:
ms.author: v-smandalika
author: v-smandalika
manager: dansimp
audience: ITPro
ms.topic: article
ms.service: exchange-online
localization_priority: Normal
ms.assetid:
description: This alert policy allows you to track and manage your activities. 
ms.custom:
---

# Alert policy

An alert policy is the mechanism that enables you to track events related to mail flow in the new Exchange Admin Center (EAC).

## Privileges for alert policy management

> [!IMPORTANT]
> **Security administrator** privileges are required to create and manage an alert policy; **Security reader** privileges are required to read/view an alert policy.

## Types of alert policies

There are two types of alert policies, namely **System** and **Custom**.

1. **System** - See [System policy](#system-policy)
2. **Custom** - See [Custom policy](#custom-policy)

### System policy

System policy is created by the system, by default. A **System** policy automatically maps a newly created tenant to it.

> [!IMPORTANT]
> A user/tenant requires **security administrator** privileges to edit a **System** policy. A user/tenant requires **security reader** privileges to view/read the **System** policy (see [Viewing/reading an alert policy](#viewingreading-an-alert-policy)).

### Custom policy

Custom policy is the policy that can be manually created by the user/tenant.

> [!IMPORTANT]
> **Security administrator** privileges are required for creating an alert policy (see). For information on creating an alert policy, see [Creating an alert policy](#creating-an-alert-policy).

**Insights for which an alert policy can be created**

A user/tenant can create an alert policy for the following mail flow-related insights:

- Mail loop
- Slow transport rule
- New users forwarding
- New domains being forwarded

#### Creating an alert policy

To create an alert policy, perform the following steps:

1. Launch the URL https://admin.exchange.microsoft.com.
2. In the left pane, select **Mail flow > Alert policies**, and click **New alert policy**. 
3. Provide a name for your policy in the **Name** box and click **Next**.

> [!NOTE]
> Entering a description for the policy in the **Description** box is optional.

4. From the **Severity** drop-down list, select the severity level.

> [!NOTE]
> The **Category** drop-down list is disabled because **Mail flow** is the only category supported in the new EAC. Therefore, after Step 4, the next step is selection of the insight type.

5. From the **Trigger an alert when the following insight is generated** drop-down list, select one of the four insight types.

6. Click **Next**.
7. Provide the name or email address of the alert notification recipients in the **Email recipients** box.
8. From the **Daily notification limit** drop-down list, select daily notification count.

> [!NOTE] 
> Choosing the daily-notification count value is optional.

9. Click **Next**.
10. Review the alert-policy settings and click **Create**.
    The alert policy is created.

## Tasks on alert policies

A user with **security administrator** privileges - in addition to creating an alert policy - can perform the following tasks on an alert policy:

- **Editing**: A user can edit both the **system** and **custom** policies. For more information, see Edit the policy.
- **Disabling**: A user can disable both the **system** and **custom**. For more information, see [Disable the policy](#disable-the-policy).  
- **Disabling its email notifications**: A user can disable the email notifications pertaining to both **system** and **custom** policies. For more information, see [Disable the email notifications](#disable-the-email-notifications).
- **Viewing**: A user can view alert policies (system or custom) on the **Alerts** screen.

> [!IMPORTANT]
> **Security reader** privileges are required for viewing/reading an alert policy. For more information, see [Viewing/reading an alert policy](#viewingreading-an-alert-policy).

### Edit the policy

A user can edit the following types of alerts:

**Of custom policies**

- Domain loop
- New users forwarding emails
- Slow mailflow rules
- New domains being forwarded emails

The procedure to edit an alert policy is the same for all types of **custom** policies. For information on how to edit a custom policy, see [Editing a custom policy](#editing-a-custom-policy)

**Of system policies**

- Messages for priority accounts are delayed or rejected
- Messages for normal accounts have been delayed

#### Editing a custom policy

To edit an alert of the type **domain loop**, perform the following steps:

1. On the left navigation pane of the new EAC, select **Mail flow** > **Alert policies**.
1. Select the policy that you want to edit, and click on it.
   The policy details screen appears.
   :::image type="content" source="../../media/domain-loop-alert-edit.png" alt-text="The screen displaying details of the alert policy":::
1. Click the **Settings** tab.
   :::image type="content" source="../../media/settings-tab-domain-loop.png" alt-text="The screen displaying the settings parameters for the insight type of domain loop":::
1. Edit the value in either or both of the following fields:
    1. Send email notifications to these users or groups.
    1. Daily notification limit
1. Click **Save**.

#### Editing system policies

This section describes the procedure to edit the following types of system policies:

- **Messages for priority accounts are delayed or rejected**: This type of system policy can be edited in two methods. For detailed information, see [Method 1](#method-1) and [Method 2 (1)](#method-2-1).
- **Messages for normal accounts are delayed**: This type of system policy can be edited in the procedure identical to the one implemented for the type **Messages for priority accounts are delayed or rejected**. See [Method 1](#method-1).

There are two methods by which a user can edit the alert type **Messages for priority accounts are delayed or rejected**.

##### Method 1

1. On the left navigation pane of the new EAC, select **Mail flow** > **Alert policies**.
1. Select the policy that you want to edit, and click on it.
   The policy details screen appears.
   :::image type="content" source="../../media/priority-accounts-alert-type.png" alt-text="The screen displaying the details of alert policy that has the insight type of priority accounts":::
1. Click the **Settings** tab.
1. Edit the value in any or all of the following fields:
    1. Send email notifications to these users or groups.
    1. Daily notification limit
    1. Threshold
1. Click **Save**.

##### Method 2

1. On the left navigation pane of the new EAC, select **Reports** > **Mail flow**.
1. Select the radio button for **Email issues for priority accounts**.
1. On the screen that appears, click **Edit policy**.
   The **Edit policy** screen appears.
   :::image type="content" source="../../media/priority-account-alert-type-2.png" alt-text="The screen on which you can edit the settings of an alert policy":::
1. Edit the value in any or all of the following fields:
    1. Send email notifications to these users or groups.
    1. Daily notification limit
    1. Threshold
1. Click **Save**.

#### Messages for normal accounts are delayed

To edit the alert of the type **Messages for normal accounts are delayed**, follow the procedure specified in [Method 1](#method-1)

### Disable the policy

To disable an alert policy, perform the following steps:

1. In the left navigation pane of the new EAC, select **Mail flow** > **Alert policies**.
   The **Alert policies** screen appears.
1. Select the alert policy you want to disable and click on it.
   :::image type="content" source="../../media/selecting-an-alert-policy-to-disable.png" alt-text="The screen on which you select an alert policy to disable it":::
   The alert policy details screen appears.
1. Uncheck the **Enable this policy** check box.
   :::image type="content" source="../../media/disabling-alert-policy.png" alt-text="The screen on which you disable an alert policy by unchecking the check box":::
1. Click **Save**.
   The alert policy is disabled. The user will no longer receive any email notifications pertaning to this alert policy.

### Disable the email notifications

A user has the option of disabling just the email notifications pertaining to an alert policy. This results in non-receipt of email notifications of the alert policy. However, the details of the alert policy can continue to be viewed on the **Alerts** screen.

To disable the email notifications of an alert policy, perform the following steps:

1. In the left navigation pane of the new EAC, select **Mail flow** > **Alert policies**.
   The **Alert policies** screen appears.
1. Select the alert policy for which you to disbale email notifications.
   :::image type="content" source="../../media/selecting-an-alert-policy-to-disable.png" alt-text="The screen on which you select an alert policy for which email notifications are to be disabled":::
   The alert policy details screen appears.
1. Click the **Settings** tab.
1. Uncheck the **Send email notifications** check box.
   :::image type="content" source="../../media/disabling-email-notifications.png" alt-text="The screen on which the email notifications for an alert policy are disabled":::
   The email notifications for the alert policy are disabled, and the user will no longer receive email notifications pertaining to the alert policy.


#### Viewing/reading an alert policy

An alert policy (**System** or **Custom**) is displayed on the **Alerts** screen. The users can view

To view/read an alert policy, perform the following steps:

1. Launch the URL https://admin.exchange.microsoft.com.
2. In the left pane, select **Mail flow > Alerts**.
   The **Alerts** screen appears, displaying reports of the various alert policies created.
3. Under the **Alert name** column, click the alert for which you want to view the details.
   The alert policy details screen appears.
4. Click **View details**.
   The screen containing elaborate details of the alert policy appears.
