---
localization_priority: Normal
description: You can create connectors to apply security restrictions to mail exchanges with a partner organization or service provider. A partner can be an organization you do business with, such as a bank. It can also be a third-party cloud service that provides services such as archiving, anti-spam, and filtering.
ms.topic: article
author: msdmaguire
ms.author: dmaguire
ms.assetid: 1ce4d6a4-41ba-4d1e-9ca9-e826252c1041
ms.reviewer: 
f1.keywords:
- NOCSH
title: Set up connectors for secure mail flow with a partner organization
ms.collection: exchange-online
audience: ITPro
ms.service: exchange-online
manager: serdars

---

# Set up connectors for secure mail flow with a partner organization

You can create connectors to apply security restrictions to mail exchanges with a partner organization or service provider. A partner can be an organization you do business with, such as a bank. It can also be a third-party cloud service that provides services such as archiving, anti-spam, and filtering.

You can create a connector to enforce encryption via transport layer security (TLS). You can also apply other security restrictions such as specifying domain names or IP address ranges that your partner organization sends mail from.

> [!NOTE]
> Setting up a connector to exchange mail with a partner organization is optional; mail flows to and from your partner organization without connectors.

If you use a third-party cloud service for email filtering and need instructions for making this work with Microsoft 365 or Office 365, see [Mail flow best practices for Exchange Online and Microsoft 365 or Office 365 (overview)](../../mail-flow-best-practices/mail-flow-best-practices.md).


## Using connectors to exchange email with a partner organization

By default, Microsoft 365 or Office 365 sends mail using TLS encryption, provided that the destination server also supports TLS. If your partner organization supports TLS, you only need to create a connector if you want to enforce certain security restrictions - for example, you always want TLS applied, or you require certificate verification whenever mail is sent from your partner to your organization.

> [!NOTE]
> For information about TLS, see [How Exchange Online uses TLS to secure email connections](https://docs.microsoft.com/microsoft-365/compliance/exchange-online-uses-tls-to-secure-email-connections) and for detailed technical information about how Exchange Online uses TLS with cipher suite ordering, see [Enhancing mail flow security for Exchange Online](https://www.microsoft.com/microsoft-365/blog/2015/06/29/enhancing-mail-flow-security-for-exchange-online/).

When you set up a connector, email messages are checked to make sure they meet the security restrictions that you specify. If email messages don't meet the security restrictions that you specify, the connector will reject them, and those messages will not be delivered. This makes it possible to set up a secure communication channel with a partner organization.

You can set up one or both of the following depending on your requirements:

- [Set up a connector to apply security restrictions to mail sent from Microsoft 365 or Office 365 to your partner organization](#set-up-a-connector-to-apply-security-restrictions-to-mail-sent-from-microsoft-365-or-office-365-to-your-partner-organization)

- [Set up a connector to apply security restrictions to mail sent from your partner organization to Microsoft 365 or Office 365](#set-up-a-connector-to-apply-security-restrictions-to-mail-sent-from-your-partner-organization-to-microsoft-365-or-office-365)

Also in this article:

- [Change a connector that Microsoft 365 or Office 365 is using for mail flow](#change-a-connector-that-microsoft-365-or-office-365-is-using-for-mail-flow)

- [Example security restrictions you can apply to email sent from a partner organization](#example-security-restrictions-you-can-apply-to-email-sent-from-a-partner-organization)

Review this section to help you determine the specific settings you need for your business.

## Set up a connector to apply security restrictions to mail sent from Microsoft 365 or Office 365 to your partner organization
<a name="setupaconnectortopartner"> </a>
This section describes the process of setting up a connector in both the New Exchange admin center and the Classic Exchange admin center. Before you set up a new connector, check any connectors that are already listed here for your organization. For example, if you already have a connector set up for a partner organization, you'll see it listed. Make sure you don't create duplicate connectors for a single organizational partner; when this happens, it can cause errors, and your mail might not be delivered.

If any connectors already exist for your organization, you can see them listed herez.

(In New Exchange admin center [EAC])
:::image type="content" source="../../media/new-exchange-admin-center.png" alt-text="Existing list of connectors"::: 

(In Classic Exchange admin center [EAC])
![Microsoft 365 and Office 365 connectors partner organization examples](../../media/9e8f0035-24b6-4d62-aecf-17f740530e31.png)

Below are the procedures to set up a new connector

### For New Exchange admin center

To create a connector in Microsoft 365 or Office 365, select **Admin**, and then select **Exchange** to go to the **Exchange admin center**. Next, select **Mail flow** and then **Connectors**. 

To start the wizard, click **+Add a connector**. On the first screen, choose the options that are depicted in the following screenshot:

:::image type="content" source="../../media/add-connector-new-eac.png" alt-text="A page on which a new connector is set up":::

Click **Next**, and follow the instructions in the wizard. Click the Help or Learn More links if you need more information. The wizard will guide you through setup. At the end, make sure your connector validates. If the connector does not validate, see [Validate connectors](https://docs.microsoft.com/exchange/mail-flow-best-practices/use-connectors-to-configure-mail-flow/validate-connectors) for help resolving issues.

### For Classic Exchange admin center

To create a connector in Microsoft 365 or Office 365, select **Admin**, and then select **Exchange** to go to the **Exchange admin center**. Next, select **mail flow** and then **connectors**.

To start the wizard, click the plus symbol **+**. On the first screen, choose the options that are depicted in the following screenshot:

![Microsoft 365 and Office 365 to partner organization connector options](../../media/93cb9e70-f8d8-4e63-bb92-caafd8b79ad7.png)

Click **Next**, and follow the instructions in the wizard. Click the **Help** or **Learn More** links if you need more information. The wizard will guide you through setup. At the end, make sure your connector validates. If the connector does not validate, see [Validate connectors](validate-connectors.md) for help resolving issues.

If you want to create a secure channel with your partner organization in both directions, set up a connector that restricts mail flow from your partner organization to Microsoft 365 or Office 365.

## Set up a connector to apply security restrictions to mail sent from your partner organization to Microsoft 365 or Office 365
<a name="setupconnectorfrompartner"> </a>

You can set up a connector to apply security restrictions to email that your partner organization sends to you. The procedure to set up a connector is described below.

### For New Exchange admin center

To start the wizard, click **+Add a connector**. On the first screen, choose the following options:

:::image type="content" source="../../media/partner-to-365-new-eac.png" alt-text="The screen on which a connector is set up to apply security restrictions":::

### For Classic Exchange admin center

To start the wizard, click the plus symbol **+**. On the first screen, choose the following options:

![Connector from partner organization to Microsoft 365 or Office 365](../../media/e6d15001-989b-48b3-a848-427b800c2a70.png)

Click **Next**, and follow the instructions in the wizard. Click the **Help** or **Learn More** links if you need more information. The wizard will guide you through setup. At the end, save your connector.

**In the context of both New and Classic Exchange admin centers**
Ask your partner organization to send a test email. Make sure the email your partner organization sends will cause the connector to be applied. For example, if you specified security restrictions for mail sent from a specific partner domain, make sure they send test mail from that domain. Check that the test email is delivered to confirm that the connector works correctly.

## Change a connector that Microsoft 365 or Office 365 is using for mail flow
<a name="Changeaconnector"> </a>

To change settings for a connector, perform the procedures specified below.

### For New Exchange admin center

Select the connector you want to edit and then click on the connector. The screen as shown in the following screenshot is displayed.

:::image type="content" source="../../media/connector-editing-screen-new-eac.png" alt-text="The screen on which the connector settings can be edited":::

### For Classic Exchange admin center

Select the connector you want to edit and then select the edit icon as shown in the following screen shot.

![Shows a screen shot with a connector selected and the edit (pencil) icon highlighted.](../../media/9654b36f-40d2-4791-ae5c-ce3afd9bb683.png)

The connector wizard opens, and you can make changes to the existing connector settings. While you change the connector settings, Microsoft 365 or Office 365 continues to use the existing connector settings for mail flow. When you save changes to the connector, Microsoft 365 or Office 365 starts using the new settings.

## Example security restrictions you can apply to email sent from a partner organization
<a name="examplesecurityrestrict"> </a>

Review these connector examples to help you decide whether you want to apply security restrictions to email sent by a partner organization, and understand what settings will meet your business needs:

### Create a partner organization connector

**For New Exchange admin center**

To create a connector in Microsoft 365 or Office 365, select **Admin**, and then select **Exchange** to go to the **Exchange admin center**. Next, select **Mail flow** and then **Connectors**.

To start the wizard, click **+Add a new connector**. To create a connector for email you receive from a partner organization, use the options depicted in the following screenshot:

:::image type="content" source="../../media/partner-to-365-new-eac.png" alt-text="The screen on which you create a connector to receive email from a partner organization":::

**For Classic Exchange admin center**

To create a connector in Microsoft 365 or Office 365, select **Admin**, and then select **Exchange** to go to the **Exchange admin center**. Next, select **mail flow** and then **connectors**.

To start the wizard, click the plus symbol **+**. To create a connector for email you receive from a partner organization, use the options depicted in the following screenshot:

![Connector from partner organization to Microsoft 365 or Office 365](../../media/e6d15001-989b-48b3-a848-427b800c2a70.png)

Once you choose this mail flow scenario (for both, New and Classic Exchange admin centers), you can set up a connector that will apply security restrictions to email that your partner organization sends to you. For some security restrictions, you might need to talk to your partner organization to obtain information to complete some settings. Look for the examples that best meet your needs to help you set up your partner connector.

> [!NOTE]
> Any email sent from your partner organization that does not meet security restrictions that you specify will not be delivered.

### Example 1: Require that email sent from your partner organization domain contosobank.com is encrypted using transport layer security (TLS)
<a name="example1"> </a>

**For New Exchange admin center**

1. Select **Mail flow** and then **Connectors**.
2. Select the connector which is to be used when security restrictions are to be applied for the email sent from the partner organization server.
3. Click on the connector.
The connector details screen as shown in the below screenshot is displayed.

:::image type="content" source="../../media/connector-editing-screen-new-eac.png" alt-text="The screen on which the connector details can be edited":::

4. Click **Edit sent email identity**.
5. Select the **By verifying that the sender domain matches one of the following domains** option, and enter **contosobank.com** in the text box.

:::image type="content" source="../../media/security-restriction-for-connector.png" alt-text="The screen on which security restrictions are configured":::

6. Click the plus icon next to the text box.
7. Click **Save**. A notification message **Connector updated successfully** is displayed.
8. Click **Edit restrictions**.
9. Select the following options:
    - **Reject email messages if they aren't sent over TLS**
10. Click **Save**. A notification message **Connector updated successfully** is displayed.

When you choose these settings, all email from your partner organization's domain, ContosoBank.com, must be encrypted using TLS. Any mail that is not encrypted will be rejected.

**For Classic Exchange admin center**

Use the options shown in the below images for New Exchange admin center and Classic Exchange admin center, respectively:

![Choose to use the sender's domain name](../../media/3b3b0cc6-3928-4cab-a022-436821f9d559.png)

Use this screen to enter your partner organization's domain name(s) so the connector can identify mail sent by your partner:

![Add partner organization domain name](../../media/6ea7db5c-71ff-41cb-bfcd-89be4106f7e1.png)

Choose this setting to require encryption for all email from ContosoBank.com using TLS:

![Choose TLS to encrypt email from partner organization](../../media/0de0e09c-8420-419f-87fc-cf66f10098ec.png)

When you choose these settings, all email from your partner organization's domain, ContosoBank.com, must be encrypted using TLS. Any mail that is not encrypted will be rejected.

### Example 2: Require that email sent from your partner organization domain ContosoBank.com is encrypted and uses their domain certificate
<a name="example1"> </a>

**For New Exchange admin center**

1. Use all the settings configured in Example 1 from Steps 1 through 9.
2. Select the **And require that the subject name of the certificate that the partner uses to authenticate with Office 365 matches this domain name** option.
3. Add the certificate domain name that your partner organization uses to connect with Microsoft 365 or Office 365 in the text box.
4. Click **Save**. A notification message **Connector updated successfully** is displayed.

**For Classic Exchange admin center**

To do this, use all the settings shown in Example 1. Also, add the certificate domain name that your partner organization uses to connect with Microsoft 365 or Office 365. Use this option during setup:

![Enter your partner organization certificate name](../../media/46229d66-dcfd-4e3d-bc12-9f53a5572f81.png)

When you set these restrictions, all mail from your partner organization domain must be encrypted using TLS, and sent from a server with the certificate name you specify. Any email that does not meet these conditions will be rejected.

### Example 3: Require that all email is sent from a specific IP address range
<a name="Example3"> </a>

This email could be from a partner organization, such as ContosoBank.com, or from your on-premises environment. For instance, the MX record for your domain, contoso.com, points to on-premises, and you want all email sent to contoso.com to come from your on-premises IP addresses only. This helps prevent spoofing and makes sure your compliance policies can be enforced for all messages.

To do this, specify your partner organization domain name to identify mail from that partner, and then restrict the IP addresses that you accept mail from. Using an IP address makes the connector more specific because it identifies a single address or an address range that your partner organization sends mail from. 

**For New Exchange admin center**

1. Use all the settings configured in Example 1 from Steps 1 through 7.
2. Click **Edit restrictions**.
3. Select the following options:
    - **Reject email messages if they aren't sent from within this IP address range**
4. Enter the IP address range that determines which are the sent email messages to be accepted.
5. Click the plus icon next to the text box.
6. Click **Save**.
![Enter your partner organization's IP address range](../../media/3a6896f0-3a60-4ef7-91e1-7cf7f24a8bc4.png)

When you set these restrictions, all email sent from your partner organization domain, ContosoBank.com, or from your on-premises environment must be sent from the IP address or an address range you specify. Any mail that does not meet these conditions will be rejected.

### Example 4: Require that all email sent to your organization from the internet is sent from a specific IP address (third-party email service scenario)
<a name="Example3"> </a>

Mail flow from a third-party email service to Microsoft 365 or Office 365 works without a connector. However, in this scenario you can optionally use a connector to restrict all mail delivery to your organization. If you use the settings described in this example, they will apply to *all email sent to your organization*. When all email sent to your organization comes from a single third-party email service, you can optionally use a connector to restrict all mail delivery; only mail sent from a single IP address or address range will be delivered.

**For New Exchange admin center**

1. Use all the settings configured in Example 1 from Steps 1 through 4.
2. Click **Edit sent email identity**.
3. Select the **By verifying that the sender domain matches one of the following domains** option.
4. Enter ***.contoso.com** as shown in the below screenshot.

:::image type="content" source="../../media/configuration-of-sender-ip-address.png" alt-text="The screen on which sender's IP address is entered":::

5. Click the plus icon next to the text box.
6. Click **Save**. A notification message **Connector updated successfully** is displayed.
7. Click **Edit restrictions** and select the **Reject email messages if they aren't sent from within this IP address range** option.
8. Enter the IP address range that determines which are the sent email messages to be accepted.
> [!NOTE]
> Make sure you identify the full range of IP addresses that your third-party email service sends mail from. If you miss an IP address, or if one gets added without your knowledge, some mail will not be delivered to your organization.

9. Click the plus icon next to the text box, and click **Save**.

**For Classic Exchange admin center**
To restrict all mail sent to your organization from a specific IP address or address range, use these options during setup:

![Choose to use the sender's domain name](../../media/3b3b0cc6-3928-4cab-a022-436821f9d559.png)

![Enter "\*" to apply settings to all sender domains](../../media/1be173e2-1c57-4d5d-9bb7-f353c1c29e1f.png)

![Enter your partner organization's IP address range](../../media/3a6896f0-3a60-4ef7-91e1-7cf7f24a8bc4.png)

When you set these restrictions, all mail sent to your organization must be sent from a specific IP address range. Any internet email that does not originate from this IP address range will be rejected.

### Example 5: Require that all mail sent from your partner organization IP address or address range is encrypted using TLS
<a name="Example3"> </a>

**For New Exchange admin center**

1. Use all the settings configured in Example 1 from Steps 1 through 4.
2.  Click **Edit sent email identity**.
3. Select the **By verifying that the IP address of the sending server matches one of the following IP addresses, which belong to your partner organization** option.


<include an image - encryption-mail-sent-from-org.png>

4. Enter the IP address or IP address range apart from which email messages originating from, should not be accepted.
5. Click the plus icon next to the text box.
6. Click **Save**. A notification message **Connector updated successfully** is displayed.
7. Click **Edit restrictions**.
8. Select the following options:
    - **Reject email messages if they aren't sent over TLS**
9. Click **Save**. A notification message **Connector updated successfully** is displayed.

**For Classic Exchange admin center**
To identify your partner organization by IP address, use these options during setup:

![Choose the IP address to identify your partner organization](../../media/d5d54819-2e69-4f76-be37-ba701876beb6.png)

![Enter your partner organization's IP address](../../media/4ad3f410-e49b-4c92-82f5-8a8a6ab9535c.png)

Add the requirement for TLS encryption by using this setting:

![Choose TLS to encrypt email from partner organization](../../media/0de0e09c-8420-419f-87fc-cf66f10098ec.png)

When you set these restrictions, all mail from your partner organization sent from the IP address or address range you specify must be sent using TLS. Any mail that does not meet this restriction will be rejected.

## See also
<a name="examplesecurityrestrict"> </a>

[Configure mail flow using connectors in Microsoft 365 or Office 365](use-connectors-to-configure-mail-flow.md)

[Mail flow best practices for Exchange Online, Microsoft 365, and Office 365 (overview)](../mail-flow-best-practices.md)

[Validate connectors](validate-connectors.md)

[What happens when I have multiple connectors for the same scenario?](set-up-connectors-to-route-mail.md#what-happens-when-i-have-multiple-connectors-for-the-same-scenario)
