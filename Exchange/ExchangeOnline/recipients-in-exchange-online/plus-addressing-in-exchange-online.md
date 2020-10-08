---
title: "Plus Addressing in Exchange Online"
ms.author: v-bshilpa
author: Benny Shilpa
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

In September 2020, support for plus addressing, also known as subaddressing, was added to Exchange Online. Subaddressing is defined as a way to support dynamic, disposable recipient (not sender) email addresses for mailboxes.

An SMTP email address uses the basic syntax: <local-part>@<domain>. For example, sean@contoso.com. Plus addressing uses the syntax: <local-part>+<tag>@<domain>. For example, sean+newsletter@contoso.com. The original email address must be valid; the +tag value that you add is arbitrary, although regular character restrictions for SMTP email addresses apply (for example, no spaces). For more information about using plus addresses, see the Using plus addresses section later in this topic.

Plus addressing is already available in Outlook.com. By default, plus addressing support is disabled in Exchange Online, because Exchange has always supported regular email addresses that contain the plus sign. If you already use plus signs in email addresses, and you enable plus addressing, these email address might stop working.

Follow the instructions in this topic to enable plus addressing in Exchange Online. You can’t enable plus addressing in the Exchange admin center (EAC); you can only use Exchange Online PowerShell. If your organization’s emails are routed through Exchange Online to your on-premises servers, mailboxes hosted on-premises will also be able to use plus addresses.  

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

## Using plus addresses

You create new plus addresses simply by thinking up a new tag. You can use plus addresses as unique addresses for services that you sign up for. Note that some web forms don’t support plus signs in email addresses. Also note that some email list subscription services require you to send unsubscribe requests from the email address that you subscribed with. Because you can’t send email messages from plus addresses, you can’t unsubscribe using that method.

Because plus addresses are not aliases that are configured on the mailbox, they don’t resolve to a user's name in Outlook clients. This results in plus addresses being easily identifiable in the To or CC fields of messages. However, there might be scenarios where you can’t use a plus address for a Microsoft service that needs to be associated with your mailbox.

To automatically identify and filter email messages that are sent to plus addresses, use Inbox rules to act on those messages. Using the condition *Recipient address includes*, you can specify an action for messages sent to a particular plus address, such as moving the messages to a folder.



