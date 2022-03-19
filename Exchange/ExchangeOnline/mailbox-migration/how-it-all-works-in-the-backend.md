---
title: Overview of the G Suite migration process in Exchange Online
ms.author: v-aiyengar
author: AshaIyengar21
manager: serdars
audience: Admin
ms.topic: conceptual
ms.service: exchange-online
localization_priority: Normal
search.appverid: MET150
f1.keywords:
- NOCSH
description: Overview of the backend process that takes place while you are migrating from G-Suite to Microsoft 365 or Office 365
ms.custom: seo-marvel-jun2021
---

# Overview of the G Suite migration process in Exchange Online

Before beginning your migration, review the following diagrams to understand how a Google Workspace staged migration works. The diagrams show how a fictitious company named Fabrikam, Inc., with the domain name *fabrikaminc.net* performed their migration.

![Original setup before G Suite migration.](../media/gsuite-mig-original-setup.png)

Prior to their migration, the MX record for the base "fabrikaminc.net" domain points to the Google Workspace tenant or mail server where all or most of Fabrikam, Inc.'s users are. Note that users have their primary email addresses at that domain.

![Before the G Suite migration begins.](../media/gsuite-mig-before-migration.png)

The MX record for the primary domain "fabrikaminc.net" still points to Google Workspace, where all the primary mailboxes reside. To prepare for the migration, new routing domains have been created: the *gsuite.fabrikaminc.net* domain points to Google Workspace and the *o365.fabrikaminc.net* domain points to Microsoft 365 or Office 365.

On the Google Workspace side, aliases have been added for all of the users in the Google Workspace routing domain. On the Microsoft 365 or Office 365 side, MailUsers have been provisioned for all of the users from the Google Workspace tenant. The ExternalEmailAddress field for MailUsers on the Microsoft 365 or Office 365 side were configured to point back to the primary mailbox using the address at the routing domain for the Google Workspace side. Additionally, there should be aliases for the user in the Microsoft 365 or Office 365 routing domain.

The green arrow indicates how, at this point in the migration, User 2 still contacts User 1 through their Google Workspace email addresses.

![During a single batch of a G Suite migration.](../media/gsuite-mig-during-batch.png)

User 1 and User 2 are part of the first migration batch to Microsoft 365 or Office 365, while User 3 and User 4 will be part of a later batch. The MX record for the primary domain "fabrikaminc.net" still points to Google Workspace, where all the primary mailboxes still reside. Because User 1 and User 2 have had their migrations started, they've been converted from MailUsers to Mailboxes on the Microsoft 365 or Office 365 side.

The ExternalEmailAddress for each user has been moved to a ForwardingSmtpAddress, so that messages sent to User 1 and User 2 will be delivered back to their source mailboxes on the Google Workspace side by rerouting the message back to the Google Workspace routing domain. This is indicated by the red arrows in the above diagram. Mail is still being synced from the source Google Workspace side to the Microsoft 365 or Office 365 side.

![After a single batch of a G Suite migration.](../media/gsuite-mig-after-batch.png)

The MX record for the primary domain "fabrikaminc.net" still points to Google Workspace. Now that User 1 and User 2 have been fully migrated to Microsoft 365 or Office 365, they should start working out of Microsoft 365 or Office 365. On the Google Workspace side, automatic mail forwarding has been set up for migrated users, so that new emails sent to their Google Workspace address will be delivered instead to the Microsoft 365 or Office 365 address via the routing domain. This is shown by the green arrows in the above diagram.

> [!IMPORTANT]
> If your organization has disabled a user's ability to set a forwarding address, the Google Workspace migration tool will also be unable to set the forwarding address. You must enable permissions to set SMTP forwarding in order for forwarding to be set successfully during your migration.

Meanwhile, the forwarding address has been removed from the Microsoft 365 or Office 365 user object, so emails will be delivered to that user in the Microsoft 365 or Office 365 routing domain (as shown by the red arrows above).

![After G Suite migration is complete.](../media/gsuite-mig-after-migration.png)

After all migration batches have been completed, all users can use their migrated mailboxes on Microsoft 365 or Office 365 as their primary mailbox. A manual MX record update for the primary domain "fabrikaminc.net" then points to the Microsoft 365 or Office 365 organization instead of the Google Workspace tenant. The routing domains and extra aliases can now be removed, as can the Google Workspace tenant. The migration of mail, calendar, and contacts from Google Workspace to Microsoft 365 or Office 365 is now complete.
