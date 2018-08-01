---
title: "Install Exchange 2016 or Exchange 2019 using unattended mode"
ms.author: dstrome
author: dstrome
manager: serdars
ms.date: 6/8/2018
ms.audience: ITPro
ms.topic: get-started-article
ms.prod: exchange-server-it-pro
localization_priority: Priority
ms.collection: Strat_EX_Admin
ms.assetid: 386465e9-41da-4e26-9816-b3b69be1f8bf
description: "Summary: Learn how to perform an unattended setup of Exchange 2016 or Exchange 2019 from the command line."
---

# Install Exchange 2016 or Exchange 2019 using unattended mode

 **Summary**: Learn how to perform an unattended setup of Exchange 2016 or Exchange 2019 from the command line.
  
Running Exchange Setup from the command line allows you to automate the installation of Exchange do and other related tasks on Exchange servers (for example, remove an existing Exchange server or recover a failed Exchange server). The command line options (switches) that are available in Exchange Setup are described in the following table:

|Switch|Valid values|Default value|Requirements|Description|
|:-----|:-----|:-----|:-----|:-----|
|_/IAcceptExchangeServerLicenseTerms_|n/a|n/a|Always|This switch is required whenever you run Setup.exe with any additional switches. If you don't use this switch in the command, you'll get an error.|
|_/Mode:\<InstallationMode\>_ <br/> (*/m:\<InstallationMode\>*\)|_Install_, _Uninstall_, _Upgrade_, or _Recover_<sup>*</sup>|_Install_|n/a|• **Install**: Installs Exchange on a new server using the Exchange server roles specified by the _/Roles_ switch. <br/>• **Uninstall**: Uninstalls Exchange from a working server. <br/>• **Upgrade**: Installs a Cumulative Update (CU) on an Exchange server. <br/>• **RecoverServer**: Recovers an Exchange server using the existing Exchange server object in Active Directory after a catastrophic hardware or software failure on the server. After you install a new Windows server with the same FQDN as the failed Exchange server, you use this switch/value combination to reinstall and recreate the Exchange server on the new computer (don't use the _/Roles_ switch). After you recover the server, you can restore databases and reconfigure any additional settings.|
|_/Roles:\<ServerRole\>_ <br/> (_/Role:\<ServerRole\>_) <br/> (*/r:\<ServerRole\>*)|_Mailbox_, _EdgeTransport_, or _ManagementTools_|n/a|Required with `/Mode:Install`|• **Mailbox (or mb)**: Installs the Mailbox server role and the Exchange management tools. You can't use this value with **EdgeTransport**. <br/>• **EdgeTransport (or et)**: Installs the Edge Transport server role and the Exchange management tools. You can't use this value with **Mailbox**. <br/>• **ManagementTools (or mt or t)**: Installs the Exchange management tools on clients or other Windows servers.|
|_/DisableAMFiltering_|n/a|n/a|Optional with `/Mode:Install /Roles:Mailbox`|Disables the built-in Exchange antimalware filtering on Mailbox servers. For more information about antimalware filtering, see [Antimalware protection in Exchange Server](../../antispam-and-antimalware/antimalware-protection/antimalware-protection.md).|
|_/DomainController:<ServerNameOrFQDN>_ <br/> (_/dc:<ServerNameOrFQDN>_)|The server name (for example, DC01) or FQDN (for example, dc01.contoso.com) of the domain controller.|A domain controller in the local Active Directory site of the computer where you're running Setup|Optional with: <br/>• All values of _/Mode_ (except when you're installing an Edge Transport server) <br/>• _/PrepareAD_, _/PrepareSchema_, _/PrepareDomain_ and _/PrepareAllDomains_|Specifies the domain controller that Exchange Setup uses to read from and write to Active Directory. <br/> If you use this switch with _/PrepareSchema_, you need to specify the schema master.|
|_/InstallWindowsComponents_|n/a|n/a|Optional with `/Mode:Install`|Installs the required Windows roles and features for the specified Exchange server role.|
|_/OrganizationName:"\<Organization Name\>"_ <br/> (_/on:"\<Organization Name\>"_)|A text string (for example, "Contoso Corporation").|First Organization|Availalbe only during the installation of the first Exchange server in the organization: <br/>• `/Mode:Install /Roles:Mailbox` <br/>• _/PrepareSchema_ or _/PrepareAD_|The organization name is used internally by Exchange, isn't typically seen by users, doesn't affect the functionality of Exchange, and doesn't determine what you can use for email addresses. <br/>• The organization name can't contain more than 64 characters, and can't be blank. <br/>• Valid characters are A to Z, a to z, 0 to 9, hyphen or dash (-), and space, but leading or trailing spaces aren't allowed. <br/>• You can't change the organization name after it's set.|
|_/TargetDir:"\<Path\>"_ <br/> (_/t:"\<Path\>"_)|A folder path (for example, "D:\Program Files\Microsoft\Exchange").|%ProgramFiles%\Microsoft\Exchange Server\V15|Optional with `/Mode:Install` and `/Mode:Recover`|Specifies where to install Exchange on the server.|
|_/UpdatesDir:"\<Path\>"_ <br/> (_/u:"\<Path\>"_)|A folder path (for example, "D:\Downloads\Exchange Updates").|The Updates folder at the root of the Exchange installation media.|Optional with `/Mode:Install`, `/Mode:Upgrade`, `/Mode:Recover`, _/AddUmLanguagePack_ or _/RemoveUmLanguagePack_.|Specifies the source location of updates for Setup to install. You can only specify one folder for updates.|
|*/ActiveDirectorySplitPermissions:\<True* \| _False\>_|True or False|False|Optional during the installation of the first Exchange server in the organization: `Mode:Install /Roles:Mailbox` or _/PrepareAD_.|Specifies the Active Directory split permissions model when preparing Active Directory. For more information, see the "Active Directory split permissions" section in [Understanding split permissions].(https://technet.microsoft.com/library/dd638106(v=exchg.150).aspx).|
|_AnswerFile:"\<PathAndFileName\>"_ <br/> (_af:"\<PathAndFileName\>"_)|The name and location of a text file (for example,"D:\Server data\answer.txt").|n/a|Available with `/Mode:Install /Roles:Mailbox` (first Exchange server or additional Exchamge servers) or `/Mode:Install /Roles:EdgeTransport`|Use this switch to create a template to install Exchange on multiple computers with the same settings. You can use the following switches in the answer file: _AdamLdapPort_, _AdamSslPort_, _CustomerFeedbackEnabled_, _DbFilePath_, _DisableAMFiltering_, _DoNotStartTransport_, _EnableErrorReporting_, _IAcceptExchangeServerLicenseTerms_, _LogFolderPath_, _Mdbname_, _OrganizatinName_, _TenantOrganizationConfig_, and _UpdatesDir_. Don't use the forward slash character ( / ) with the switches in the answer file.|
|*/CustomerFeedbackEnbled:\<True* \| _False\>_|True or False|False|Optional with `/Mode:Install` and _/PrepareAD_|Specifies whether to allow or prevent Exchange from providing usage feedback to Micrsoft to help improve future Exchange features. You can enable or disable this setting after Exchange setup is complete.|
|_/DbFilePath:"\<Path\>"_|A folder path (for example, "D:\Exchange Database Files").|%ExchangeInstallPath%Mailbox\Mailbox Database \<10DigitNumber\> where %ExchangeInstallPath% is %ProgramFiles%\Microsoft\Exchange Server\V15\Mailbox or the location you specified with the _/TargetDir_ switch.|Optional with `/Mode:Install /Roles:Mailbox`|Specifies the location of the first mailbox database that's created on the new Mailbox server. You can specify the name of the database file with the _/MdbName_ switch and the location of the database transaction log files with the _/LogFolderPath_ switch.|
|_/DoNotStartTransport_|n/a|n/a|Optional with `/Mode:Install /Roles:Mailbox`, `/Mode:Install /Roles:EdgeTransport`, and `/Mode:Recover`.|Tells Setup to not start the Microsoft Exchange Transport service (mail flow) on Mailbox servers or Edge Transport servers after Setup is complete. You can use this switch to do additional configuration before the servr accepts email messages (for example, configure antispam agents or move the queue database back onto a recovered Exchange server.)|
|_/EnableErrorReporting_|n/a|n/a|Optional with `/Mode:Install` and `/Mode:Recover`.|Specifies whether to allow Exchange to automatically checking online for solutions to errors that it encounters. You can enable or disable this setting after Exchange setup is complete.|
|_/LogFolderPath:"\<Path\>"_|A folder path (for example, "E:\Exchange Database Logs").|%ExchangeInstallPath%Mailbox\Mailbox Database \<10DigitNumber\> where %ExchangeInstallPath% is %ProgramFiles%\Microsoft\Exchange Server\V15\Mailbox or the location you specified with the _/TargetDir_ switch.|Optional with `/Mode:Install /Roles:Mailbox`.|Specifies the location of the transaction log files for the first mailbox database that's created on the new Mailbox server. You can specify the location of the database files with the _/DbFilePath_ switch.|
|_/MdbName:"\<FileName\>.edb"_|An .edb filename (for example, "db01.edb")|Mailbox Database \<10DigitNumber\>.edb (for example, Mailbox Database 0139595516.edb)|Optional with `/Mode:Install /Roles:Mailbox`.|Specifies the name of the first mailbox database that's created on the new Mailbox server. You can specify the location of the database files with the _/DbFilePath_ switch.|
|_/TenantOrganizationConfig:"\<Path\>"_|A folder path (for example "C:\Data")|n/a|Required in hybrid deployments with `/Mode:Install` or _/PrepareAD_.|Used in hybrid deployments between on-premises organizations and Office 365. Specifies the location of the file that contains the configuration information for your Office 365 organization. You create this file by running the **Get-OrganizationConfig** cmdlet in Exchange Online PowerShell in your Office 365 organization.|

For more information about planning for Exchange 2016 or Exchange 2019, see [Planning and deployment for Exchange Server](../../plan-and-deploy/plan-and-deploy.md).
  
We recommend that the Edge Transport role be installed in a perimeter network outside of your organization's internal Active Directory forest. While you can install the Edge Transport server role on a domain-joined computer, doing so will only enable domain management of Windows features and settings. The Edge Transport role itself doesn't use Active Directory. Instead, it uses the Active Directory Lightweight Directory Services (AD LDS) Windows feature to store configuration and recipient information. For more information about the Edge Transport role, see [Edge Transport servers](../../architecture/edge-transport-servers/edge-transport-servers.md).
  
> [!NOTE]
> The Edge Transport role can't be installed on the same computer as the Mailbox server role.
  
For information about tasks to complete after installation, see [Exchange 2016 post-installation tasks](../../plan-and-deploy/post-installation-tasks/post-installation-tasks.md).
  
## What do you need to know before you begin?

The following information applies to both the Mailbox and Edge Transport server roles.
  
- Make sure you've read the release notes prior to installing Exchange 2016. For more information, see [Release notes for Exchange 2016](../../release-notes.md).
    
- The computer you install Exchange 2016 on needs to have a supported operating system, have enough disk space, and satisfy other requirements. For information about system requirements, see [Exchange 2016 system requirements](../../plan-and-deploy/system-requirements.md).
    
- To run Exchange 2016 setup, you need to install various Windows roles and features, .NET Framework 4.5.2 or later, and other required software. To understand the prerequisites for all server roles, see [Exchange 2016 prerequisites](../../plan-and-deploy/prerequisites.md).
    
- For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](../../about-documentation/exchange-admin-center-keyboard-shortcuts.md).
    
> [!CAUTION]
> After you install Exchange 2016 on a server, you must not change the server name. Renaming a server after you have installed an Exchange 2016 server role is not supported.
  
The following information applies to the Exchange 2016 Mailbox server role.
  
- Estimated time to complete: 60 minutes
    
- The computer you install Exchange 2016 on must be a member of an Active Directory domain.
    
- If you're installing the first Exchange 2016 server in the organization, the account you use needs to be a member of the Enterprise Admins group.
    
- If you haven't previously prepared the Active Directory schema, the account you use also needs to be a member of the Schema Admins group.
    
- If you've already prepared the schema and aren't installing the first Exchange 2016 server in the organization, the account you use needs to be a member of the Exchange 2016 Organization Management role group.
    
    Administrators who are members of the Delegated Setup role group can deploy Exchange 2016 servers that have been previously provisioned by a member of the Organization Management role group.
    
The following information applies to the Exchange 2016 Edge Transport server role.
  
- Estimated time to complete: 40 minutes
    
- You need to configure the primary DNS suffix on the computer. For example, if the fully qualified domain name of your computer is edge.contoso.com, the DNS suffix for the computer is contoso.com. For more information, see [Primary DNS Suffix is missing [ms.exch.setupreadiness.FqdnMissing]](../../plan-and-deploy/deployment-ref/ms-exch-setupreadiness-fqdnmissing.md).
    
- Exchange 2010 Hub Transport servers need an update before you can create an EdgeSync Subscription between them and an Exchange 2016 Edge Transport server. If you don't install this update, the EdgeSync Subscription won't work correctly. For more information, see the "Supported coexistence scenarios" section in [Exchange 2016 system requirements](../../plan-and-deploy/system-requirements.md).
    
- Make sure the account you use is a member of the local Administrators group on the computer you're installing the Edge Transport role.
    
## Use Setup.exe to install Exchange 2016 in unattended mode

1. Log on to the computer on which you want to install Exchange 2016.
    
2. Download the Exchange 2016 installation files from the [Microsoft Download Center](https://go.microsoft.com/fwlink/p/?LinkId=627251).
    
3. Navigate to the network location of the Exchange 2016 installation files.
    
4. At the command prompt, run the applicable command for your organization.
    
    > [!IMPORTANT]
    > If you have User Access Control (UAC) enabled, you must run `Setup.exe` from an elevated command prompt.
  
  ```
  Setup.exe 
  [/SourceDir:<source directory>]
  
  
  [/AddUmLanguagePack:<UM language pack name>] 
  [/RemoveUmLanguagePack:<UM language pack name>] 
  [/NewProvisionedServer:<server>] [/RemoveProvisionedServer:<server>] 

  ```

5. Setup copies the setup files locally to the computer on which you're installing Exchange 2016.
    
6. Setup checks the prerequisites, including all prerequisites specific to the server roles that you're installing. If you haven't met all the prerequisites, Setup fails and returns an error message that explains the reason for the failure. If you've met all the prerequisites, Setup installs Exchange 2016.
    
7. Restart the computer after Exchange 2016 has completed.
    
8. Complete your deployment by performing the tasks provided in [Exchange Server post-installation tasks](../../plan-and-deploy/post-installation-tasks/post-installation-tasks.md).
    
## Examples

The following are examples of using Setup.exe:
  
- **Setup.exe /mode:Install /role:Mailbox /OrganizationName:MyOrg /IAcceptExchangeServerLicenseTerms**
    
    This command creates an Exchange 2016 organization in Active Directory called MyOrg, installs the Mailbox server role and the management tools, and also accepts the Exchange 2016 licensing terms.
    
- **Setup.exe /mode:Install /role:Mailbox /TargetDir:"C:\Exchange Server" /IAcceptExchangeServerLicenseTerms**
    
    This command installs the Mailbox server role and the management tools in the "C:\Exchange Server" directory. This command assumes an Exchange 2016 organization has already been prepared.
    
- **Setup.exe /mode:Install /r:MB /IAcceptExchangeServerLicenseTerms**
    
    This command installs the Mailbox server role and the management tools in the default installation location.
    
- **Setup.exe /mode:Install /r:EdgeTransport /IAcceptExchangeServerLicenseTerms**
    
    This command installs the Edge Transport server role and the management tools in the default installation location.
    
- **Setup.exe /mode:Install /r:ET /IAcceptExchangeServerLicenseTerms**
    
    This command installs the Edge Transport server role and the management tools in the default installation location.
    
- **Setup.exe /mode:Uninstall /IAcceptExchangeServerLicenseTerms**
    
    This command completely removes Exchange 2016 from the server and removes this server's Exchange configuration from Active Directory.
    
- **Setup.exe /PrepareAD /on:"My Org" /IAcceptExchangeServerLicenseTerms**
    
    This command creates an Exchange organization called My Org and prepares Active Directory for Exchange 2016.
    
- **Setup.exe /role:Mailbox /UpdatesDir:"C:\ExchangeServer\New Patches" /IAcceptExchangeServerLicenseTerms**
    
    This command updates ExchangeServer.msi with patches from the specified directory, and then installs the Mailbox server role and the management tools. If a language pack bundle is included in this directory, the language pack is also installed.
    
- **Setup.exe /mode:Install /role:Mailbox /DomainController:DC01 /IAcceptExchangeServerLicenseTerms**
    
    This command uses the domain controller DC01 to query and make changes to Active Directory while installing Mailbox server role and the management tools.
    
- **Setup.exe /mode:Install /role:Mailbox /AnswerFile:c:\ExchangeConfig.txt /IAcceptExchangeServerLicenseTerms**
    
    This command installs the Mailbox server role by using the settings in the ExchangeConfig.txt file.
    
- **Setup.exe /rprs:Exchange03 /IAcceptExchangeServerLicenseTerms**
    
    This command removes the object Exchange03 from Active Directory.
    
- **Setup.exe /AddUmLanguagePack:ko-KR /IAcceptExchangeServerLicenseTerms**
    
    This command installs the Korean Unified Messaging language pack from the %ExchangeSourceDir%\ServerRoles\UnifiedMessaging directory.
    
## How do you know this worked?

To verify that you've successfully installed Exchange 2016, see [Verify an Exchange 2016 installation](../../plan-and-deploy/post-installation-tasks/verify-installation.md).
  
Having problems? Ask for help in the Exchange forums. Visit the forums at: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkId=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkId=267542), or [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkId=285351).
