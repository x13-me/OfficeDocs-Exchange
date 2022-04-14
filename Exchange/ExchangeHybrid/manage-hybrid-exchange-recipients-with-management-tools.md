---
ms.localizationpriority: medium
description: 'Manage on-premises recipients in Exchange Server 2019 Hybrid Environments using Exchange Server Management tools.'
ms.topic: how-to
author: JoanneHendrickson
ms.author: jhendr
ms.assetid: 928a4a0b-0082-4d50-a696-bfaf2782f42d
ms.reviewer: 
title: "Manage recipients in Exchange Server 2019 Hybrid environments"
ms.collection:
- Strat_EX_Admin
- exchange-server
f1.keywords:
- NOCSH
audience: ITPro
ms.prod: exchange-server-it-pro
manager: serdars

---
# Manage recipients in Exchange Server Hybrid environments using Exchange Server Management tools

If you keep an Exchange server running just for recipient management, you may be able to shut down your last Exchange server and manage recipients using Windows PowerShell.

>[!Note]
>This feature is only available for Exchange Server 2019 April 2020 Cumulative Update or higher.

## Overview

In Exchange Hybrid environments, you must have an active Exchange Server to manage recipients attributes. First, attributes are edited using an Exchange Server in on-premises Active Directory (AD), that are then copied to Azure AD using directory synchronization. On-premises recipients can’t be modified directly in Azure Active Directory (Azure AD) or Exchange Online. Therefore customers have to keep an Exchange Server running using directory synchronization via AAD Connect tool.
 
## Will this work for me?

An updated version of the Exchange Management Tools is now available that eliminates the need for a running Exchange server if all of the following are true:

- Have migrated all mailboxes and public folders to Exchange Online 
- Use AD for recipient management and Azure AD Connect for synchronization
- Don't use/require the on-premises Exchange admin center or Exchange Role-Based Access Control (RBAC)
- Are comfortable with using only Windows PowerShell for recipient management
- Don't require auditing or logging of recipient management activity
- Run only one Exchange server and only for recipient management purposes
- Want to manage recipients without running any Exchange servers.

With the updated Exchange Management Tools, domain admins and members of the Recipient Management EMT group can use Windows PowerShell to run the following cmdlets without a running Exchange server:

- -MailUser
- -MailContact
- -RemoteMailbox
- -DistributionGroup (excluding Upgrade-DistributionGroup)
- -DistributionGroupMember
- -EmailAddressPolicy
- -User 

>[!Note]
> You can't modify on-premises recipients directly in Azure AD or Exchange Online. 

### Prerequisites

- Exchange Server 2019 April 2020 Cumulative Update or higher

## Verify that Management Tools can run without Exchange Server

If your environment includes only a single Exchange server running solely because of recipient management requirements, use the steps below to test the Management Tools update.

### Prepare the Exchange Environment

1. Verify that all mailboxes are in the cloud by running the following commands in the Exchange Management Shell:

•	Set-AdServerSettings -ViewEntireForest $true
•	Get-Mailbox

>[!Note]
>Built-in admin mailboxes are not synced to cloud through Azure AD Connect by default. Before you proceed, you should disable these mailboxes using Disable-Mailbox.

2. Verify that the Exchange Online tenant coexistence domain (usually something like “contoso.mail.onmicrosoft.com”) is configured as target delivery domain by running the following command:

```powershell
Get-RemoteDomain Hybrid* | fl DomainName,TargetDeliveryDomain

```

If the coexistence domain is not added as a remote domain, you can add it using New-RemoteDomain. For example:

```powershell

New-RemoteDomain -Name 'Hybrid Domain - M365B434489.mail.onmicrosoft.com' -DomainName 'M365B434489.mail.onmicrosoft.com'

```

If it isn't set as the Target Delivery Domain, you can set it using *Set-RemoteDomain*. For example:

```powershell

Set-RemoteDomain -TargetDeliveryDomain: $true -Identity 'Hybrid Domain - M365B434489.mail.onmicrosoft.com'

```
>[!Note]
>In you have already removed Exchange Server or never had an Exchange Server to start with, Set-Remotedomain and New-RemoteDomain cmdlets can be accessed via Microsoft.Exchange.Management.PowerShell.E2010 snapin. Add the snapin before using the *remotedomain cmdlets.

3. Install the Exchange Management Tools role using the package you downloaded from the TAP site. The updated tools can be installed on any domain-joined computer in an Exchange organization, and can be used in organizations running Exchange Server 2013, Exchange Server 2016, and/or Exchange Server 2019. 

>[!Note]
>Installing the updated Exchange Management Tools in an environment with only Exchange 2013 and/or Exchange 2016 will upgrade the Exchange organization to Exchange Server 2019, and it will perform an AD schema update. If you have a large AD deployment, or if a separate team manages AD, use the steps here to perform the schema update.

4. Install the Windows Remote Server Administration Tools using the steps here.

5. If you have the Scripting Agent enabled, copy **ScriptingAgentConfig.xml** from *$env:ExchangeInstallPath\Bin\CmdletExtensionAgents* on the Exchange Server, to the *$env:ExchangeInstallPath\Bin\CmdletExtensionAgents* folder on the computer with the Management Tools update installed.

7. Run the provided script to create the Recipient Management EMT security group that grants users without Domain admin rights to manage recipients.
a)	Sign-in to the computer with the Management Tools update as a Domain Admin and open Windows PowerShell.
b)	Load the Recipient Management snap-in by running Add-PSSnapin *RecipientManagement.
c)	Run Add-PermissionForEMT.ps1 from the $env:ExchangeInstallPath\Scripts folder.
The script creates a security group called Recipient Management EMT. Members of this group have recipient management permissions. All admins without domain admin rights need to perform recipient management should be added to this security group.
7.	Sign in to the computer with the Management Tools update with the appropriate permissions (domain admin or member of Recipient Management EMT) and load the Recipient Management snap-in by running Add-PSSnapin *RecipientManagement. 

This step must be performed every time you manage recipients.

8.	Test all recipient management cmdlets and verify that you see expected results.
9.	Shut down your last Exchange server and verify that all recipient management cmdlets still work as expected.

## Permanently shutting down your last Exchange Server

If you intend to permanently shut down your last Exchange Server, we recommend that you use the following steps to clean up aspects of your Exchange configuration to improve the security posture of your environment.

>[!Important]
>If you are using your last Exchange server for any purpose other than recipient management (e.g., for SMTP relay), then do not shut it down.

1. Turn on your last Exchange server.
2. Clean up your hybrid configuration by performing Steps 1 to 8 for Scenario 2 in How and when to decommission your on-premises Exchange servers in a hybrid deployment
3. Remove the Federation Trust by running the following command in the Exchange Management Shell:

```powershell
Remove-FederationTrust "Microsoft Federation Gateway" 
```

4. Remove the Federation Certificate:  To find the certificate thumbprint, run: 

```powershell
$fedThumbprint = (Get-ExchangeCertificate | ?{$_.Subject -eq "CN=Federation"}).Thumbprint  
``` 
To remove the certificate thumbprint, run:

```powershell
Remove-ExchangeCertificate –Thumbprint $fedThumbprint
```
5. Remove the service principal credentials created for OAuth. To do this, you need to determine which KeyId matches the key value of the OAuth certificate. To find the KeyId that matches, follow these steps:

a. Run these commands in the Exchange Management Shell to get the OAuth credValue:
```powershell
$thumbprint = (Get-AuthConfig).CurrentCertificateThumbprint 
$oAuthCert = (dir Cert:\LocalMachine\My) | where {$_.Thumbprint -match $thumbprint} 
$certType = [System.Security.Cryptography.X509Certificates.X509ContentType]::Cert 
$certBytes = $oAuthCert.Export($certType) 
$credValue = [System.Convert]::ToBase64String($certBytes) 
```
b. Find the KeyId that is same as the $credValue found above, run the following commands as a tenant admin using the Azure Active Directory Module for Windows PowerShell.

```powershell
Install-Module -Name MSOnline
Connect-MsolService
$ServiceName = "00000002-0000-0ff1-ce00-000000000000" 
$p = Get-MsolServicePrincipal -ServicePrincipalName $ServiceName 
$keyId = (Get-MsolServicePrincipalCredential -AppPrincipalId $p.AppPrincipalId -ReturnKeyValues $true | ?{$_.Value -eq $credValue}).KeyId 
``` 
This gives the KeyId of the key whose value matches the $credValue found above.

c. To remove the service principal credential, run the following command: 

```powershell
Remove-MsolServicePrincipalCredential –KeyIds @($keyId) -AppPrincipalId $p.AppPrincipalId
```
6.	Uninstall the Hybrid agent. If your environment has a Modern Hybrid configuration, follow the steps below to remove it: 

a. On the computer where the Hybrid agent is installed, import the Hybrid Management PowerShell module. Then run:
a.	C:\Program Files\Microsoft Hybrid Service\HybridManagement.psm1 
b.	To remove the App, an AppId is required. Use any of the following cmdlets in Exchange Online PowerShell to find the AppId.  

```powershell
Get-OrganizationRelationship ((Get-OnPremisesOrganization).OrganizationRelationship) | Select-Object TargetSharingEpr 
```
The output looks like this:

```powershell
TargetSharingEpr
----------------
https://6ca7c832-49a2-4a5d-aeae-a616f6d4b8e7.resource.mailboxmigration.his.msappproxy.net/EWS/Exchange.asmx
----------------
https://6ca7c832-49a2-4a5d-aeae-a616f6d4b8e7.resource.mailboxmigration.his.msappproxy.net/EWS/Exchange.asmx
```

Or, run:

```powershell
Get-MigrationEndpoint "Hybrid Migration Endpoint - EWS (Default Web Site)" | Select-Object RemoteServer
```
The output looks like this:

```powershell 
RemoteServer
------------
6ca7c832-49a2-4a5d-aeae-a616f6d4b8e7.resource.mailboxmigration.his.msappproxy.net
```
In this example, 6ca7c832-49a2-4a5d-aeae-a616f6d4b8e7 is the AppId to be used in the next step.

c. Remove the App by running:

```powershell
Remove-HybridApplication -appId 6ca7c832-49a2-4a5d-aeae-a616f6d4b8e7 -Credential (Get-Credential)
```

>[!Note]
>The AppId is 6ca7c832-49a2-4a5d-aeae-a616f6d4b8e7 only for this example; your value will be different).

d.	Uninstall the Hybrid agent using the steps here. 
7.	If not already done, point your MX and Autodiscover DNS records to Exchange Online. This is important to ensure mail flow isn't affected. For more information, see External Domain Name System records for Office 365. 

8.	Shut down your last Exchange server.

## Active Directory clean up

If you plan to never run Exchange Server on-premises, we recommend that you clean up your Active Directory by removing unnecessary Exchange objects. 

>[!Important]
>This step can’t be undone, so only proceed if you **never** want to run Exchange Server again.
 
AD cleanup can be done using the CleanupActiveDirectoryEMT script shipped with Management tools. The script removes system mailboxes, unnecessary Exchange containers, permissions for Exchange Security Groups on the domain and configuration partitions, and the Exchange Security Groups.

This script is available at: *$env:ExchangeInstallPath\Scripts\CleanupActiveDirectoryEMT.ps1*

### Important: Be Aware

**Once you shut down the last Exchange server, Exchange RBAC will no longer function**. Users who were a part of Exchange Recipient groups or had custom Exchange roles allowing for recipient management will no longer have permission. Only domain admins and users who are assigned permission using Add-PermissionForEMT.ps1 script will be able to perform recipient management.

Once you shut down your last Exchange server and perform the Exchange hybrid and Active Directory cleanup steps listed above, you can erase and reformat your last Exchange server.
