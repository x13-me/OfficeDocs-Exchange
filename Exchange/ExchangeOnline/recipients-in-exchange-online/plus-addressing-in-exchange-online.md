---
title: "Plus Addressing in Exchange Online"
ms.author: v-bshilpa
author: Benny-54
manager: Serdars
audience: ITPro
f1.keywords:
ms.topic: article
ms.service: exchange-online
localization_priority: Normal
search.appverid:
ms.collection:
ms.custom:
description: You use plus addressing to support dynamic, disposable recipient (not sender) email addresses in your Exchange Online organization.
---

# Plus Addressing in Exchange Online

From September 2020, plus addressing, also known as subaddressing, is available in Exchange Online. Subaddressing is defined as a way to support dynamically-created recipient (not sender) email addresses for mailboxes.

An SMTP email address uses the basic syntax: `<local-part>@<domain>`. For example, sean@contoso.com. 

Plus addressing uses the syntax: `<local-part>+<tag>@<domain>`. For example, sean+newsletter@contoso.com. 

The original email address must be valid; the `+tag` value that you add is arbitrary, although regular character restrictions for SMTP email addresses apply (for example, no spaces). For more information about using plus addresses, see **Using plus addresses**.

By default, plus addressing support is disabled in Exchange Online. Since Exchange Online has always supported regular email addresses that already contain the plus sign, if you enable plus addressing, these email addresses might stop working. See the note below in **Enable plus addressing in your Exchange Online organization**.

You can't enable plus addressing in the Exchange admin center (EAC); you can only enable it through Exchange Online PowerShell. 

>[!NOTE]
> Currently, plus addresses are only supported for mailboxes but support for Groups and DLs is being rolled out and will be available by the end of December 2020. 

## Enable plus addressing in your Exchange Online organization

1. [Connect to Exchange Online PowerShell](https://docs.microsoft.com/powershell/exchange/connect-to-exchange-online-powershell?view=exchange-ps).

2. The command uses the following syntax:

   ```PowerShell
   Set-OrganizationConfig -AllowPlusAddressInRecipients <$true | $false>
   ```

3. To enable plus addressing in your organization, run the following command:

   ```PowerShell
   Set-OrganizationConfig -AllowPlusAddressInRecipients $true
   ```

> [!NOTE]
> This feature was rolled out behind a setting because, historically, customers have been able to use plusses in addresses for mailboxes in Exchange Online and on-premises servers. When this feature is enabled, Exchange Online will first check if the full address can resolve to a mailbox that the service is aware of. It is only when that resolution fails, that a plus is looked for and a second attempt to resolve the address without the plus and tag is done. This means that the feature is compatible with addresses containing plusses that Exchange Online knows about. If you relay messages to a mailbox on-premises that does not resolve in Exchange Online, message delivery will be affected. The messages will be parsed and addressed to the parsed address e.g. sean@contoso.com instead of the full sean+newsletter@contoso.com, using the example above.  

## Using plus addresses

You can create new plus addresses by adding a new tag. You can use plus addresses as unique addresses for services that you sign up for. 

> [!NOTE]
> Some web forms don't support plus signs in email addresses. If you have subscribed to some email list subscription services using an SMTP email address, and you need to unsubscribe from them, you must use the email address that you subscribed with. You cannot unsubscribe by sending emails with plus addresses. You also cannot unsubscribe from some email subscriptions using unsubscribe email messages with plus addresses if you have subscribed to them. 

As plus addresses are not aliases that are configured on the mailbox, they don't resolve to a user's name in Outlook clients. This results in plus addresses being easily identifiable in the `To` or `CC` fields of messages. However, there might be scenarios where you can't use a plus address for a Microsoft service that needs to be associated with your mailbox.

To automatically identify and filter email messages that are sent to plus addresses, use Inbox rules to act on those messages. Using the condition *Recipient address includes*, you can specify an action for messages sent to a particular plus address, such as moving the messages to a folder.

## Related article

[Add or remove email addresses for a mailbox](https://docs.microsoft.com/Exchange/recipients-in-exchange-online/manage-user-mailboxes/add-or-remove-email-addresses)
