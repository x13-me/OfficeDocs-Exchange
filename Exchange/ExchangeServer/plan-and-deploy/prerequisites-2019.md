---
title: "Exchange 2019 prerequisites"
ms.author: chrisda
author: chrisda
manager: serdars
ms.date: 7/19/2018
ms.audience: ITPro
ms.topic: conceptual
ms.prod: exchange-server-it-pro
localization_priority: Critical
ms.collection: Strat_EX_Admin
ms.assetid: 
description: "Summary: Windows operating system prerequisites for Exchange 2019 and Exchange management tools."
---

# Exchange 2016 prerequisites

 **Summary**: Windows operating system prerequisites for Exchange 2019 and Exchange management tools.

> [!TIP]
> Coming from the Exchange Deployment Assistant? Click [Exchange 2013 prerequisites](https://technet.microsoft.com/library/bb691354(v=exchg.150).aspx).

This topic provides the steps for installing the necessary Windows Server operating system prerequisites for Exchange 2019 Mailbox servers and Edge Transport servers, and also the Windows prequisites for installing the Exchange 2019 management tools on Windows client computers.

After you've prepared your environment for Exchange 2019, use the Exchange Deployment Assistant for the next steps in your actual deployment. For information on hybrid deployments, see [Exchange Server Hybrid Deployments](https://technet.microsoft.com/library/jj200581(v=exchg.150).aspx).

> [!TIP]
> Have you heard about the Exchange Server Deployment Assistant? It's a free online tool that helps you quickly deploy Exchange 2016 in your organization by asking you a few questions and creating a customized deployment checklist just for you. If you want to learn more about it, go to [Microsoft Exchange Server Deployment Assistant](https://go.microsoft.com/fwlink/p/?linkid=626978).

## What do you need to know before you begin?

- Verify that your Active Directory forest functional level is Windows Server 2012 R2 or later, and that the schema master is running Windows Server 2012 R2 or later. For more information about the forest functional levels, see [Understanding Active Directory Domain Services (AD DS) Functional Levels](https://go.microsoft.com/fwlink/p/?linkId=137037).

- Verify the Windows operating system requirements for Exchange 2019 at [Operating system](system-requirements.md#operating-system).

- Verify the computer is joined to the appropriate internal Active Directory domain.

- Be aware that some prerequisites require you to reboot the server to complete the installation.

- Install the latest Windows updates on your computer. For more information, see [Deployment Security Checklist](https://technet.microsoft.com/library/aa996026(v=exchg.150).aspx). Note that this topic applies to Exchange 2013 and later.

    > [!NOTE]
    > You can't upgrade Windows from one version to another, or from Standard to Datacenter, when Exchange is installed on the server.

> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkId=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkId=267542), or [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkId=285351).


## Active Directory preparation

You can use any member of the Active Directory domain to prepare Active Directory for Exchange 2019. The computer has the following requirements:

1. Depending on the version of Windows, the computer requires the following software:

    - [.NET Framework 4.7.1](https://go.microsoft.com/fwlink/p/?linkid=866906) or later

    - [Visual C++ Redistributable Packages for Visual Studio 2013](https://go.microsoft.com/fwlink/?linkid=2002913).

2. Install the Remote Tools Administration Pack by running the following command in Windows PowerShell:

    ```
    Install-WindowsFeature RSAT-ADDS
    ```

For more information about preparing Active Directory, see [Prepare Active Directory and domains](prepare-ad-and-domains.md).

## Windows Server 2019 prerequisites

The requirements to install Exchange 2019 on computers running Windows Server 2019 are described in the following sections.

### Mailbox servers on Windows Server 2019

1. Run the following command in Windows PowerShell to install the required Windows components:

  ```
  Install-WindowsFeature AS-HTTP-Activation, Server-Media-Foundation, NET-Framework-45-Features, RPC-over-HTTP-proxy, RSAT-Clustering, RSAT-Clustering-CmdInterface, RSAT-Clustering-Mgmt, RSAT-Clustering-PowerShell, Web-Mgmt-Console, WAS-Process-Model, Web-Asp-Net45, Web-Basic-Auth, Web-Client-Auth, Web-Digest-Auth, Web-Dir-Browsing, Web-Dyn-Compression, Web-Http-Errors, Web-Http-Logging, Web-Http-Redirect, Web-Http-Tracing, Web-ISAPI-Ext, Web-ISAPI-Filter, Web-Lgcy-Mgmt-Console, Web-Metabase, Web-Mgmt-Console, Web-Mgmt-Service, Web-Net-Ext45, Web-Request-Monitor, Web-Server, Web-Stat-Compression, Web-Static-Content, Web-Windows-Auth, Web-WMI, Windows-Identity-Foundation, RSAT-ADDS
  ```

2. Install the [Visual C++ Redistributable Packages for Visual Studio 2013](https://go.microsoft.com/fwlink/?linkid=2002913).

### Edge Transport servers on Windows Server 2019

1. Run the following command in Windows PowerShell to install the required Windows components:

  ```
  Install-WindowsFeature ADLDS
  ```

2. Install the [Visual C++ Redistributable Packages for Visual Studio 2013](https://go.microsoft.com/fwlink/?linkid=2002913).

## Windows client prerequisites for the Exchange admin tools

The requirements to install the Exchange 2019 management tools on client computers running Windows 10 are described in the following steps:

1. Install the [Visual C++ Redistributable Packages for Visual Studio 2013](https://go.microsoft.com/fwlink/?linkid=2002913).

2. Run the following command from an elevated Windows PowerShell session:

```
Enable-WindowsOptionalFeature -Online -FeatureName IIS-ManagementScriptingTools,IIS-ManagementScriptingTools,IIS-IIS6ManagementCompatibility,IIS-LegacySnapIn,IIS-ManagementConsole,IIS-Metabase,IIS-WebServerManagementTools,IIS-WebServerRole
```


