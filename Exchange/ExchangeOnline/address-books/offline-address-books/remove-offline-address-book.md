---
title: "Remove an offline address book from Exchange "
ms.author: chrisda
author: chrisda
manager: serdars
ms.date: 
ms.audience: ITPro
ms.topic: article
ms.service: exchange-online
localization_priority: Normal
ms.assetid: d69f1e8a-b3cb-4739-90cd-85ea450d06f3
description: "Admins can learn how to remove offline address book (OAB) from Exchange Online."
---

# Remove an offline address book

This topic explains how to remove an offline address book (OAB) from Exchange Online. If you remove the default OAB, you must assign a different OAB as the default OAB. For instructions about how to change the default OAB, see [Change the default offline address book](change-default-offline-address-book.md).

For additional management tasks related to OABs, see [Offline address book procedures](offline-address-book-procedures.md).

## What do you need to know before you begin?

- Estimated time to complete each procedure: 5 minutes.

- You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Offline address books" entry in the [Email Address and Address Book Permissions](https://technet.microsoft.com/library/1c1de09d-16ef-4424-9bfb-eb7edffbc8c2.aspx) topic. 

- By default in Exchange Online, the Address List role isn't assigned to any role groups. To use any cmdlets that require the Address List role, you need to add the role to a role group. For more information, see the "Add a role to a role group" section in the topic, **Manage role groups**.

- You can't use the Exchange admin center (EAC) to perform this procedure. You can only use Exchange Online PowerShell. To connect to Exchange Online PowerShell, see [Connect to Exchange Online PowerShell](https://docs.microsoft.com/powershell/exchange/exchange-online/connect-to-exchange-online-powershell/connect-to-exchange-online-powershell).

> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at [Exchange Online](https://go.microsoft.com/fwlink/p/?linkId=267542) or [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkId=285351). 

## Use Exchange Online PowerShell to remove an OAB

This example removes an OAB named My OAB.

```
Remove-OfflineAddressBook -Identity "My OAB"
```

For detailed syntax and parameter information, see [Remove-OfflineAddressBook](https://technet.microsoft.com/library/88a8f173-34b9-4e75-8f1a-26ad6f972e98.aspx).


## How do you know this worked?

To verify that you've successfully removed the OAB, run the following command to verify that the OAB is gone.

```
Get-OfflineAddressBook
```
