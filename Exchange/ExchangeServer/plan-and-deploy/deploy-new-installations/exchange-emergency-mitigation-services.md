---
ms.localizationpriority: high
description: Exchange Emergency Mitigation Service (EEMS)
ms.topic: overview
author: joannehendrickson
ms.author: jhendr
ms.reviewer: 
title: Exchange Emergency Mitigation Service (EEMS)
ms.collection:
- Strat_EX_Admin
- exchange-server
f1.keywords:
- NOCSH
audience: ITPro
ms.prod: exchange-server-it-pro
manager: serdars
---

# Exchange Emergency Mitigation (EM) service

What is it?

The Exchange Emergency Mitigation (EM) service works to keep your Exchange Servers secure by identifying and addressing threats by applying mitigations to your servers using the cloud-based Mitigation Service endpoint. It also is used to collects and sends diagnostic data to Microsoft.

"A mitigation" is an action or set of actions used to secure an Exchange server from a known threat. If Microsoft learns about a security threat, we create a mitigation for the issue. The mitigation is sent directly to the Exchange server, which automatically implements the pre-configured settings. The mitigation package is a digitally signed XML file containing configuration settings to mitigate a known security threat. Once downloaded to the Exchange server, the EM service validates the signature to verify that the XML was not tampered with and has the proper issuer, EKU, and certificate chain. After successful validation, the EM service applies the mitigation.

Each mitigation is a temporary, interim fix until you can apply the Security Update that fixes the vulnerability. The EM service is not a replacement for Exchange SUs. However, it is the fastest and easiest way to mitigate the highest risks to Internet-connected, on-premises Exchange servers before updating.

The Exchange EM service runs as a Windows service on your Exchange Server. When you install the September 2021 (or later) CU of Exchange Server 2016 or Exchange Server 2019, the EM service will be installed automatically on servers with the Mailbox role.  The EM service will not be installed on Edge Transport servers. 

The use of the Exchange EM service is optional. If you do not want to automatically apply mitigations to your servers, this feature can be disabled.

After the EM service has been installed, it checks the Mitigation Service Cloud Endpoint for available mitigations every hour. 


## Prerequisites

If these prerequisites are not already on the Windows Server where Exchange is installed or to be installed, the setup will prompt you to install these prerequisites during the readiness check

- IIS URL Rewrite Module
- Universal C Runtime in Windows (KB2999226)


## Connectivity

The Exchange EM Service needs outbound connectivity to the Mitigation Service Cloud Endpoint to provide protection against security threats through mitigations. If the outbound connectivity to the Mitigation Service Cloud Endpoint is not available during installation of Exchange Server, the setup issues a warning during readiness check. 

While the Exchange EM service can be installed without connectivity, it must have outbound connectivity to download and apply the latest mitigations. This endpoint must be reachable from the computer on which Exchange Server is installed for EM service to function correctly.

|Endpoint|Address|Port|Description|
|:-----|:-----|:-----|:-----|
|Mitigation Service Cloud|officeclient.microsoft.com/*|TCP: 443|Required endpoint for Exchange EM Service|


## Test-MitigationServiceConnectivity script

Verify that an Exchange server has connectivity to the Mitigation Service Cloud endpoint by using the **Test-MitigationServiceConnectivity.ps1** script (available in the scripts folder) from the Exchange server.

If the server has connectivity, the output will be as follows:

```powershell 
Result: Success.
Message: The Mitigation Service endpoint is accessible from this computer.
```

If the server doesn’t have connectivity, the output will be as follows:

```powershell 
Result: Failed.
Message: Unable to connect to the Mitigation Service endpoint from this computer. To learn about connectivity requirements, see https://aka.ms/HelpConnectivityEEMS.
```

## Disabling auto apply of Mitigations through EM Service
One of the Exchange EM service functions is downloading mitigations from the Mitigation Service Cloud endpoint and automatically applying them to the Exchange Server. If your organization has an alternate means of mitigating a known threat periodically, you may choose to disable the "auto apply" of mitigations via the Exchange EM Service. You can enable or disable it at an organizational level or the Exchange server level.
 
- **Set-OrganizationConfig -MitigationsEnabled $false** 
This cmdlet is used to disable automatic mitigation for your entire organization. By default, this is set to "True". When set to "False", the EM service still checks for mitigations hourly but won’t automatically apply mitigations to any Exchange server in the organization, regardless of the value of MitigationsEnabled at the server level.

- **Set-ExchangeServer -Identity <ServerName> -MitigationsEnabled $false**
This is used to automatic mitigation on a specific server. By default, this is set to "True". When set to "False", the EM service checks for mitigations hourly but won’t automatically apply them to the specified server.

The combination of these two settings determines the behavior of the EM service on each Exchange server in the organization, as shown here:

|Org Setting|Server setting|Behavior|
|:-----|:-----|:-----|
|True|True|EM service will automatically apply mitigations to the Exchange server.|
|True|False|EM service will not automatically apply mitigations to a specific Exchange server.|
|False|False|EM service will not automatically apply mitigations to any Exchange server|


## 	Mitigations
A mitigation is an action or set of actions that are taken automatically to secure an Exchange server from a known threat that is being actively exploited in the wild. This means that to protect your organization and mitigate risk, the EM service may automatically disable features or functionality on an Exchange server. 

The EM service can apply 3 types of mitigations:

- **IIS Rewrite rule mitigation**. This is essentially a rule that blocks specific patterns of malicious *http requests* that can endanger Exchange Server.
- **Exchange service mitigation**. This disables any vulnerable service on the Exchange Server.
- **App Pool mitigation** This disables any vulnerable app pool.

As an admin, you have visibility and control over mitigation already applied using cmdlets and PowerShell scripts. You can find details on applied mitigations and their status using scripts included with EM. Find details of mitigations blocked by an admin Windows explorer

### Viewing Applied Mitigations

Once mitigations are applied to a server, you can view the applied mitigations using following cmdlet. 

```powershell
Get-ExchangeServer -Identity <ServerName> | fl name, MitigationsApplied
```
```powershell
Name				: Server1
MitigationsApplied	: {M01.1, M01.2, M01.3}
```


The same cmdlet can also be used to see the list of applied mitigations across your environment as shown below

```powershell
Get-ExchangeServer | fl name, MitigationsApplied
```
```powershell
Name				:	Server1
MitigationsApplied	: 	{M01.1, M01.2, M01.3}

Name				:	Server2
MitigationsApplied	:	{M01.1, M01.2, M01.3}
```

## Reapplying a Mitigation
If you accidentally reverse a mitigation, the EM service will reapply it when it performs its hourly check for new mitigations. To manually reapply any mitigation, stop and restart the EM service. Ten minutes after the restart, the service will run its check and apply any migitations.

### Blocking Mitigations and reversing the Mitigation
If a mitigation critically impacts the functioning of your Exchange Server, you can block the mitigation and manually reverse the effect. 

To block any mitigation, add the Mitigation ID in the **MitigationsBlocked** parameter:

```powershell
Set-ExchangeServer -Identity <Servername> -MitigationsBlocked @(“M1”)
```

If there is more than one mitigation to be blocked, please use the following:

```powershell
Set-ExchangeServer -Identity <Servername> -MitigationsBlocked @(“M1”, “M2”)
```
The above operation would block M1 mitigation, which would ensure EM service will not reapply this mitigation in next hourly cycle.

After this based on mitigation type, you can reverse the effect of the mitigation. To reverse IIS rewrite rule mitigation, delete the rule in IIS. For reversing the Service and App Pool mitigation, start the service or app pool manually.

You can also remove one or more mitigations from the block list by removing the **Mitigation ID** in the **MitigationsBlocked** parameter. 

For example:

```powershell
Set-ExchangeServer -Identity <Servername> -MitigationsBlocked @()
```

After the mitigation is removed from the blocked list, the mitigation can now be reapplied by the EM service in its next run. To manually reapply the mitigation, stop and restart the EM service. Ten minutes after the restart, the service will run its check and apply any migitations.

>!Important]
>Refrain from making any changes to the **MitigationsApplied** parameter, as it is used by EM service to store and track Mitigation Status.


## Viewing Applied and Blocked Mitigations
You can view both applied and blocked mitigations for all the servers in your organization by using the **Get-ExchangeServer** cmdlet.

To view the list of applied and blocked mitigations for all the servers:

```powershell
Get-ExchangeServer | fl name, MitigationsApplied, MitigationsBlocked
```
```powershell
Name				:	Server1
MitigationsApplied	: 	{M01.1, M01.3}
MitigationsBlocked	: 	{M01.2}

Name				:	Server2
MitigationsApplied	:	{M01.1, M01.2}
MitigationsBlocked	: 	{M01.3}
```

To view the list of applied and blocked mitigations on a per-server basis:


```powershell
Get-ExchangeServer -Identity <ServerName> | fl name, *Mitigations*
```


```powershell
Name				:	Server1
MitigationsEnabled	:	True
MitigationsApplied	: 	{M01.1, M01.3}
MitigationsBlocked	: 	{M01.2}
```


## Get-Mitigation Script
Use the **Get-Mitigations.ps1** script supplied through the Exchange setup to analyze and keep track of all the mitigations provided by Microsoft. This script is available in the “\V15\Scripts” folder located in the Exchange Server installation directory. 

The script displays the ID, type, description, and status of each mitigation. The list includes any applied, blocked, or failed mitigations.

To view the details of a specific server, provide server name in the Identity field such as “.\Get-Mitigation.ps1 -Identity <Server>”.  To view the status of all the servers in your organization, simply remove the parameter.

**Example:** Export the list of applied mitigations and their descriptions to a CSV file by using the ExportCSV argument of Get-Mitigation.ps1 script:

```powershell
.\Get-Mitigation.ps1 -Identity <Server> -ExportCSV “C:\temp\CSVReport.csv”
```

>[!Important]
>The Get mitigation script needs PowerShell version 4.0.

## Removing Mitigations after SU or CU upgrade
After an SU or a CU has been installed, an admin must remove any mitigations that are no longer needed. For example, if Mitigation with ID M1 is no longer relevant after SU upgrade, the EM service will stop applying M1. This mitigation will disappear from the list of applied mitigations. Depending on the type of mitigation, it can be reversed if required. 

## Audit and Logging

Any mitigations blocked by you will be logged in the Windows Event Log. In addition to logging blocked mitigations, the EM service also logs details about service startup, shutdown, and termination (like all services running on Windows) and details of its actions and any errors encountered by the EM service. For example, Events 1005 and 1006 with a source of "MSExchange Mitigation Service" will be logged for successful actions such as when a mitigation is applied. Event 1008, which has the same source, will be logged for any encountered errors, such as when the EM service cannot reach the Mitigation Service Cloud Endpoint.

View the **Search-AdminAuditLog** to review actions taken by yourself or other admins, including enabling and disabling automatic mitigations.

The EM service maintains a separate log file in the **MitigationService** folder under the Exchange Server installation directory. This log details the tasks performed by the EM service, including fetched, parsed, and applied mitigations and details about the information sent to the Mitigation Service Cloud Endpoint if sending diagnostic data is enabled.


## Diagnostic Data
The Exchange EM Service collects and sends diagnostic data to Microsoft using the Mitigation Service Cloud endpoint.  It helps keep Exchange Server secure and up to date, finds and fixes problems, and identifies and mitigates threats. To learn more on what is collected and how to change the Diagnostic Data collection setting, see [Diagnostic Data collected for Exchange Server](diagnostic-data-exchange-server.md). 
