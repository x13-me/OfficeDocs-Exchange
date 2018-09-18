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

# Exchange 2019 prerequisites


> [!TIP]
> Looking for information on previous versions? Use the following links for [Exchange 2016 prerequisites](prerequisites-2016.md) or [Exchange 2013 prerequisites](https://technet.microsoft.com/library/bb691354(v=exchg.150).aspx).

::: moniker range="exchserver-2013"

This topic provides the steps for installing the necessary Windows Server operating system prerequisites for Exchange 2019 Mailbox servers and Edge Transport servers, and also the Windows prequisites for installing the Exchange 2019 Management Tools on Windows client computers.

::: moniker-end

::: moniker range="exchserver-2016"

This topic provides the steps for installing the necessary Windows Server operating system prerequisites for Exchange 2016 Mailbox servers and Edge Transport servers, and also the Windows prequisites for installing the Exchange 2016 Management Tools on Windows client computers.

::: moniker-end

After you've prepared your environment for Exchange 2019, use the Exchange Deployment Assistant for the next steps in your actual deployment. For information on hybrid deployments, see [Exchange Server Hybrid Deployments](https://technet.microsoft.com/library/jj200581(v=exchg.150).aspx).

> [!TIP]
> Have you heard about the Exchange Server Deployment Assistant? It's a free online tool that helps you quickly deploy Exchange 2016 in your organization by asking you a few questions and creating a customized deployment checklist just for you. If you want to learn more about it, go to [Microsoft Exchange Server Deployment Assistant](https://go.microsoft.com/fwlink/p/?linkid=626978).

## What do you need to know before you begin?

- Verify that your Active Directory forest functional level is Windows Server 2012 R2 or later, and that the schema master is running Windows Server 2012 R2 or later. For more information about the forest functional levels, see [Understanding Active Directory Domain Services (AD DS) Functional Levels](https://go.microsoft.com/fwlink/p/?linkId=137037).

- Verify the Windows operating system requirements for Exchange 2019 at [Operating system](system-requirements.md#operating-system).

    > [!NOTE]
    > New to Exchange 2019 is the ability to upgrade your operating system to a newer version while Exchange is installed on Windows Server 2019 or later.
    
- Verify the computer is joined to the appropriate internal Active Directory domain.

- Install the latest Windows updates on your computer. For more information, see [Deployment Security Checklist](https://technet.microsoft.com/library/aa996026(v=exchg.150).aspx).

> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkId=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkId=267542), or [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkId=285351).


## Active Directory preparation

You can use any member of the Active Directory domain to prepare Active Directory for Exchange 2019. The computer has the following requirements:

1. The computer used to update the active directory requires the following software:

    - [.NET Framework 4.7.2](https://go.microsoft.com/fwlink/p/?linkid=863265) or later

    - [Visual C++ Redistributable Package for Visual Studio 2012](https://www.microsoft.com/download/details.aspx?id=30679) is required if using the graphical setup wizard.  When using the /Prepare switches in the command line version of SETUP to update the Active Directory, this package is not required.
    
     > [!NOTE]
    > Using the graphical setup wizard to prepare the Active Directory will require the installation of the Management Tools Exchange role.

2. Install the Remote Tools Administration Pack by running the following command in Windows PowerShell:

    ```
    Install-WindowsFeature RSAT-ADDS`
    ```

For more information about preparing Active Directory, see [Prepare Active Directory and domains](prepare-ad-and-domains.md).

## Windows Server 2019 prerequisites

The requirements to install Exchange 2019 on computers running Windows Server 2019 are described in the following sections. The recommended option is to simply use the setup parameter /InstallWindowsComponents when using the command line setup experience or selecting the check box in the graphical setup program to install windows prerequisites.  Using either of these options, you will no longer be required to restart your computer after the Windows components are added.

### Mailbox servers on Windows Server 2019

1. The computer used to host the Mailbox role requires the following software:

    - [.NET Framework 4.7.2](https://go.microsoft.com/fwlink/p/?linkid=863265) or later

    - [Visual C++ Redistributable Package for Visual Studio 2013](https://go.microsoft.com/fwlink/?linkid=2002913).

2. Add required Lync/Skype for Business components:

    - Install the Server Media Foundation windows feature by executing the following command in Windows PowerShell:
    
    ```
    Install-WindowsFeature Server-Media-Foundation`
    ```
    
   - Install [Unified Communications Managed API 4.0](https://www.microsoft.com/download/details.aspx?id=34992).  This package is available for download and in the \UCMARedist folder on the Exchange Server media.

   > [!NOTE]
    > When installing on Windows Server Core, you must use the installation package located in \UCMARedist on distributed media.Run the following command in Windows PowerShell to install the required Windows components:

3. Install the required Windows components using a setup option or execute the following in Windows PowerShell:

   > Desktop Experience:

    ```
    Install-WindowsFeature AS-HTTP-Activation, Server-Media-Foundation, NET-Framework-45-Features, RPC-over-HTTP-proxy, RSAT-Clustering, RSAT-Clustering-CmdInterface, RSAT-Clustering-Mgmt, RSAT-Clustering-PowerShell, Web-Mgmt-Console, WAS-Process-Model, Web-Asp-Net45, Web-Basic-Auth, Web-Client-Auth, Web-Digest-Auth, Web-Dir-Browsing, Web-Dyn-Compression, Web-Http-Errors, Web-Http-Logging, Web-Http-Redirect, Web-Http-Tracing, Web-ISAPI-Ext, Web-ISAPI-Filter, Web-Lgcy-Mgmt-Console, Web-Metabase, Web-Mgmt-Console, Web-Mgmt-Service, Web-Net-Ext45, Web-Request-Monitor, Web-Server, Web-Stat-Compression, Web-Static-Content, Web-Windows-Auth, Web-WMI, Windows-Identity-Foundation, RSAT-ADDS
    ```

   > Server Core:

    ```
    Install-WindowsFeature AS-HTTP-Activation, Server-Media-Foundation, NET-Framework-45-Features, RPC-over-HTTP-proxy, RSAT-Clustering, RSAT-Clustering-CmdInterface, RSAT-Clustering-Mgmt, RSAT-Clustering-PowerShell, WAS-Process-Model, Web-Asp-Net45, Web-Basic-Auth, Web-Client-Auth, Web-Digest-Auth, Web-Dir-Browsing, Web-Dyn-Compression, Web-Http-Errors, Web-Http-Logging, Web-Http-Redirect, Web-Http-Tracing, Web-ISAPI-Ext, Web-ISAPI-Filter, Web-Metabase, Web-Mgmt-Service, Web-Net-Ext45, Web-Request-Monitor, Web-Server, Web-Stat-Compression, Web-Static-Content, Web-Windows-Auth, Web-WMI, Windows-Identity-Foundation, RSAT-ADDS
    ```
    
### Edge Transport servers on Windows Server 2019

1. Install the [Visual C++ Redistributable Package for Visual Studio 2012](https://www.microsoft.com/download/details.aspx?id=30679).

2. Use a setup option to install the required Windows components or execute the following command in Windows PowerShell:

    ```
    Install-WindowsFeature ADLDS
    ```

## Windows client prerequisites for the Exchange 2019 management tools

The requirements to install the Exchange 2019 Management Tools on client computers running Windows 10 are described in the following steps:

1. Install the [Visual C++ Redistributable Package for Visual Studio 2012](https://www.microsoft.com/download/details.aspx?id=30679).

2. Use a setup option to install the required Windows components or run the following command from an elevated Windows PowerShell:

    ```
    Enable-WindowsOptionalFeature -Online -FeatureName IIS-ManagementScriptingTools,IIS-ManagementScriptingTools,IIS-IIS6ManagementCompatibility,IIS-LegacySnapIn,IIS-ManagementConsole,IIS-Metabase,IIS-WebServerManagementTools,IIS-WebServerRole
    ```
