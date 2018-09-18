---
title: "Exchange prerequisites"
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
description: "Summary: Windows operating system prerequisites for Exchange and Exchange management tools."
---

# Exchange Server prerequisites

This topic provides the steps for installing the necessary Windows Server operating system prerequisites for Exchange Mailbox servers and Edge Transport servers, and also the Windows prerequisites for installing the Exchange Management Tools on Windows client computers.

After you've prepared your environment for Exchange, use the Exchange Deployment Assistant for the next steps in your actual deployment. For information on hybrid deployments, see [Exchange Server Hybrid Deployments](https://technet.microsoft.com/library/jj200581(v=exchg.150).aspx).

> [!TIP]
> Have you heard about the Exchange Server Deployment Assistant? It's a free online tool that helps you quickly deploy Exchange Server in your organization by asking you a few questions and creating a customized deployment checklist just for you. If you want to learn more about it, go to [Microsoft Exchange Server Deployment Assistant](https://go.microsoft.com/fwlink/p/?linkid=626978).

## What do you need to know before you begin?

::: moniker range="exchserver-2019"

- Verify that your Active Directory forest functional level is Windows Server 2012 R2 or later, and that the schema master is running Windows Server 2012 R2 or later. For more information about the forest functional levels, see [Understanding Active Directory Domain Services (AD DS) Functional Levels](https://go.microsoft.com/fwlink/p/?linkId=137037).

::: moniker-end

::: moniker range="exchserver-2016"

- Make sure that the functional level of your forest is at least Windows Server 2008 R2, and that the schema master is running Windows Server 2008 R2 or later. For more information about the Windows functional level, see [Understanding Active Directory Domain Services (AD DS) Functional Levels](https://go.microsoft.com/fwlink/p/?linkId=137037).

- The full installation option of Windows Server 2012 and Windows Server 2012 R2 must be used for all servers running Exchange 2016 server roles or management tools.

- Some prerequisites require you to reboot the server to complete installation.

    > [!NOTE]
    > You can't upgrade Windows from one version to another, or from Standard to Datacenter, when Exchange is installed on the server.

::: moniker-end

- Verify the Windows operating system requirements for Exchange at [Operating system](system-requirements.md#operating-system).

::: moniker range="exchserver-2019"

    > [!NOTE]
    > New to Exchange 2019 is the ability to upgrade your operating system to a newer version while Exchange is installed on Windows Server 2019 or later.

::: moniker-end
    
- Verify the computer is joined to the appropriate internal Active Directory domain.

- Install the latest Windows updates on your computer. For more information, see [Deployment Security Checklist](https://technet.microsoft.com/library/aa996026(v=exchg.150).aspx).

> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkId=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkId=267542), or [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkId=285351).


## Active Directory preparation

You can use any member of the Active Directory domain to prepare Active Directory for Exchange. The computer has the following requirements:

::: moniker range="exchserver-2019"

1. The computer used to update the active directory requires the following software:

    - [.NET Framework 4.7.2](https://go.microsoft.com/fwlink/p/?linkid=863265) or later

    - [Visual C++ Redistributable Package for Visual Studio 2012](https://www.microsoft.com/download/details.aspx?id=30679) is required if using the graphical setup wizard.  When using the /Prepare switches in the command line version of SETUP to update the Active Directory, this package is not required.
    
     > [!NOTE]
    > Using the graphical setup wizard to prepare the Active Directory will require the installation of the Management Tools Exchange role.

2. Install the Remote Tools Administration Pack by running the following command in Windows PowerShell:

    ```
    Install-WindowsFeature RSAT-ADDS`
    ```
::: moniker-end

::: moniker range="exchserver-2016"

First, install the following software on the computer that will be used to prepare Active Directory:

- [.NET Framework 4.7.1](https://go.microsoft.com/fwlink/p/?linkid=866906)

- [Visual C++ Redistributable Packages for Visual Studio 2013](https://go.microsoft.com/fwlink/?linkid=2002913)

After you've installed the software listed above, complete the following steps to install the Remote Tools Administration Pack. After you've installed the Remote Tools Administration Pack you'll be able to use the computer to prepare Active Directory. For more information about preparing Active Directory, see [Prepare Active Directory and domains](prepare-ad-and-domains.md).

1. Open Windows PowerShell.

2. Install the Remote Tools Administration Pack using the following command.

  ```
  Install-WindowsFeature RSAT-ADDS
  ```

::: moniker-end

For more information about preparing Active Directory, see [Prepare Active Directory and domains](prepare-ad-and-domains.md).

::: moniker range="exchserver-2019"

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
::: moniker-end

::: moniker range="exchserver-2016"

## Windows Server 2012 and Windows Server 2012 R2 prerequisites
<a name="WS2012"> </a>

The prerequisites that are needed to install Exchange 2016 on computers running Windows Server 2012 or Windows Server 2012 R2 depends on which Exchange role you want to install. Read the section below that matches the role you want to install.

### Mailbox server role
<a name="WS2012MBX"> </a>

Follow the instructions in this section to install the prerequisites on computers running Windows Server 2012 or Windows Server 2012 R2 where you want to install the Mailbox server role.

Do the following to install the required Windows roles and features:

1. Open Windows PowerShell.

2. Run the following command to install the required Windows components.

  ```
  Install-WindowsFeature AS-HTTP-Activation, Server-Media-Foundation, NET-Framework-45-Features, RPC-over-HTTP-proxy, RSAT-Clustering, RSAT-Clustering-CmdInterface, RSAT-Clustering-Mgmt, RSAT-Clustering-PowerShell, Web-Mgmt-Console, WAS-Process-Model, Web-Asp-Net45, Web-Basic-Auth, Web-Client-Auth, Web-Digest-Auth, Web-Dir-Browsing, Web-Dyn-Compression, Web-Http-Errors, Web-Http-Logging, Web-Http-Redirect, Web-Http-Tracing, Web-ISAPI-Ext, Web-ISAPI-Filter, Web-Lgcy-Mgmt-Console, Web-Metabase, Web-Mgmt-Console, Web-Mgmt-Service, Web-Net-Ext45, Web-Request-Monitor, Web-Server, Web-Stat-Compression, Web-Static-Content, Web-Windows-Auth, Web-WMI, Windows-Identity-Foundation, RSAT-ADDS
  ```

After you've installed the operating system roles and features, install the following software in the order shown:

1. [.NET Framework 4.7.1](https://go.microsoft.com/fwlink/p/?linkid=866906)

2. [Visual C++ Redistributable Packages for Visual Studio 2013](https://go.microsoft.com/fwlink/?linkid=2002913)

3. [Microsoft Unified Communications Managed API 4.0, Core Runtime 64-bit](https://go.microsoft.com/fwlink/p/?linkId=258269)

### Edge Transport server role
<a name="WS2012Edge"> </a>

Follow the instructions in this section to install the prerequisites on computers running Windows Server 2012 or Windows Server 2012 R2 where you want to install the Edge Transport server role.

Do the following to install the required Windows roles and features:

1. Open Windows PowerShell.

2. Run the following command to install the required Windows components.

  ```
  Install-WindowsFeature ADLDS
  ```

After you've installed the operating system roles and features, install the following software in the order shown:

1. [.NET Framework 4.7.1](https://go.microsoft.com/fwlink/p/?linkid=866906)

2. [Visual C++ Redistributable Packages for Visual Studio 2013](https://go.microsoft.com/fwlink/?linkid=2002913)

## Windows Server 2016 prerequisites
<a name="WS2016"> </a>

The prerequisites that are needed to install Exchange 2016 on computers running Windows Server 2016 depends on which Exchange role you want to install. Read the section below that matches the role you want to install.

> [!IMPORTANT]
> Exchange 2016 Cumulative Update 3 or later is required if you want to install Exchange on Windows Server 2016.

### Mailbox server role
<a name="WS2016MBX"> </a>

Follow the instructions in this section to install the prerequisites on computers running Windows Server 2016 where you want to install the Mailbox server role.

Do the following to install the required Windows roles and features:

1. Open Windows PowerShell.

2. Run the following command to install the required Windows components.

  ```
  Install-WindowsFeature NET-Framework-45-Features, Server-Media-Foundation, RPC-over-HTTP-proxy, RSAT-Clustering, RSAT-Clustering-CmdInterface, RSAT-Clustering-Mgmt, RSAT-Clustering-PowerShell, Web-Mgmt-Console, WAS-Process-Model, Web-Asp-Net45, Web-Basic-Auth, Web-Client-Auth, Web-Digest-Auth, Web-Dir-Browsing, Web-Dyn-Compression, Web-Http-Errors, Web-Http-Logging, Web-Http-Redirect, Web-Http-Tracing, Web-ISAPI-Ext, Web-ISAPI-Filter, Web-Lgcy-Mgmt-Console, Web-Metabase, Web-Mgmt-Console, Web-Mgmt-Service, Web-Net-Ext45, Web-Request-Monitor, Web-Server, Web-Stat-Compression, Web-Static-Content, Web-Windows-Auth, Web-WMI, Windows-Identity-Foundation, RSAT-ADDS
  ```

After you've installed the operating system roles and features, install the following software in the order shown:

1. [.NET Framework 4.7.1](https://go.microsoft.com/fwlink/p/?linkid=866906)

2. [Microsoft Knowledge Base article KB3206632](https://go.microsoft.com/fwlink/p/?linkid=837748)

3. [Visual C++ Redistributable Packages for Visual Studio 2013](https://go.microsoft.com/fwlink/?linkid=2002913)

4. [Microsoft Unified Communications Managed API 4.0, Core Runtime 64-bit](https://go.microsoft.com/fwlink/p/?linkId=258269)

### Edge Transport server role
<a name="WS2016Edge"> </a>

Follow the instructions in this section to install the prerequisites on computers running Windows Server 2016 where you want to install the Edge Transport server role.

Do the following to install the required Windows roles and features:

1. Open Windows PowerShell.

2. Run the following command to install the required Windows components.

  ```
  Install-WindowsFeature ADLDS
  ```

After you've installed the operating system roles and features, install the following software in the order shown:

1. [.NET Framework 4.7.1](https://go.microsoft.com/fwlink/p/?linkid=866906)

2. [Visual C++ Redistributable Packages for Visual Studio 2013](https://go.microsoft.com/fwlink/?linkid=2002913)

## Windows 8.1 and Windows 10 prerequisites (admin tools only)
<a name="Windows8"> </a>

Follow the instructions in this section to install the prerequisites on computers running Windows 8.1 or Windows 10 where you want to install the Exchange 2016 Admin Tools.

On Windows 8.1 computers, install [.NET Framework 4.7.1](https://go.microsoft.com/fwlink/p/?linkid=866906).

On Windows 8.1 and Windows 10 computers, install [Visual C++ Redistributable Packages for Visual Studio 2013](https://go.microsoft.com/fwlink/?linkid=2002913).

On Windows 8.1 and Windows 10 computers, run the following command from an elevated Windows PowerShell session.

```
Enable-WindowsOptionalFeature -Online -FeatureName IIS-ManagementScriptingTools,IIS-ManagementScriptingTools,IIS-IIS6ManagementCompatibility,IIS-LegacySnapIn,IIS-ManagementConsole,IIS-Metabase,IIS-WebServerManagementTools,IIS-WebServerRole
```

::: moniker-end