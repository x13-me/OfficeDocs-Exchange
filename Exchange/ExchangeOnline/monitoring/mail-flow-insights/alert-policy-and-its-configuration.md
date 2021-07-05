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

System policy is created by the system, by default. A **System** policy automatically maps a newly newly created tenant to it.

> [!IMPORTANT]
> A user/tenant requires **security administrator** privileges to edit a **System** policy. A user/tenant requires **security reader** privileges to view/read the **System** policy (see [Viewing/reading an alert policy](#viewingreading-an-alert-policy)).

### Custom policy

Custom policy is the policy that can be manually created by the user/tenant.

> [!IMPORTANT]
> **Security administrator** privileges are required for creating an alert policy (see). For information on creating an alert policy, see [Creating an alert policy](#creating-an-alert-policy).

In addition to creating an alert policy, a user with **security administrator** privileges can execute the following tasks:

- Edit the policy
- Disable the policy
- Disbale the email notifications

> [!IMPORTANT]
> **Security reader** privileges are required for viewing/reading an alert policy. For more information, see [Viewing/reading an alert policy](#viewingreading-an-alert-policy).

#### Creating an alert policy

To create an alert policy, perform the following steps:

1. Launch the URL https://admin.exchange.microsoft.com.
2. In the left pane, choose **Mail flow > Alert policies**, and click **New alert policy**. 
3. Provide a name for your policy in the **Name** box and click **Next**.

> [!NOTE]
> Entering a description for the policy in the **Description** box is optional.

4. From the **Severity** drop-down list, select the severity level.

> [!NOTE]
> The **Category** drop-down list is disabled because **Mail flow** is the only category supported in the new EAC. Therefore, after Step 4, the next step is selection of the insight type.

5. From the **Trigger an alert when the following insight is generated** drop-down list, select one of the four insight types.

6. Click **Next**.
7. Provide the name or email address of the alert notification recipients in the **Email recipients** box.
8. From the **Daily notification limit** drop-down list, select daily-notification count.

> [!NOTE] 
> Choosing the daily-notification count value is optional.

9. Click **Next**.
10. Review the alert-policy settings and click **Create**.
    The alert policy is created.

**Insights for which an alert policy can be created**

A user/tenant can create an alert policy for the following mail flow-related insights:

- Mail loop
- Slow transport rule
- New users forwarding
- New domains being forwarded

#### Viewing/reading an alert policy

An alert policy (**System** or **Custom**) is displayed on the **Alerts** screen. The users can view

To view/read an alert policy , perform the following steps:

1. Launch the URL https://admin.exchange.microsoft.com.
2. In the left pane, choose **Mail flow > Alerts**.
   The **Alerts** screen appears, displaying reports of the various alert policies created.
3. Under the **Alert name** column, click the alert for which you want to view the details.
   The alert policy details screen appears.
4. Click **View details**.
   The screen containing elaborate details of the alert policy appears.
