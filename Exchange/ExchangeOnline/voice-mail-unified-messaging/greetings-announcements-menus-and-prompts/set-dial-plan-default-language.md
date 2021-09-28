---
ms.localizationpriority: medium
description: You can set the default language for a Unified Messaging (UM) dial plan. Each dial plan you create will initially use English (en-US) as the default language.
ms.topic: article
author: msdmaguire
ms.author: jhendr
ms.assetid: 7a1d2e7e-4053-40af-9ec1-ec714df12ad4
ms.reviewer: 
f1.keywords:
- NOCSH
title: Set the default language on a dial plan in Exchange Online
ms.collection: exchange-online
audience: ITPro
ms.service: exchange-online
manager: serdars

---

# Set the default language on a dial plan in Exchange Online

> [!NOTE]
> Cloud Voicemail takes the place of Exchange Unified Messaging (UM) in providing voice messaging functionality for Skype for Business 2019 voice users who have mailboxes on Exchange Server 2019 or Exchange Online, and for Microsoft Teams or Skype for Business Online voice users. For more information, see [Plan Cloud Voicemail service](/skypeforbusiness/hybrid/plan-cloud-voicemail) and [Retiring Unified Messaging in Exchange Online](https://techcommunity.microsoft.com/t5/Exchange-Team-Blog/Retiring-Unified-Messaging-in-Exchange-Online/ba-p/608991).

### Use the EAC to set the default language on a UM dial plan

1. In the EAC, navigate to **Unified Messaging** \> **UM dial plans**.

2. In the list view, select the UM dial plan that you want to modify, and then, on the toolbar, click **Edit** ![Edit icon.](../../media/ITPro_EAC_EditIcon.gif).

3. On the **UM dial plan** page, click **Configure**.

4. On the **Settings** page, under **Audio language**, select the language you want to set from the drop-down list.

5. Click **Save** to accept your changes.

### Use Exchange Online PowerShell to set the default language on a UM dial plan

This example sets the default language on a UM dial plan named `MyUMDialPlan` to German.

```PowerShell
Set-UMDialPlan -Identity MyUMDialPlan -DefaultLanguage de-DE
```

This example sets the default language on a UM dial plan named `MyUMDialPlan` to Japanese.

```PowerShell
Set-UMDialPlan -Identity MyUMDialPlan -DefaultLanguage ja-JP
```

This example sets the default language on a UM dial plan named `MyUMDialPlan` to Australian English.

```PowerShell
Set-UMDialPlan -Identity MyUMDialPlan -DefaultLanguage en-AU
```
