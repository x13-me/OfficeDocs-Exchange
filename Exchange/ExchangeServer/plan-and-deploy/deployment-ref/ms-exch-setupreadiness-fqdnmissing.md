---
title: "Primary DNS Suffix is missing [ms.exch.setupreadiness.FqdnMissing]"
ms.author: dstrome
author: dstrome
manager: serdars
ms.date: 7/22/2015
ms.audience: ITPro
ms.topic: reference
f1_keywords:
- 'ms.exch.setupreadiness.FqdnMissing'
ms.prod: exchange-server-it-pro
localization_priority: Normal
ms.assetid: 310765bf-a650-4a3d-a5e4-6173b559d4f6
description: "Microsoft Exchange Server 2016 Setup can't continue because the primary domain name system (DNS) suffix for the computer you're installing Exchange on hasn't been configured."
---

# Primary DNS Suffix is missing [ms.exch.setupreadiness.FqdnMissing]

Microsoft Exchange Server 2016 Setup can't continue because the primary domain name system (DNS) suffix for the computer you're installing Exchange on hasn't been configured.
  
To resolve this issue, add a primary DNS suffix on the computer using the steps below and then run Setup again.
  
> [!IMPORTANT]
> Changing the computer name or primary DNS suffix after you install Exchange 2016 isn't supported.
  
1. Log on to the computer where you want to install the Edge Transport role as a user that's a member of the local Administrators group.
    
2. Open the **Control Panel** and then double-click **System**.
    
3. In the **Computer name, domain, and workgroup settings** section, click **Change settings**.
    
4. In the **System Properties** window, make sure the **Computer Name** tab is selected and then click **Change…**.
    
5. In **Computer Name/Domain Changes**, click **More…**.
    
6. In **Primary DNS suffix of this computer**, enter the DNS domain name for the Edge Transport server. For example, contoso.com.
    
7. Click **OK** to close each window.
    
Having problems? Ask for help in the Exchange forums. Visit the forums at: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkId=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkId=267542), or [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkId=285351).
