---
title: "Create an offline address book"
ms.author: chrisda
author: chrisda
manager: serdars
ms.date: 
ms.audience: ITPro
ms.topic: article
f1_keywords:
- 'Microsoft.Exchange.Management.SnapIn.Esm.OrganizationConfiguration.Mailbox.NewOabWizardForm.OabIntroductionWizardPage'
ms.service: exchange-online
localization_priority: Normal
ms.assetid: b57bb4ce-5b6e-4702-a2f8-04bf3898a861
description: "Admins can learn how to create offline address books (OABs) in Exchange Online."
---

# Create an offline address book

An offline address book (OAB) is a downloadable address list collection that Outlook users can access while disconnected from Exchange Online. An OAB allows Outlook users to access the information within the specified address lists while disconnected from Exchange Online. Admins can decide which address lists are made available to users who work offline.

For additional management tasks related to OABs, see [Offline address book procedures](offline-address-book-procedures.md).

## What do you need to know before you begin?

- Estimated time to complete: 5 minutes.

- You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Offline address books" entry in the [Email Address and Address Book Permissions](https://technet.microsoft.com/library/1c1de09d-16ef-4424-9bfb-eb7edffbc8c2.aspx) topic. 

- By default in Exchange Online, the Address List role isn't assigned to any role groups. To use any cmdlets that require the Address List role, you need to add the role to a role group. For more information, see the "Add a role to a role group" section in the topic, **Manage role groups**.

- You can't use the Exchange admin center (EAC) to perform this procedure. You can only use Exchange Online PowerShell. To connect to Exchange Online PowerShell, see [Connect to Exchange Online PowerShell](https://docs.microsoft.com/powershell/exchange/exchange-online/connect-to-exchange-online-powershell/connect-to-exchange-online-powershell).

> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at [Exchange Online](https://go.microsoft.com/fwlink/p/?linkId=267542) or [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkId=285351). 

## Use Exchange Online PowerShell to create an OAB with web-based distribution

This example creates an OAB named OAB_Contoso that contains the default global address list.

```
New-OfflineAddressBook -Name "OAB_Contoso" -AddressLists "\Default Global Address List"
```

For detailed syntax and parameter information, see [New-OfflineAddressBook](https://technet.microsoft.com/library/8b9a3931-90c3-4b36-9dcb-5e2e65cd7e5e.aspx).
