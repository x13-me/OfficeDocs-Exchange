---
title: "Planning and deployment for Exchange 2019"
ms.author: chrisda
author: chrisda
manager: serdars
ms.date: 7/18/2018
ms.audience: ITPro
ms.topic: hub-page
ms.prod: exchange-server-it-pro
localization_priority: Priority
ms.collection: Strat_EX_Admin
ms.assetid: 692c59e3-f0b0-4cef-a66e-751aa740abae
description: "Summary: Guidance for planning and deploying Exchange Server 2019."
---

# Planning and deployment

 **Summary**: Guidance for planning and deploying Exchange Server 2019.

The following sections contain links to information about planning for and then deploying Exchange Server 2019.

> [!IMPORTANT]
> Make sure you read the [Release notes for Exchange 2019](../release-notes-2019.md) topic before you begin your deployment. The release notes contain important information on issues you might encounter during and after your deployment.

## Planning for Exchange 2019

 Use the information at following links to help plan your deployment of Exchange 2019 into your organization.

> [!IMPORTANT]
> See the [Establish a test environment](#establish-a-test-environment) section later in this topic for information about installing Exchange 2019 in a test environment.

[Exchange architecture](../architecture/architecture.md)

> Learn about the Mailbox and Edge Transport server roles and more in Exchange 2019.

[Exchange 2019 system requirements](system-requirements.md)

> Understand the system requirements that need to be satisfied in your organization before you can install Exchange 2019.

[Exchange 2019 prerequisites](prerequisites.md)

> Learn about the Windows Server features and the other software that needs to be installed for a successful installation of Exchange 2019.

[Microsoft Exchange Server Deployment Assistant](https://go.microsoft.com/fwlink/p/?LinkId=626978)

> Use this tool to generate a customized checklist for planning, installing, or upgrading to Exchange 2019. Guidance is available for multiple scenarios, including an on-premises, hybrid, or cloud deployment.

[Active Directory](active-directory/active-directory.md)

> Read this topic to learn about how Exchange 2019 uses Active Directory and how your Active Directory deployment affects your Exchange deployment.

[Antispam and antimalware protection in Exchange Server](../antispam-and-antimalware/antispam-and-antimalware.md)

> Read this topic to understand the built-in antispam and antimalware protection options in Exchange 2019.

[Exchange Server Hybrid Deployments](https://docs.microsoft.com/exchange/exchange-hybrid)

> Read this topic to help you with planning a hybrid deployment with Microsoft Office 365 and your on-premises Exchange 2019 organization.

[Exchange 2016 virtualization](../plan-and-deploy/virtualization.md)

> Read this topic to learn more about how you can deploy Exchange 2019 in a virtualized environment.

[Exchange Online and Exchange development](https://docs.microsoft.com/exchange/client-developer/exchange-server-development)

> This topic contains important information about Application Programming Interfaces (APIs) that are available for applications that use Exchange 2019.

### Establish a test environment

Before installing Exchange 2019 for the first time, we recommend that you install it in an isolated test environment. This approach reduces the risk of end-user downtime and negative ramifications to the production environment.

The test environment will act as your "proof of concept" for your new Exchange 2019 design and make it possible to move forward or roll back any implementations before deploying into your production environments. Having an exclusive test environment for validation and testing allows you to do pre-installation checks for your future production environments. By installing in a test environment first, we believe that your organization will have a better likelihood of success in a full production implementation.

For many organizations, the costs of building a test lab may be high because of the need to duplicate the production environment. To reduce the hardware costs associated with a prototype lab, we recommend the use of virtualization by using Hyper-V technologies in Windows Server. Hyper-V enables server virtualization, allowing multiple virtual operating systems to run on a single physical machine.

For more detailed information about Hyper-V, see [Server Virtualization](https://go.microsoft.com/fwlink/p/?LinkId=117704). For information about Microsoft support of production Exchange 2019 server on hardware virtualization software, see [Exchange 2019 system requirements](system-requirements.md#exchange-2019-system-requirements).

## Deploying Exchange 2019

The deployment phase is the period when you install Exchange 2019 into your organization. Before you begin the deployment phase, you should plan your Exchange organization. For more information, see the [Planning for Exchange 2019](#planning-for-exchange-2019) section earlier in this topic.

Use the information at the following links to help you deploy Exchange 2019.

[Prepare Active Directory and domains for Exchange 2019](prepare-ad-and-domains.md)

> Learn about the steps you need to take to prepare your Active Directory forest for Exchange 2019 and the changes Exchange makes to your forest.

[Install the Exchange 2019 Mailbox role using the Setup wizard](deploy-new-installations/install-mailbox-role.md)

> Follow the steps in this topic to use the Exchange 2019 Setup wizard to install Exchange 2016 Mailbox servers into a new Exchange organization.

[Install Exchange 2019 using unattended mode](deploy-new-installations/unattended-installs.md)

> Follow the steps in this topic to use Exchange 2019 unattended setup to install Exchange 2019 into a new Exchange organization.

[Install the Exchange 2019 Edge Transport role using the Setup wizard](deploy-new-installations/install-edge-transport-role.md)

> Follow the steps in this topic to use the Exchange 2019 Setup wizard to install the Exchange 2016 Edge Transport server into a perimeter network.

[Upgrade Exchange 2019 to the latest cumulative update](install-cumulative-updates.md)

> Follow the steps in this topic to apply the latest cumulative update or service pack to Exchange 2019 servers in your organization.

[Exchange Server Hybrid Deployments](https://docs.microsoft.com/exchange/exchange-hybrid)

> Read this topic for information that will help you deploy Exchange in an existing hybrid deployment.

[Exchange 2019 post-installation tasks](post-installation-tasks/post-installation-tasks.md)

> Learn about post-installation tasks to complete your Exchange 2019 installation.

## Understanding Exchange 2016 Setup

You can use different types and modes of Exchange 2019 Setup to install and maintain the various editions and versions of Exchange 2019.

### Exchange editions and versions

Exchange 2019 is available in two server editions: Standard Edition and Enterprise Edition. The edition you install is defined by your product key (the only available download can install both versions). For more information, see [Exchange Server Licensing](https://go.microsoft.com/fwlink/p/?linkid=237292).

### Types of Exchange Setup

You have the following options for Exchange 2016 Setup:

- **Exchange Setup wizard**: Running Setup.exe without any command-line switches provides an interactive experience where you're guided by the Exchange 2019 Setup wizard.

- **Exchange unattended setup**: Running Setup.exe with command-line switches enables you to install Exchange from an interactive command line or through a script.

### Modes of Exchange Setup

Setup for Exchange 2019 includes the following modes:

- **Install**: You're installing a new server role (Mailbox server, Edge Transport server, or Management tools). This mode is available in the Exchange Setup wizard and unattended setup.

- **Uninstall**: You're removing the Exchange installation from a computer. You can use this mode from both the Exchange Setup wizard and unattended setup.

- **Upgrade**: You're installing a cumulative update (CU) on an existing Exchange server. You can use this mode from both the Exchange Setup wizard and unattended setup.

  > [!NOTE]
  > Exchange doesn't support in-place upgrades from previous versions. This mode is used only to install CUs.

- **RecoverServer**: There's been a catastrophic failure of an Exchange server and you need to recover data. You must install a Windows server using the same fully qualified domain name (FQDN) as the failed server, and then run Exchange Setup with the **/m:RecoverServer** switch without specifiying the Exchange server roles to restore.

    Setup detects the Exchange server object in Active Directory and installs the corresponding files and configuration automatically. After you recover the server, you can restore databases and reconfigure any additional settings. To run in **RecoverServer** mode:

    - You can't have Exchange already installed on the server.

    - The Exchange server object must exist in Active Directory.

    - You can only use unattended setup.

  > [!NOTE]
  > You must complete one mode of Setup before you can use another mode.
