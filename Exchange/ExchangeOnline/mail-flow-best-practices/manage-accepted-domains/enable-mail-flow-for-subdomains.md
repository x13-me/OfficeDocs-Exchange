---
localization_priority: Normal
description: Admins can learn how to enable mail flow for subdomains in Exchange Online.
ms.topic: article
author: msdmaguire
ms.author: jhendr
ms.assetid: 4033a30a-f506-481c-8ef0-fd9a0508ae38
ms.reviewer: 
title: Enable mail flow for subdomains in Exchange Online
ms.collection: 
- exchange-online
- M365-email-calendar
audience: ITPro
f1.keywords:
- NOCSH
ms.service: exchange-online
manager: serdars

---

# Enable mail flow for subdomains in Exchange Online

If you have a hybrid environment, with mailboxes hosted both in Exchange Online and on-premises Exchange, and you have subdomains of the accepted domains that only exist in your on-premises environment, you can enable email flow to and from these on-premises subdomains. For example, if you have an accepted domain called Contoso.com, and you enable match subdomains, users can send email to, or receive email from all subdomains of Contoso.com that exist in your on-premises environment, such as marketing.contoso.com and nwregion.contoso.com. In Microsoft Forefront Online Protection for Exchange (FOPE), this feature was called _catch-all domains_.

> [!IMPORTANT]
> - If you have a limited number of subdomains, and know all the subdomain names, we recommend setting up each subdomain as an accepted domain in the Microsoft 365 admin center, instead of using the procedures in this topic. By setting up each subdomain separately, you can have finer control over mail flow and can include unique mail flow rules (also known transport rules) for each subdomain. For more information about adding a domain in the Microsoft 365 admin center, see [Add a domain to Microsoft 365](/microsoft-365/admin/setup/add-domain).
>
> - In order to enable match subdomains, an accepted domain must be set up as an internal relay domain. For information about setting the domain type to internal relay, see [Manage accepted domains in Exchange Online](manage-accepted-domains.md).
>
> - After you enable match subdomains, in order for the service to deliver mail for all subdomains to your organization's email server (outside Microsoft 365 or Office 365), you must also change the connector that originates from Office 365 to your organization. For instructions, see [Use the EAC to add the domain to connector that originates from Office 365 to your organization](#use-the-eac-to-add-the-domain-to-connector-that-originates-from-office-365-to-your-organization).

## What do you need to know before you begin?

- Estimated time to complete: 5 minutes

- You need permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Domains" entry in the [Feature permissions in Exchange Online](../../permissions-exo/feature-permissions.md) topic.

- To open the Exchange admin center (EAC), see [Exchange admin center in Exchange Online](../../exchange-admin-center.md). To connect to Exchange Online PowerShell, see [Connect to Exchange Online PowerShell](/powershell/exchange/connect-to-exchange-online-powershell).

- For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts for the Exchange admin center](../../accessibility/keyboard-shortcuts-in-admin-center.md).

> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at [Exchange Online](https://social.technet.microsoft.com/forums/msonline/home?forum=onlineservicesexchange) or [Exchange Online Protection](https://social.technet.microsoft.com/forums/forefront/home?forum=FOPE).

## Use the Exchange admin center (EAC) to set up match-subdomains on a domain

### New EAC

1. Navigate to **Mail Flow** \> **Accepted domains**. The **Accepted domains** screen appears.

:::image type="content" source="../../media/accepted-domains.png" alt-text="The screen displaying accepted domains":::

2. Select an accepted domain and click it. The accepted domain's details screen appears.

3. Verify that **Internal Relay** is selected. If **Authoritative** is selected, change it to **Internal Relay**.

:::image type="content" source="../../media/setting-internal-relay.png" alt-text="The screen on which the INTERNAL RELAY option is chosen":::

4. Check the check box for **Accept mail for all subdomains**.

:::image type="content" source="../../media/setting-email-acceptance-for-all-subdomains.png" alt-text="The screen on which the user configures acceptance of emails from all subdomains":::

5. Click **Save**.

The accepted domain is updated successfully.

### Classic EAC

1. Navigate to **Mail Flow** \> **Accepted domains**, and select the domain.
The domain details dialog box is displayed.

2. In the Details pane, Verify that **Internal Relay** is selected.

:::image type="content" source="../../media/choosing-internal-relay-old-eac.png" alt-text="The screen on which it is ensured that Internal Relay type is chosen":::

3. Select **Accept mail for all subdomains**.

:::image type="content" source="../../media/configuring-subdomains-to-send-receive-mails.png" alt-text="The screen on which all subdomains are set such that they can send and receive emails":::

## Use the EAC to add the domain to connector that originates from Office 365 to your organization

### New EAC

1. Navigate to **Mail Flow** \> **Connectors**.

2. Select a connector that originates from Office 365 to your organization's email server, and click it.

The connector properties screen appears.

3. Under **Use of connector**, click **Edit use**. The **Use of connector** screen appears.

4. Click the radio button for **Only when email messages are sent to these domains**.

:::image type="content" source="../../media/determining-timing-of-connector-new-eac.png" alt-text="The option on the New EAC screen to choose when the connector can be used":::

5. In the text box, enter the name of the domain to which you want to apply the connector. For example, ***.contoso.com**.

6. Click **+**.

7. Click **Next**. The **Validation email** screen appears.

8. In the text box, enter the email of an active mailbox on your organization's server.

9. Click **+**.

10. Click **Validate**. The validation process starts.

11. Once the validation process is completed, click **Save**.

### Classic EAC

1. Navigate to **Mail Flow** \> **Connectors**.

2. Select a connector that originates from Office 365 to your organization's email server.
 
3. Click the "Edit" icon ![Edit icon](../../media/ITPro_EAC_EditIcon.png). The **Edit Connector** screen appears.

4. Click **Next**. The **When do you want to use this connector** section appears.

5. Select the radio button for **Only when email messages are sent to these domains**.

:::image type="content" source="../../media/determining-timing-of-connector-old-eac.png" alt-text="The option on the Classic EAC screen to choose when the connector can be used":::

6. Click the "Add" icon ![Add Icon](../../media/ITPro_EAC_AddIcon.png). The **add domain** screen appears.

7. In the text box, enter the name of the domain to which you want to apply the connector. For example, \*.contoso.com.

8. Click **OK**. The **Edit Connector** screen reappears. The value *.contoso.com is listed in the text field.

9. Click **Next** and navigate through the other screens in the wizard.

10.  Click **Save** on the last screen.

## Use Exchange Online PowerShell to set up match-subdomains on a domain

To add the match subdomains to a domain that is set up as an internal relay, use this syntax:

```powershell
Set-AcceptedDomain -Identity <Domain Name> -MatchSubdomains $true
```

This example sets up match subdomains for the contoso.com domain.

```powershell
Set-AcceptedDomain -Identity contoso.com -MatchSubdomains $true
```

For detailed syntax and parameter information, see [Set-AcceptedDomain](/powershell/module/exchange/set-accepteddomain).