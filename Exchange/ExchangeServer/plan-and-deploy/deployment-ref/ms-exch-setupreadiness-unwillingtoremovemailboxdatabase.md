---
title: "Cannot remove mailbox database [UnwillingToRemoveMailboxDatabase]"
ms.author: dstrome
author: dstrome
manager: serdars
ms.date: 7/22/2015
ms.audience: ITPro
ms.topic: reference
f1_keywords:
- 'ms.exch.setupreadiness.UnwillingToRemoveMailboxDatabase'
ms.prod: exchange-server-it-pro
localization_priority: Normal
ms.assetid: 5881e4c0-c2e2-48db-84b4-7f9ce3cf46a7
description: "Microsoft Exchange Server 2016 Setup can't continue because it can't remove a user mailbox database from the local server without incurring potential data loss."
---

# Cannot remove mailbox database [UnwillingToRemoveMailboxDatabase]

Microsoft Exchange Server 2016 Setup can't continue because it can't remove a user mailbox database from the local server without incurring potential data loss.
  
 Exchange 2016 Setup determines whether all mailbox databases have been removed from the server before the Mailbox server role is removed. However, user mailboxes might still remain on the server.
  
To resolve this issue, move any mailboxes on the server to another Exchange server or, if the mailboxes and the data contained within them are no longer required, disable the mailboxes. Then run Exchange 2016 Setup again.
  
- For more information about how to identify a mailbox in the database, see [Get-Mailbox](http://technet.microsoft.com/library/8a5a6eb9-4a75-47f9-ae3b-a3ba251cf9a8.aspx).
    
- For more information about how to move a mailbox, see [Mailbox moves in Exchange 2016](../../recipients/mailbox-moves.md).
    
- For more information about how to disable a mailbox, see [Disable-Mailbox](http://technet.microsoft.com/library/33be55a3-1880-437d-a631-c1cca1736421.aspx).
    
- For more information about how to remove a mailbox database, see [Manage mailbox databases in Exchange 2016](../../architecture/mailbox-servers/manage-databases.md).
    
Having problems? Ask for help in the Exchange forums. Visit the forums at: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkId=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkId=267542), or [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkId=285351).
  

  

