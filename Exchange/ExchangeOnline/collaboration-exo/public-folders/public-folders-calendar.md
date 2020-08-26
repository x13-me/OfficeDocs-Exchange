---
localization_priority: Normal
description: Public folders calendars
ms.topic: conceptual
author: cichur
ms.author: v-cichur
ms.assetid: bf65842b-a4db-49a8-bb3a-d0bafb7d3e45
ms.reviewer: 
f1.keywords:
- NOCSH
title: Public folders calendars in Microsoft 365, Office 365, and Exchange Online
ms.collection: 
- exchange-online
- M365-email-calendar
audience: ITPro
ms.service: exchange-online
manager: serdars

---

# Public folder calendar

A public folder calendar is a good solution for people looking for only shared calendar without having to maintain an additional mailbox along with it. This article explains how to set up and access public folder calendars in Microsoft Exchange Online.

> [!Important]
> You must use the Microsoft Outlook desktop client to create the public folder calendar.

> [!Note]
> The Calendar type of public folder can be accessed from Outlook Web App (OWA) and the Outlook desktop client. Public folders, including calendar, cannot be accessed from OWA or the Outlook app on mobile devices.

## Prerequisites

Before you create your public folder calendar, follow the prerequisites.

1. Ensure public folders are [deployed](https://docs.microsoft.com/exchange/collaboration-exo/public-folders/create-public-folder-mailbox) in Exchange Online.

2. Use the following command to see a list of any public folder mailboxes present in the organization:

```
Get-Mailbox -PublicFolder
Get-PublicFolder \\
```

3. If you don't see a list of public folder mailboxes, then follow the steps to [create a public folder mailbox](https://docs.microsoft.com/exchange/collaboration-exo/public-folders/create-public-folder-mailbox).

4. Verify that you have the necessary [access rights](https://support.microsoft.com/help/2573274/public-folder-permissions-for-exchange-server) to create the public folder.

- If you want the user to be able to create a public folder on the root of the public folder hierarchy, along with all other access rights, run the following command:

  ```
  Add-PublicFolderClientPermission -Identity “\\” -AccessRights Owner -User User1
  ```

- If you want the user to be able to create a public folder under the existing public folder named Marketing, then run the following command:

  ```
   Add-PublicFolderClientPermission -Identity “\\Marketing” -AccessRights Editor -User User1
  ```

5. Login to the Outlook desktop client and ensure you're able to access the public folder deployment.

## Create a public folder calendar:
----------------------------------

Once you have ensured the prerequisites are met, then you're read to get started creating a public folder calendar.

1. Login to Outlook desktop client with user account that has necessary [access rights](https://support.microsoft.com/en-us/help/2573274/public-folder-permissions-for-exchange-server) to create public folder

2. Expand folders

> <img src="c:\Users\v-cichur\Documents\GitHub\OfficeDocs-Exchange-pr\Exchange\ExchangeOnline\collaboration-exo\public-folders/media/image1.png" style="width:3.12516in;height:1.02089in" alt="A screenshot of a cell phone Description automatically generated" />

3. Create new public folder

> To create public folder calendar on the root hierarchy, right click on “All Public Folders” and select New Folder…
>
> <img src="c:\Users\v-cichur\Documents\GitHub\OfficeDocs-Exchange-pr\Exchange\ExchangeOnline\collaboration-exo\public-folders/media/image2.png" style="width:3.90298in;height:3.42379in" alt="A screenshot of a cell phone Description automatically generated" />
>
> Or to create calendar under existing public folder, right click the folder and select “New Folder…”
>
> <img src="c:\Users\v-cichur\Documents\GitHub\OfficeDocs-Exchange-pr\Exchange\ExchangeOnline\collaboration-exo\public-folders/media/image3.png" style="width:3.97243in;height:4.27105in" alt="A screenshot of a cell phone Description automatically generated" />

4. Type in the name of Public folder to be created and select Calendar Items from the “Folder contains” drop down list and click OK

> <img src="c:\Users\v-cichur\Documents\GitHub\OfficeDocs-Exchange-pr\Exchange\ExchangeOnline\collaboration-exo\public-folders/media/image4.png" style="width:3.35434in;height:4.11827in" alt="A screenshot of a cell phone Description automatically generated" />

-   The calendar type folder shows up with different icon:

> <img src="c:\Users\v-cichur\Documents\GitHub\OfficeDocs-Exchange-pr\Exchange\ExchangeOnline\collaboration-exo\public-folders/media/image5.png" style="width:2.90987in;height:2.06261in" alt="A close up of a logo Description automatically generated" />

-   For faster access, right click on the folder and select Add to favourites

> <img src="c:\Users\v-cichur\Documents\GitHub\OfficeDocs-Exchange-pr\Exchange\ExchangeOnline\collaboration-exo\public-folders/media/image6.png" style="width:3.98632in;height:4.02798in" alt="A screenshot of a cell phone Description automatically generated" />

## Share a public folder calendar
------------------------------

By default, everyone in the organization can access public folder and create items on it:

> <img src="c:\Users\v-cichur\Documents\GitHub\OfficeDocs-Exchange-pr\Exchange\ExchangeOnline\collaboration-exo\public-folders/media/image7.png" style="width:4.09049in;height:5.40306in" alt="A screenshot of a social media post Description automatically generated" />

If you want to delegate additional access rights, add other users and provide required set of [permissions](https://support.microsoft.com/en-us/help/2573274/public-folder-permissions-for-exchange-server)

## Access a public folder calendar in OWA:
----------------------------------------

-   Login to OWA

-   Right click on Folders and select Add public folder to Favourites

> <img src="c:\Users\v-cichur\Documents\GitHub\OfficeDocs-Exchange-pr\Exchange\ExchangeOnline\collaboration-exo\public-folders/media/image8.png" style="width:3.50018in;height:1.74315in" alt="A screenshot of a cell phone Description automatically generated" />

-   Browse through the hierarchy, select the desired public folder and click Add Public Folder

> <img src="c:\Users\v-cichur\Documents\GitHub\OfficeDocs-Exchange-pr\Exchange\ExchangeOnline\collaboration-exo\public-folders/media/image9.png" style="width:6.06281in;height:3.88214in" alt="A screenshot of a cell phone Description automatically generated" />

-   Close the Add public folder menu

-   The calendar public folder show in Calendar area of the OWA

-   Click on Calendar icon

-   And you should see the public folder calendar under Other Calendars

> <img src="c:\Users\v-cichur\Documents\GitHub\OfficeDocs-Exchange-pr\Exchange\ExchangeOnline\collaboration-exo\public-folders/media/image10.png" style="width:3.17361in;height:6.46528in" />

 ## Receive emails to a public folder calendar
------------------------------------------

Follow the steps in [mail enable public folder calendar](enable-or-disable-mail-for-public-folder.md) to allow users email calendar invites/appointments to the calendar