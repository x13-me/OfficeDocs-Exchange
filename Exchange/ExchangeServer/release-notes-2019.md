---
title: "Release notes for Exchange 2019"
ms.author: chrisda
author: chrisda
manager: serdars
ms.date: 7/18/2018
ms.audience: ITPro
ms.topic: get-started-article
ms.prod: exchange-server-it-pro
localization_priority: Critical
ms.assetid: 
description: "Summary: Important information that you need to know to successfully deploy Exchange Server 2019."
---

# Release notes for Exchange 2019

> [!TIP]
> Coming from the Exchange Deployment Assistant? Click [Release notes for Exchange 2016](release-notes.md) or [Release notes for Exchange 2013](https://technet.microsoft.com/library/jj150489(v=exchg.150).aspx) .

Welcome to Microsoft Exchange Server 2019! This topic contains important information that you need to know to successfully deploy Exchange 2019. Please read this topic completely before beginning your deployment.

**Known issues in Exchange Server 2019**

When attempting to uninstall Exchange Server on Windows 2019 Server Core using the graphical setup wizard, the operation will fail.  The wizard attempts to launch the Control Panel to uninstall Exchange Server which does not exist in Windows Server Core.  To uninstall Exchange Server on Windows Server Core use the command line version of SETUP.

    ```
    SETUP.exe /m:uninstall
    ```

This issue will be resolved in a future CU update for Exchange Server 2019.
