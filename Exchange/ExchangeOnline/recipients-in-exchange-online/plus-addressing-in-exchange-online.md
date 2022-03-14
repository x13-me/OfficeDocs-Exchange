---
title: Plus Addressing in Exchange Online
ms.author: v-bshilpa
author: Benny-54
manager: Serdars
audience: ITPro
f1.keywords:
ms.topic: article
ms.service: exchange-online
ms.localizationpriority: medium
search.appverid:
ms.collection:
ms.custom:
description: You use plus addressing to support dynamic, disposable recipient (not sender) email addresses in your Exchange Online organization.
---

# Plus Addressing in Exchange Online

> [!NOTE]
> A change is coming to make plus addressing enabled by default. This change is planned for late April 2022. When the change occurs, the allow setting AllowPlusAddressInRecipients below will not longer work. Customers who do not want to allow their users to use plus addressing, can disable the feature with a new setting which has been documented below.    

From September 2020, plus addressing, also known as subaddressing, is available in Exchange Online. Subaddressing is a defined way to support dynamic, disposable recipient (not sender) email addresses for mailboxes.

An SMTP email address uses the basic syntax: `<local-part>@<domain>`. For example, sean@contoso.com. 

Plus addressing uses the syntax: `<local-part>+<tag>@<domain>`. For example, sean+newsletter@contoso.com. 

The original email address must be valid; the `+tag` value that you add is arbitrary, although regular character restrictions for SMTP email addresses apply (for example, no spaces). For more information about using plus addresses, see **Using plus addresses**.

Plus addressing is available in [Outlook](https://outlook.live.com/owa/). By default, plus addressing support is disabled in Exchange Online. Since Exchange Online has always supported regular email addresses that already contain the plus sign, if you enable plus addressing, these email addresses might stop working.

If your organization's email is routed through Exchange Online to your on-premises servers, mailboxes hosted on-premises will also be able to use plus addresses.  

## Use PowerShell to disable plus addressing (New Setting)

1. [Connect to Exchange Online PowerShell](/powershell/exchange/connect-to-exchange-online-powershell).

2. The command uses the following syntax:

   ```PowerShell
   Set-OrganizationConfig -DisablePlusAddressingInRecipients <$true | $false>
   ```

3. To disable plus addressing in your organization, run the following command:

   ```PowerShell
   Set-OrganizationConfig -DisablePlusAddressInRecipients $true
   ```
   
4. This setting will only take effect when plus addressing is turned on by default. That change should roll out in late April. Before then, customers just need to ensure the setting AllowPlusAddressInRecipients below is not set to True for plus addressing to be disabled. 

## Use the new Exchange admin center to enable plus addressing (Setting to be deprecation)

1. In the new [Exchange admin center](https://admin.exchange.microsoft.com), go to **Settings** \> **Mail flow**.

2. Select **Turn on plus addressing for your organization**, and then select **Save**.

## Use PowerShell to enable plus addressing

1. [Connect to Exchange Online PowerShell](/powershell/exchange/connect-to-exchange-online-powershell).

2. The command uses the following syntax:

   ```PowerShell
   Set-OrganizationConfig -AllowPlusAddressInRecipients <$true | $false>
   ```

3. To enable plus addressing in your organization, run the following command:

   ```PowerShell
   Set-OrganizationConfig -AllowPlusAddressInRecipients $true
   ```


> [!NOTE]
> This feature was rolled out behind a setting because, historically, customers have been able to use plusses in addresses for mailboxes in Exchange Online and on-premises servers. When this feature is enabled, Exchange Online will first check if the full address can resolve to a mailbox that the service is aware of. It is only when that resolution fails, that a plus is looked for and a second attempt to resolve the address without the plus and tag is done. This means that the feature is compatible with addresses containing plusses that Exchange Online knows about. If you relay messages to a mailbox on-premises that does not resolve in Exchange Online, message delivery will be affected. The messages will be parsed and addressed to the parsed address for example, sean@contoso.com instead of the full sean+newsletter@contoso.com, using the example above.  

## Using plus addresses

You can create new plus addresses by adding a new tag. You can use plus addresses as unique addresses for services that you sign up for. 

> [!NOTE]
>
> Some web forms don't support plus signs in email addresses.
>
> If you need to unsubscribe from an email list subscription service, some subscription services require that you use the original email address that you subscribed with. You can't unsubscribe by sending an email from a plus address.

As plus addresses are not aliases that are configured on the mailbox, they don't resolve to a user's name in Outlook clients. This limitation results in plus addresses being easily identifiable in the `To` or `CC` fields of messages. However, there might be scenarios where you can't use a plus address for a Microsoft service that needs to be associated with your mailbox.

To automatically identify and filter email messages that are sent to plus addresses, use Inbox rules to act on those messages. Using the condition *Recipient address includes*, you can specify an action for messages sent to a particular plus address, such as moving the messages to a folder.
