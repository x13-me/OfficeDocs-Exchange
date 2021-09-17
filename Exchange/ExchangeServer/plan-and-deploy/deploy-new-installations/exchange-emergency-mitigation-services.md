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

The Exchange Emergency Mitigation (EM) service collects and sends diagnostic data to Microsoft using the Mitigation Service Cloud endpoint.  It helps keep Exchange Server secure and up to date, finds and fixes problems, and identifies and mitigates threats. 

The Exchange EM service works using the cloud-based Mitigation Service Endpoint to provide mitigation against security threats. The use of EEMS is optional for customers who want to safeguard their Exchange Servers by automatically applying mitigations to their servers. If your organization doesn't want to use EM, an admin can disable it.

Like any other Exchange service, Exchange EM service runs as a Windows service on your Exchange Server. When you install the September 2021 (or later) CU of Exchange Server 2016 or Exchange Server 2019, EEMS will be installed automatically on servers with the Mailbox role.  EEMS will not be installed on Edge Transport servers. 

Once installed through Exchange Setup, EM service checks the Mitigation Service Cloud Endpoint for available mitigations every hour. 

"A mitigation" is an action or set of actions used to secure an Exchange server from a known threat. If Microsoft learns about a security threat, we create a mitigation for the issue.  That mitigation is sent directly to the Exchange server, which automatically implements the pre-configured settings. The mitigation package is a digitally signed XML file containing configuration settings to mitigate a known security threat. Once downloaded to the Exchange server, the EM service validates the signature to verify that the XML was not tampered with and has the proper issuer, EKU and cert chain. After successful validation, the EM service applies the mitigation(s).

The work performed by the EM service is a temporary, interim mitigation for customers until they can apply the Security Update that fixes the vulnerability. The EM service is not a replacement for Exchange SUs. Still, it is the fastest and easiest way to mitigate the highest risks to Internet-connected, on-premises Exchange servers before updating.


## Prerequisites

The Exchange EM Service needs following prerequisites. If these prerequisites are not already on the Windows Server where Exchange is installed or to be installed, the setup will prompt the admin to install these prerequisites during readiness check as errors.

- IIS URL Rewrite Module
- Universal C Runtime in Windows (KB2999226)


## Connectivity

The Exchange EM Service needs outbound connectivity to the Mitigation Service Cloud Endpoint to provide protection against security threats through mitigations. If the outbound connectivity to the Mitigation Service Cloud Endpoint is not available during installation of Exchange Server, the setup issues a warning during readiness check. 

The EM service can be installed without connectivity, however, to perform the function of downloading and applying the latest mitigations it needs outbound connectivity. Following endpoint should be reachable from the machine on which Exchange Server is installed for EM service to function properly.

|Endpoint|Address|Port|Description|
|:-----|:-----|:-----|:-----|
|Mitigation Service Cloud|officeclient.microsoft.com/*|TCP: 443|Required endpoint for Exchange EM Service|


## Test-MitigationServiceConnectivity script

Admins can verify that an Exchange server has connectivity to the Mitigation Service Cloud endpoint using the **Test-MitigationServiceConnectivity.ps1** script (available in the scripts folder) from the Exchange server.

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
One of the functions of the EM service is downloadding  mitigations from Mitigation Service Cloud endpoint and automatically applying them to the Exchange Server. If your organization has an alternate means of mitigating a known threat periodically, you may choose to disable the auto-apply of mitigations via EM Service. An admin can enable and disable auto-apply functionality of EM Service at an organizational level or at the Exchange server level.
 
- **Set-OrganizationConfig -MitigationsEnabled $false** 
This is used to disable automatic mitigation org-wide. By default, this is set to true. When set to false, the EM service will check for mitigations hourly but won’t automatically apply mitigations to any Exchange server in the organization, regardless of the value of MitigationsEnabled at the server level.

- **Set-ExchangeServer -Identity <ServerName> -MitigationsEnabled $false**
This is used to automatic mitigation on a specific server. By default, this is set to true. When set to false, the EM service checks for mitigations hourly but won’t automatically apply them to the specified server.

The combination of these two settings determines the behavior of the EM service on each Exchange server in the organization, as shown here:

|Org Setting||
|:-----|:-----|:-----|
||	True|	EM will automatically apply mitigations to the Exchange server when both are True.
Server Setting	True	

Org Setting	True	EM will not automatically apply mitigations to a specific Exchange server when the Org setting is True, and the Server setting is False.
Server Setting	False	

Org Setting	False	EM will not automatically apply mitigations to any Exchange server when the Org setting is False.
Server Setting	True or False	


## 	Mitigations
A mitigation is an action or set of actions that are taken automatically to secure an Exchange server from a known threat that is being actively exploited in the wild. This means that to protect your organization and mitigate risk, the EM service may automatically disable features or functionality on an Exchange server. 

The EM service can apply 3 types of mitigations:

- **IIS Rewrite rule mitigation**. This is essentially a rule that blocks specific patterns of malicious *http requests* that can endanger Exchange Server.
- **Exchange service mitigation**. This disables any vulnerable service on the Exchange Server.
- **App Pool mitigation** This disables any vulnerable app pool.

As an admin, you have visibility and control over mitigation already applied using cmdlets and PowerShell scripts. You can find details on applied mitigations and their status using scripts included with EM.  Find details of mitigations blocked by an admin Windows explorer

### Viewing Applied Mitigations

Once mitigations are applied to a server, an admin can view the applied mitigations using following cmdlet. 

```powershell
Get-ExchangeServer -Identity <ServerName> | fl name, MitigationsApplied
Name				: Server1
MitigationsApplied	: {M01.1, M01.2, M01.3}
```


The same cmdlet can also be used to see the list of applied mitigations across your environment as shown below

```powershell
Get-ExchangeServer | fl name, MitigationsApplied
```
Name				:	Server1
MitigationsApplied	: 	{M01.1, M01.2, M01.3}

Name				:	Server2
MitigationsApplied	:	{M01.1, M01.2, M01.3}


## Reapplying a Mitigation
In case of an accidental reversal of a mitigation by an admin, the EM service will reapply the mitigation when it performs its hourly check for new mitigations. Admins can also manually reapply a mitigation without waiting for the EM service to check for mitigations by stopping and then restarting the EM service. After restarting the EM service, the first run to check and apply mitigation occurs after 10 minutes.

### Blocking Mitigations and reversing the Mitigation
If a mitigation critically impacts the functioning of your Exchange Server, the admin can block the mitigation and then manually reverse the effect. 

To block any mitigation, admins need to add the Mitigation ID in the MitigationsBlocked parameter which is shown below:

```powershell
Set-ExchangeServer -Identity <Servername> -MitigationsBlocked @(“M1”)
```

In case there are more than one mitigation to be blocked, please use the following:

```powershell
Set-ExchangeServer -Identity <Servername> -MitigationsBlocked @(“M1”, “M2”)
```
The above operation would block M1 mitigation, which would ensure EM service will not reapply this mitigation in next hourly cycle.

After this based on mitigation type, admins can reverse the effect of Mitigation. To reverse IIS rewrite rule mitigation, admins can delete the rule in IIS. For reversing the Service and App Pool mitigation, admins can just start these service or app pool manually.

Admins can also remove one or more mitigations from the block list by removing the **Mitigation ID** in the **MitigationsBlocked** parameter. 

For example:

```powershell
Set-ExchangeServer -Identity <Servername> -MitigationsBlocked @()
```

After the mitigation is removed from the blocked list, the mitigation can now be reapplied by the EM service in its next run. Admins can manually reapply a mitigation without waiting for the EM service’s next run by stopping and then restarting the EM service. After restart of EM service, the first run to check and apply mitigation occurs after 10 minutes.

>!Important]
>Admins should refrain from making any changes to the **MitigationsApplied** parameter, as it is used by EM service to store and track Mitigation Status.


## Viewing Applied and Blocked Mitigations
Admins can view both mitigations applied as well as blocked for a server or all the servers in organization using the same Get-ExchangeServer cmdlet as explained above. 

For viewing list of applied and blocked mitigations for all the servers, admins can use the cmdlet in following way:

```powershell
Get-ExchangeServer | fl name, MitigationsApplied, MitigationsBlocked
```

Name				:	Server1
MitigationsApplied	: 	{M01.1, M01.3}
MitigationsBlocked	: 	{M01.2}

Name				:	Server2
MitigationsApplied	:	{M01.1, M01.2}
MitigationsBlocked	: 	{M01.3}

Admins can see the list of applied and blocked mitigations on a per-server basis in following way:


```powershell
Get-ExchangeServer -Identity <ServerName> | fl name, *Mitigations*
```
Name				:	Server1
MitigationsEnabled	:	True
MitigationsApplied	: 	{M01.1, M01.3}
MitigationsBlocked	: 	{M01.2}

## Get-Mitigation Script
Admins should use the **Get-Mitigations.ps1** script supplied through the Exchange setup to analyze and keep track of all the mitigations provided by Microsoft. This script is available in the scripts folder “\V15\Scripts” located in the Exchange Server installation directory. The script shows the Mitigation ID, Type and Description of each mitigation. And in addition to showing the list of applied and blocked mitigations it also shows the mitigations that failed to apply through the field state which can be “Applied”, “Blocked” and “Failed”.
This script can be used as shown below. If no parameter is supplied to the script, this will show the status for all the servers in the organization. To view the details of specific server, admins should provide server name in Identity field like “.\Get-Mitigation.ps1 -Identity <Server>”

E.g.:

Admins can export the list of applied mitigations and their descriptions to a CSV file by using the ExportCSV argument of Get-Mitigation.ps1 script as shown below.
.\Get-Mitigation.ps1 -Identity <Server> -ExportCSV “C:\temp\CSVReport.csv”
Important: Get mitigation script needs PowerShell version 4.0 and above to function as designed.

## Removing Mitigations after SU or CU upgrade
After an SU or a CU has been installed, an admin must remove any mitigations that are no longer needed. For example, if Mitigation with ID M1 is no longer relevant after SU upgrade, the EM service will stop applying M1. This mitigation will disappear from the list of applied mitigations. Based on type of mitigations, these can be reversed by admins if required. 

## Audit and Logging

Any mitigations blocked by an admin will be logged in the Windows Event Log. In addition to logging blocked mitigations, the EM service will also log details about service startup, shutdown, and termination (like all services running on Windows), as well as details of its actions and any errors encountered by the EM service. For example, events 1005 and 1006 with a source of MSExchange Mitigation Service will be logged for successful actions such as when a mitigation is applied, and event 1008 with the same source will be logged for any errors that are encountered, such as when the EM service cannot reach the Mitigation Service Cloud Endpoint.
Admins can use Search-AdminAuditLog to review actions taken by an admin, including enabling and disabling automatic mitigations.

The EM service also maintains a separate log file in the MitigationService folder under the Exchange Server installation directory. This log details the tasks performed by the EM service, including fetching mitigations, parsing mitigations, and applying mitigations, as well as details about the information sent to the Mitigation Service Cloud Endpoint if sending diagnostic data is enabled.


## Diagnostic Data
The Exchange EM Service collects and sends diagnostic data to Microsoft using the Mitigation Service Cloud endpoint.  It helps keep Exchange Server secure and up to date, finds and fixes problems, and identifies and mitigates threats. To learn more on what is collected and how to change the Diagnostic Data collection setting, see [Diagnostic Data collected for Exchange Server](diagnostic-data-exchange-server.md). 
