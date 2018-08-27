---
title: "Exchange 2019 system requirements"
ms.author: chrisda
author: chrisda
manager: serdars
ms.date: 7/18/2018
ms.audience: ITPro
ms.topic: conceptual
ms.prod: exchange-server-it-pro
localization_priority: Critical
ms.collection: Strat_EX_Admin
ms.assetid: 
description: "Summary: Learn about what you need to have in your environment before installing Exchange Server 2019."
---

# Exchange 2019 system requirements

 **Summary**: Learn about what you need to have in your environment before installing Exchange Server 2019.

> [!TIP]
> Looking for requirements for previous versions? Click [Exchange 2016 system requirements](system-requirements-2016.md) or [Exchange 2013 system requirements](https://technet.microsoft.com/library/aa996719(v=exchg.150).aspx).

Before you install Exchange Server 2019, we recommend that you review this topic to ensure your network, hardware, software, clients, and other elements meet the requirements for Exchange 2019. Also, make sure you understand the coexistence scenarios that are supported for Exchange 2019 and earlier versions of Exchange.

## Supported coexistence scenarios

The supported coexistence scenarios between Exchange 2019 and earlier versions of Exchange are described in the following table:

|**Exchange version**|**Exchange 2019 organization coexistence**|
|:-----|:-----|
|Exchange 2010 and earlier versions|Not supported|
|Exchange 2013|Supported with Exchange 2013 Cumulative Update 21 (CU21) or later on all Exchange 2013 servers in the organization, including Edge Transport servers.|
|Exchange 2016|Supported with Exchange 2016 CU10 or later on all Exchange 2016 servers in the organization, including Edge Transport servers.
|Mixed Exchange 2013 and Exchange 2016 organization|Supported if all Exchange 2013 and Exchange 2016 servers in the organization meet the requirements as previously described in this table.|
 
## Supported hybrid deployment scenarios

Exchange 2019 supports hybrid deployments with Office 365 tenants that have been upgraded to the latest version of Office 365. For more information about specific hybrid deployments, see [Hybrid deployment prerequisites](../../ExchangeHybrid/hybrid-deployment-prerequisites.md).

## Network and directory servers

The requirements for the network and the directory servers in your Exchange 2019 organization are described in the following table:

|**Component**|**Requirement**|
|:-----|:-----|
|Domain controllers|All domain controllers in the forest need to be running one of the following versions of Windows Server: <br/>• Windows Server 2019 Standard or Datacenter <br/>• Windows Server 2016 Standard or Datacenter <br/>• Windows Server 2012 R2 Standard or Datacenter|
|Active Directory|The Active Directory forest functionality level needs to be **Windows Server 2012 R2** or higher.|
|DNS namespace|Exchange 2010 or later supports the following DNS namespaces:  <br/> • Contiguous  <br/> • Noncontiguous  <br/> • Single label domains  <br/> • Disjoint  <br/> For more information about DNS namespaces that are supported by Exchange, see [KB2269838](https://go.microsoft.com/fwlink/p/?linkid=3052&kbid=2269838).|
|IPv6|Exchange 2013 or later supports IPv6 only when IPv4 is also installed and enabled on the Exchange server. <br/> If you deploy Exchange in this configuration, and your network supports IPv4 and IPv6, all Exchange 2013 or later servers can send data to and receive data from devices, servers, and clients that use IPv6 addresses. For more information, see [IPv6 Support in Exchange 2013](https://technet.microsoft.com/library/33543023-eb9a-4102-b990-84a818a52814.aspx).|
 
## Directory server architecture

Active Directory domain controllers on 64-bit hardware with a 64-bit version of Windows Server will increase directory service performance for Exchange 2019.

### Installing Exchange on directory servers

For security and performance reasons, we don't recommend installing Exchange 2019 on Active Directory directory servers. Only install Exchange 2019 on member servers.

To learn more about the issues that you'll encounter when you install Exchange on a directory server, see [Installing Exchange on a domain controller is not recommended [WarningInstallExchangeRolesOnDomainController]](../plan-and-deploy/deployment-ref/ms-exch-setupreadiness-warninginstallexchangerolesondomaincontroller.md). After Exchange is installed, changing the server role from a member server to a directory server or vice-versa isn't supported.

## Hardware

For information about deploying Exchange in a virtualized environment, see [Exchange Server virtualization](../plan-and-deploy/virtualization.md).

 |**Component**|**Requirement**|**Notes**|
|:-----|:-----|:-----|
|Processor|Either of the following types of 64-bit processors: <br/>• Intel processor that supports Intel 64 architecture (formerly known as Intel EM64T). <br/>• AMD processor that supports the AMD64 platform. <br/> **Note**: Intel Itanium IA64 processors aren't supported.|See the [Operating system](#operating-system) section later in this topic for supported operating systems.|
|Memory|Varies depending on Exchange roles that are installed: <br/>• **Mailbox**: 128GB minimum <br/>• **Edge Transport**: 64GB minimum  <br/> Note that Exchange 2019 has large memory support (up to 256 GB).||
|Paging file size| Set the page file to a size equal to 25% of installed memory.|None|
|Disk space|• At least 30GB of free space on the drive where you're installing Exchange. <br/>• At least 200MB of free space on the system drive. <br/>• At least 500MB on the drive containing the message queue database.||
|Screen resolution|1024 x 768 pixels (XGA) or higher|None|
|File system|NTFS is required on partitions that contain the following types of files: <br/> • The System partition. <br/> • Exchange binaries.  <br/>•  Files generated by Exchange diagnostic logging. <br/> • Transport database files (for example, the mail queue database). <br/> Optionally, you can use ReFS on the partitions that contain the following types of files: <br/> • Mailbox databases and transaction logs.|None|
 
## Operating system

The supported operating systems for Exchange 2019 are described in the following table:

|**Exchange component**|**Requirement**|
|:-----|:-----|
|Mailbox and Edge Transport server roles|Windows Server 2019 Standard or Datacenter|
|Management tools|One of the following versions of Windows:  <br/>• Windows Server 2019 Standard or Datacenter <br/>• 64-bit edition of Windows 10|

**Notes**:

- Installing Exchange 2019 on a computer that's running Windows Server Core is fully supported and recommended. The Desktop Experience feature is no longer required.

- Installing Exchange 2019 on a computer that's running Nano Server isn't supported. 

**Supported Powershell versions for Exchange 2019 servers**

Exchange 2019 servers support the version of PowerShell that's included in the release of Windows Server where Exchange is installed. Don't install stand-alone downloads of WMF or PowerShell on Exchange servers.

 **Installing other software on Exchange 2019 servers**

We don't support installing Office client or Office server software on Exchange servers (for example, SharePoint Server, Skype for Business Server, Office Online Server, or Project Server). Other software that you want to install on Exchange 2019 servers needs to be designed to run on the same computer as Exchange.

## .NET Framework

We strongly recommend that you use the latest version of the .NET Framework that's supported by the release of Exchange you're installing.

> [!IMPORTANT]
> **Releases of .NET Framework that aren't listed in the table below aren't supported on any release of Exchange 2019**. This includes minor and patch-level releases of .NET Framework.

|**Exchange version**|**.NET Framework 4.7.2**|
|:-----|:-----|
|Exchange 2019 RTM|Supported|
 
## Supported clients

- Outlook 2019

- Outlook 2016

- Outlook 2016 for Mac

- Outlook for Mac for Office 365

## Skype For Business integration

If integrating Skype for Business presence and instant messaging with Exchange Server, Skype for Business 2013 Cumulative Update 1 or later is required.

## Exchange third-party clients

Exchange Server offers several well-known protocols, and publishes APIs that third-party vendors often write clients for.

Microsoft makes no warranties, expressed or implied, as to the overall suitability, fitness, compatibility, or security of clients that are created by third-party developers.

If you want to use a third-party client that uses our protocols or APIs, we recommend that you thoroughly review and test all considerations (functionality, security, maintenance, management, and so on) before you deploy the client in the enterprise workspace. We also recommend that you make sure that the third-party vendor offers an appropriate Enterprise Support Agreement (ESA).
  

