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
> Setting up a connector to exchange mail with a partner organization is optional; mail flows to and from your partner organization occur without connectors.

If you use a third-party cloud service for email filtering and need instructions for making this work with Microsoft 365 or Office 365, see [Mail flow best practices for Exchange Online and Microsoft 365 or Office 365 (overview)](../../mail-flow-best-practices/mail-flow-best-practices.md).

## Using connectors to exchange email with a partner organization

By default, Microsoft 365 or Office 365 sends mails using TLS encryption, provided that the destination server also supports TLS. If your partner organization supports TLS, you only need to create a connector if you want to enforce certain security restrictions - for example, you always want TLS applied, or you require certificate verification whenever mail is sent from your partner to your organization.

> [!NOTE]
> For information about TLS, see [How Exchange Online uses TLS to secure email connections](https://docs.microsoft.com/microsoft-365/compliance/exchange-online-uses-tls-to-secure-email-connections) and for detailed technical information about how Exchange Online uses TLS with cipher suite ordering, see [Enhancing mail flow security for Exchange Online](https://www.microsoft.com/microsoft-365/blog/2015/06/29/enhancing-mail-flow-security-for-exchange-online/).

When you set up a connector, email messages are checked to ensure they meet the security restrictions that you specify. If email messages don't meet the security restrictions that you specify, the connector rejects them, and those messages will not be delivered. This behavior of the connector makes it possible to set up a secure communication channel with a partner organization.

You can set up one or both of the following, depending on your requirements:

- [Set up a connector to apply security restrictions to mail sent from Microsoft 365 or Office 365 to your partner organization](#set-up-a-connector-to-apply-security-restrictions-to-mail-sent-from-microsoft-365-or-office-365-to-your-partner-organization)

- [Set up a connector to apply security restrictions to mail sent from your partner organization to Microsoft 365 or Office 365](#set-up-a-connector-to-apply-security-restrictions-to-mail-sent-from-your-partner-organization-to-microsoft-365-or-office-365)

Also in this article:

- [Change a connector that Microsoft 365 or Office 365 is using for mail flow](#change-a-connector-that-microsoft-365-or-office-365-is-using-for-mail-flow)

- [Example security restrictions you can apply to email sent from a partner organization](#example-security-restrictions-you-can-apply-to-email-sent-from-a-partner-organization)

Review this section to help you determine the specific settings you need for your business.

## Set up a connector to apply security restrictions to mail sent from Microsoft 365 or Office 365 to your partner organization
<a name="setupaconnectortopartner"> </a>
This section describes the process of setting up a connector in both the New Exchange admin center (EAC) and the Classic EAC. Before you set up a new connector, do the following:

- Check for any connectors that are already listed here for your organization. For example, if you already have a connector set up for a partner organization, you'll see it listed. Ensure you don't create duplicate connectors for a single organizational partner; when this happens, it can cause errors, and your mail might not be delivered.

If any connectors already exist for your organization, you can see them listed here, as shown in the below screenshots for New EAC and Classic EAC, respectively.

:::image type="content" source="../../media/new-exchange-admin-center.png" alt-text="Existing list of connectors"::: 

![Microsoft 365 and Office 365 connectors partner organization examples](../../media/9e8f0035-24b6-4d62-aecf-17f740530e31.png)

- Navigate to the new EAC from the Microsoft 365 admin center by clicking **Exchange** under the **Admin centers** pane.

Below are the procedures to set up a new connector.

### For New EAC

1. Navigate to **Mail flow > Connectors**. The **Connectors** screen appears.

2. Click **+Add a connector**. The **New connector** screen appears, as shown in the following screenshot:

:::image type="content" source="../../media/office-365-to-partner.png" alt-text="The screen on which a connector for Office 365 is added":::

3. Configure the following settings:

    a. Under **Connection from**, choose **Office 365**.
    
    b. Under **Connection to**, choose **Partner Organization**.
  
4. Click **Next**. The **Connector name** screen appears.

5. Provide a name for the connector and click **Next**. The **Use of connector** screen appears.

6. Choose any one of the two options and click **Next**. The **Routing** screen appears.

> [!NOTE]
> If you choose the second option, provide the name of any one of the domains that are part of your organization. If there is only one domain for your organization, enter its name.

7. Choose any of the two options and click **Next**. The **Security restrictions** screen appears.

> [!NOTE]
> If you choose the first option, you need not mention the details of smart host. If you choose second option, enter the domain name of the smart host in the text box.

8. Configure the following settings:

- Choose **Always use Transport Layer Security (TLS) to secure the connection (recommended)**.

> [!NOTE]
> It is not mandatory to configure the Transport Layer Security (TLS) settings on the **Security restrictions** page. You can navigate to the next screen without choosing anything on this screen. The need to define TLS settings on this page depends on whether the destination server supports TLS or not.

- Choose one of the options under **Connect only if the recipient's email server certificate matches this criteria**.

> [!NOTE]
> If you are choosing the **Issue by a trusted certificate authority (CA)** option, the **Add the subject name or subject alternative name (SAN) matches this domain name** option is activated.
>  
> It is optional to choose the **Add the subject name or subject alternative name (SAN) matches this domain name** option. However, if you choose it, you must enter the domain name to which the certificate name matches.

9. Click **Next**. The **Validation email** screen appears.

10. Provide an email address that is part of the mailbox in your organization's email server, and click **+**

11. Click **Validate**. The validation process starts.

12. Once the validation process is completed, click **Next**. The **Review connector** screen appears.

13. Review the settings you have configured and click **Create connector**.

The connector is created.

> [!NOTE]
> If you need more information about the setup, click the **Help** or **Learn More** links.

14. At the end, ensure your connector validates. If the connector does not validate, see [Validate connectors](https://docs.microsoft.com/exchange/mail-flow-best-practices/use-connectors-to-configure-mail-flow/validate-connectors) for help resolving issues.

### For Classic EAC

Navigate to the Classic EAC portal by clicking **Classic Exchange admin center**. Select **mail flow** and then **connectors**.

To start the wizard, click the plus symbol **+**. On the first screen, choose the options that are depicted in the following screenshot:

![Microsoft 365 and Office 365 to partner organization connector options](../../media/93cb9e70-f8d8-4e63-bb92-caafd8b79ad7.png)

Click **Next**, and follow the instructions in the wizard. Click the **Help** or **Learn More** links if you need more information. The wizard will guide you through setup. At the end, ensure your connector validates. If the connector does not validate, see [Validate connectors](validate-connectors.md) for help resolving issues.

If you want to create a secure channel with your partner organization in both directions, set up a connector that restricts mail flow from your partner organization to Microsoft 365 or Office 365.

## Set up a connector to apply security restrictions to mail sent from your partner organization to Microsoft 365 or Office 365
<a name="setupconnectorfrompartner"> </a>

You can set up a connector to apply security restrictions to email that your partner organization sends to you. The procedure to set up a connector is described below.

### For New EAC

1. Navigate to **Mail flow > Connectors**. The **Connectors** screen appears.

2. Click **+Add a connector**. The **New conenctor** screen appears, as shown in the following screenshot.

:::image type="content" source="../../media/home-screen-to-add-a-new-connector.png" alt-text="The screen on which the process to create a connector begins":::

3. Select the **Partner organization** radio button under **Connection from**.

> [!NOTE]
> Once you select the **Partner organization** radio button under **Connection from**, the option under **Connection to** is greyed out, implying that **Office 365** is chosen by default.

:::image type="content" source="../../media/partner-to-365-new-eac.png" alt-text="The screen on which a connector is set up to apply security restrictions":::

4. Click **Next**. The **Connector name** screen appears, as shown in the following screenshot:

:::image type="content" source="../../media/providing-name-to-connector.png" alt-text="The screen on which the connector is given a name":::

5. Provide a name for the connector and click **Next**. The **Authenticating sent email** screen appears.

6. Choose one of the two options.

> [!NOTE]
> If you choose the first option, you can provide the name of any one domain from the list of domains for your organization. If you have only one domain for your organization, enter its name.
> If you choose the second option, provide an IP address of any of the recipients who are part of your organization's mailbox.

:::image type="content" source="../../media/screen-for-365-to-identify-partner-org.png" alt-text="The screen on which the partner organization is identified by domain name":::

7. Click **Next**. The **Security restrictions** screen appears.

8. Choose **Reject email messages if they aren't sent over TLS**.

> [!NOTE]
> It is optional to choose the option of **And require that the subject name of the certificate that the partner uses to authenticate with Office 365 matches this domain name**. If you choose this option, enter the domain name of the partner organization.

:::image type="content" source="../../media/security-restrictions-screen.png" alt-text="The screen on which settings that define security restrictions are set":::

9. Check the **Reject email messages if they aren't sent from within this IP address range** check box, and provide the IP address range, as shown in the following screenshot.

> [!IMPORTANT]
>You can choose this option in addition to the option specified in Step 5; Else, you can choose either this option or the one in Step 5. Choosing at least one of these options is mandatory.

:::image type="content" source="../../media/defining-ip-address-range.png" alt-text="The screen on which the sender's ID address is defined as a criteria":::

10. Click **Next**. The **Review connector** screen appears.

11. Review the settings you have configured and click **Create connector**.

:::image type="content" source="../../media/creating-a-connector.png" alt-text="The screen on which the connector creation process is completed":::

The connector is created.

> [!NOTE]
> If you need more information, you can click the **Help** or **Learn More** links. In particular, see [Identifying email from your email server](https://docs.microsoft.com/previous-versions/exchange-server/exchange-150/dn910993(v=exchg.150)) for help in configuring certificate or IP address settings for this connector. The wizard will guide you through the setup.

### For Classic EAC

To start the wizard, click the plus symbol **+**. On the first screen, choose the following options:

![Connector from partner organization to Microsoft 365 or Office 365](../../media/e6d15001-989b-48b3-a848-427b800c2a70.png)

Click **Next**, and follow the instructions in the wizard. Click the **Help** or **Learn More** links if you need more information. The wizard will guide you through setup. At the end, save your connector.

Ask your partner organization to send a test email. Ensure the email your partner organization sends will cause the connector to be applied. For example, if you specified security restrictions for mail sent from a specific partner domain, ensure they send test mail from that domain. Check that the test email is delivered to confirm that the connector works correctly.

## Change a connector that Microsoft 365 or Office 365 is using for mail flow
<a name="Changeaconnector"> </a>

To change settings for a connector, perform the procedures specified below.

Select the connector you want to edit and then click the **Edit** icon, as shown in the following two screens for New EAC and Classis EAC, respectively.

:::image type="content" source="../../media/connector-editing-screen-new-eac.png" alt-text="The screen on which the connector settings can be edited":::

![Shows a screen shot with a connector selected and the edit (pencil) icon highlighted.](../../media/9654b36f-40d2-4791-ae5c-ce3afd9bb683.png)

The connector wizard opens, and you can make changes to the existing connector settings. While you change the connector settings, Microsoft 365 or Office 365 continues to use the existing connector settings for mail flow. When you save changes to the connector, Microsoft 365 or Office 365 starts using the new settings.

## Example security restrictions you can apply to email sent from a partner organization
<a name="examplesecurityrestrict"> </a>

Review these connector examples to help you decide whether you want to apply security restrictions to emails sent by a partner organization, and understand what settings will meet your business needs:

### Create a partner organization connector

**For New EAC**

For details on this procedure, see The **For New EAC** subsection in the **Set up a connector to apply security restrictions to mail sent from your partner organization to Microsoft 365 or Office 365** section in this topic.

**For Classic EAC**

From the new EAC portal, navigate to the Classic EAC portal by clicking **Classic Exchange admin center**. Select **mail flow** and then **connectors**.

To start the wizard, click the plus symbol **+**. To create a connector for email you receive from a partner organization, use the options depicted in the following screenshot:

![Connector from partner organization to Microsoft 365 or Office 365](../../media/e6d15001-989b-48b3-a848-427b800c2a70.png)

Once you choose this mail flow scenario, you can set up a connector that will apply security restrictions to emails that your partner organization sends to you. For some security restrictions, you might need to talk to your partner organization to obtain information to complete some settings. Look for the examples that best meet your needs to help you set up your partner connector.

> [!NOTE]
> Any email sent from your partner organization which does not meet security restrictions that you specify will not be delivered.

### Example 1: Require that email sent from your partner organization domain contosobank.com is encrypted using transport layer security (TLS)
<a name="example1"> </a>

To do this, specify your partner organization domain name to identify mail from that partner, and then choose transport layer security (TLS) encryption when you create the connector for mail flow from your partner to Microsoft 365 or Office 365. 

During setup of the connector in the New EAC, use the options as shown in the following screenshots:

:::image type="content" source="../../media/connector-partner-to-365-encryption-tls.png" alt-text="The screen on which TLS encryption is done":::

Use this screen to enter your partner organization's domain name(s) so the connector can identify mail sent by your partner:

:::image type="content" source="../../media/domain-name-partner-to-365-encryption-tls.png" alt-text="The screen on which the domain name is set":::

Choose this setting to require encryption for all email from ContosoBank.com using TLS:

:::image type="content" source="../../media/requiring-tls-encryption.png" alt-text="YThe screen on which the mandatory TLS encryption is configured":::

During setup of the connector in the Classic EAC, use the options as shown in the following screenshots:

![Choose to use the sender's domain name](../../media/3b3b0cc6-3928-4cab-a022-436821f9d559.png)

Use this screen to enter your partner organization's domain name(s) so the connector can identify mail sent by your partner:

![Add partner organization domain name](../../media/6ea7db5c-71ff-41cb-bfcd-89be4106f7e1.png)

Choose this setting to require encryption for all email from ContosoBank.com using TLS:

![Choose TLS to encrypt email from partner organization](../../media/0de0e09c-8420-419f-87fc-cf66f10098ec.png)

When you choose these settings, all emails from your partner organization's domain, ContosoBank.com, must be encrypted using TLS. Any mail that is not encrypted will be rejected.

### Example 2: Require that email sent from your partner organization domain ContosoBank.com is encrypted and uses their domain certificate
<a name="example1"> </a>

To do this in the New EAC, perform the following steps:

1. Use all the settings shown in **Example 1** above. 

2. Add the certificate domain name that your partner organization uses to connect with Microsoft 365 or Office 365, as shown in the screenshot below.

:::image type="content" source="../../media/encryption-using-certificate-new-eac.png" alt-text="The screen on which encryption is done using the domain certificate name":::

To do this in the Classic EAC

1. Use all the settings shown in **Example 1** above.

2. Add the certificate domain name that your partner organization uses to connect with Microsoft 365 or Office 365, as shown in the screenshot below.

![Enter your partner organization certificate name](../../media/46229d66-dcfd-4e3d-bc12-9f53a5572f81.png)

When you set these restrictions, all mail from your partner organization domain must be encrypted using TLS, and sent from a server with the certificate name you specify. Any email that does not meet these conditions will be rejected.

### Example 3: Require that all emails are sent from a specific IP address range
<a name="Example3"> </a>

This email could be from a partner organization, such as ContosoBank.com, or from your on-premises environment. For instance, the MX record for your domain, contoso.com, points to on-premises, and you want all emails being sent to contoso.com to come from your on-premises IP addresses only. This helps prevent spoofing and ensures your compliance policies can be enforced for all messages.

To do this, specify your partner organization domain name to identify mail from that partner, and then restrict the IP addresses that you accept mail from. Using an IP address makes the connector more specific because it identifies a single address or an address range that your partner organization sends mails from. 

In the New EAC, the procedure is as described below:

1. Enter your partner domain as described in **Example 1** above.
2. Use the options as shown in the screenshot below.

:::image type="content" source="../../media/receive-email-from-specific-ip-address.png" alt-text="The screen on which email source IP address is set":::

In the Classic EAC, the procedure is as described below:

1. Enter your partner domain as described in **Example 1** above.
2. Use the options as shown in the screenshot below.

![Enter your partner organization's IP address range](../../media/3a6896f0-3a60-4ef7-91e1-7cf7f24a8bc4.png)

When you set these restrictions, all emails that are sent from your partner organization domain, ContosoBank.com, or from your on-premises environment will be from the IP address or an address range you specify. Any mail that does not meet these conditions will be rejected.

### Example 4: Require that all email sent to your organization from the internet is sent from a specific IP address (third-party email service scenario)
<a name="Example3"> </a>

Mail flow from a third-party email service to Microsoft 365 or Office 365 works without a connector. However, in this scenario, you can optionally use a connector to restrict all mail delivery to your organization. If you use the settings described in this example, they will apply to *all email sent to your organization*. When all emails sent to your organization comes from a single third-party email service, you can optionally use a connector to restrict all mail delivery; only mail sent from a single IP address or address range will be delivered.

> [!NOTE]
> Ensure you identify the full range of IP addresses that your third-party email service sends mail from. If you miss an IP address, or if one gets added without your knowledge, some mails will not be delivered to your organization.

In the New EAC, to restrict all mails sent to your organization from a specific IP address or address range, use the options during setup as shown in the following screenshots:

:::image type="content" source="../../media/specific-internet-ip-address.png" alt-text="The screen on which there is a configuration to apply the settings globally":::

:::image type="content" source="../../media/configuring-receipt-from-specific-ip-address.png" alt-text="The screen on which the your partner organization's IP address range is defined":::

In the Classic EAC, to restrict all mails sent to your organization from a specific IP address or address range, use the options during setup as shown in the following screenshots:

![Choose to use the sender's domain name](../../media/3b3b0cc6-3928-4cab-a022-436821f9d559.png)

![Enter "\*" to apply settings to all sender domains](../../media/1be173e2-1c57-4d5d-9bb7-f353c1c29e1f.png)

![Enter your partner organization's IP address range](../../media/3a6896f0-3a60-4ef7-91e1-7cf7f24a8bc4.png)

When you set these restrictions, all mails sent to your organization will be from a specific IP address range. Any internet email that does not originate from this IP address range will be rejected.

### Example 5: Require that all mail sent from your partner organization IP address or address range is encrypted using TLS
<a name="Example3"> </a>

To identify your partner organization by IP address, in the New EAC, use these options during setup:

:::image type="content" source="../../media/identify-partner-by-ip-address.png" alt-text="The screen on which the mails by partner organization are identified by IP address of the sender":::

Add the requirement for TLS encryption by using this setting:

:::image type="content" source="../../media/configuring-receipt-from-specific-ip-address.png" alt-text="The screen on which IP addresses by which Partner organization will be identified is set":::

To identify your partner organization by IP address, in the Classic EAC, use these options during setup:

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
