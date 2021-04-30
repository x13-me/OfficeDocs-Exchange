---
localization_priority: Normal
description: Admins can learn how to use connectors and mail flow rules to route mail in Exchange Online
ms.topic: article
author: msdmaguire
ms.author: jhendr
ms.assetid: 82d105e2-e955-4e03-99c3-3314a5d21a4c
ms.reviewer: 
f1.keywords:
- NOCSH
title: Scenario Conditional mail routing in Exchange Online
ms.collection: exchange-online
audience: ITPro
ms.service: exchange-online
manager: serdars

---

# Scenario: Conditional mail routing in Exchange Online

There might be times you need to route mail differently depending on whom the mail is sent to or from, where it's being sent, the contents of the message, and so on. For example, if you have multiple sites around the world, you might want to route mails to a specific site. You can do this using connectors and mail flow rules (also known as transport rules).

When the steps below are completed, a mail flow rule will redirect messages addressed to users whose City property is set to New Orleans to the IP address specified by the connector from Office 365 to your organization's email server.

## Step 1: Use the Exchange admin center to create the connector

The first thing we need to do is create a connector from Office 365 to your organization's email server. This connector will be used by the mail flow rule that we'll set up in Step 2. In this connector, you'll select where received messages originate from (such as a mailbox in your Microsoft 365 or Office 365 organization), the type of organization to which the messages will be sent (such as your on-premises servers), the security that should be applied to the connection, and name or IP address of the target server. If you want to learn more about how to create connectors, check out [Configure mail flow using connectors](use-connectors-to-configure-mail-flow.md).

The subsequent two procedures are for creating connectors from Office 365 to your organization's email server. These connectors are to be created in the New Exchange admin center (EAC) and Classic EAC.

### New EAC

1. Navigate to **Mail flow** \> **Connectors**. The **Connectors** screen appears.

2. Click **+ Add a new connector**. The **New connector** screen appears.

3. Under **Connection from**, choose **Office 365**.
    
4. Under **Connection to**, choose either **Your organization's email server** or **Partner organization** (if you want to connect to a server other than your organizations).

:::image type="content" source="../../media/365-to-your-organization.png" alt-text="The screen on which a connector is being created from Office 365 to your organization's mail server":::

5. Click **Next**. The **Connector name** screen appears.

6. Provide a name for the connector and add a description.

7. Check the check box for **Turn it on** under **What do you want to do after connector is saved?**

:::image type="content" source="../../media/providing-a-connector-name-and-turning-on.png" alt-text="The screen on which a name is given to the connector that is then turned on":::

8. Click **Next**. The **Use of connector** screen appears.

9. Choose **Only when I have a transport rule set up that redirects messages to this connector**.

:::image type="content" source="../../media/configuring-transport-rule.png" alt-text="A screen on which the transport rule is chosen as a condition":::

10. Click **Next**. The **Routing** screen appears.

11. Enter one or more smart hosts in the text box. (These smart hosts are the ones to which Microsoft 365 or Office 365 will deliver email messages.)

> [!NOTE]
> You must provide either the domain name or the IP address of the server.

12. Click **+**. The smart host value is displayed under the text box.

:::image type="content" source="../../media/specifying-smart-host.png" alt-text="The screen on which the smart host address is defined":::

> [!NOTE]
> It is mandatory to click **+** after entering the smart host name to navigate to the next screen.

13. Click **Next**. The **Security restrictions** screen appears.

14. Check the check box for **Always use Transport Layer Security (TLS) to secure the connection (recommended)**.

:::image type="content" source="../../media/define-tls-settings.png" alt-text="The screen on which TLS settings are defined":::

15. Click **Next**. The **Validation email** screen appears.

16. Enter an email address that is valid on the mailbox of your organization's email server.

17. Click **+**. The email address is displayed below the text box, indicating it is ready to be validated.

18. Click **Validate**. The validation process starts.

19. Once the validation process is completed, click **Next**. The **Review connector** screen appears.

20. Review the settings for the new connector and click **Create connector**. The connector is created.

### Classic EAC

1. Go to **Mail flow** \> **Connectors** and click **New** ![Add Icon](../../media/ITPro_EAC_AddIcon.gif) to create a new connector.

2. In the **From:** drop-down box, choose **Office 365**.

3. In the **To:** drop-down box, choose either Your organization's email server or Partner organization if you want to connect to a server other than your organizations.

   ![route to and from options](../../media/eaa1aabd-31fa-4598-921b-7803182f7b5f.png)

4. Name the connector and add a description. If you want to turn on the connector immediately, check **Turn it on**. Click **Next**.

   ![name connector](../../media/f4b47d74-3251-4d04-83aa-7978ba5cd0e4.png)

5. Choose **Only when I have a transport rule...** and click **Next**.

   ![transport rule option](../../media/5aab8ee0-7244-41ea-b504-71ff3e5d1f18.png)

6. Specify one or more smart hosts to which Microsoft 365 or Office 365 will deliver email messages.

   ![add host](../../media/d41ef961-224c-4c7e-8ac8-756b785a73fc.png)

7. Define your Transport Layer Security (TLS) settings depending on your security needs.

   ![define TLS settings](../../media/728b161e-7780-4686-a169-df37a7f96531.png)

8. Review your new connector configurations and click **Next** to validate the connector.

## Step 2: Use the EAC to create a mail flow rule

Now that we've created a connector, we need to create a mail flow rule that will send mail to it based on the criteria you define. There are many conditions you can select from to control when messages should be sent to the connector.

To create a mail flow rule in EAC, perform the following steps:

> [!NOTE]
> The below procedure is applicable for New and Classic EACs.

1. In the EAC, navigate to **Mail flow** \> **Rules**. Click **New** ![Add Icon](../../media/ITPro_EAC_AddIcon.gif) and choose **Create a new rule...**.

2. In the **New rule** window, name the rule. To see all the options available for the rule, click **More options...** at the bottom of the page.

   ![click more options](../../media/96c2ca71-32b2-423c-99f6-1ee35c63af5c.png)

3. For **\*Apply this rule if...**, select **The recipient...** and **has specific properties including any of these words**. The **select user properties** box appears. Click ![Add Icon](../../media/ITPro_EAC_AddIcon.gif), and under **User properties:** choose **City**. **City** is an Active Directory attribute made available for use by the rule. Specify the name of the city, such as New Orleans. Click **OK**, and then click **OK** again to close the **select user properties** box.

   ![apply rule if](../../media/98b9ea9b-ca67-44bd-99ff-a8e3ca0493bc.png)

   > [!IMPORTANT]
   > Check the accuracy of user attributes in Active Directory to ensure that the mail flow rule works as intended. > Note that changes made in the connector from Office 365 to your organization's email server take time to replicate.

4. For **\*Do the following...**, choose **Redirect the message to...** and then specify **the following connector**. The **select connector** box appears. Choose the connector from Office 365 to your organization's email server which you created previously.

You can choose more properties for the rule, such as the test mode and when to activate the rule.

5. To save the connector, click **Save**.
