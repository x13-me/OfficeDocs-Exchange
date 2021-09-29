---
ms.localizationpriority: high
description: Exchange Emergency Mitigation Service (Exchange EM Service)
ms.topic: overview
author: joannehendrickson
ms.author: jhendr
ms.reviewer: 
title: Exchange Emergency Mitigation Service (Exchange EM Service)
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

The Exchange Emergency Mitigation service (EM service) is to help keep your Exchange Servers secure by applying mitigations to address any potential threats against your servers. It uses the cloud-based Office Config Service (OCS) to check for and download available mitigations and to send diagnostic data to Microsoft.

The EM service runs as a Windows service on an Exchange Mailbox server. When you install the September 2021 (or later) CU on Exchange Server 2016 or Exchange Server 2019, the EM service will be installed automatically on servers with the Mailbox role. The EM service will not be installed on Edge Transport servers.

The use of the EM service is optional. If you do not want Microsoft to automatically apply mitigations to your Exchange servers, this feature can be disabled.


## 	Mitigations
A mitigation is an action or set of actions that is taken automatically to secure an Exchange server from a known threat that is being actively exploited in the wild. To help protect your organization and mitigate risk, the EM service may automatically disable features or functionality on an Exchange server. 

The EM service can apply 3 types of mitigations:

- **IIS URL Rewrite rule mitigation**. This is a rule that blocks specific patterns of malicious HTTP requests that can endanger an Exchange server.
- **Exchange service mitigation**. This disables a vulnerable service on an Exchange server.
- **App Pool mitigation** This disables a vulnerable app pool on an Exchange server.

You have visibility and control over any applied mitigation by using PowerShell cmdlets and scripts.

### How does it work
If Microsoft learns about a security threat, we may create and release a mitigation for the issue. In that event, the mitigation would besend from the OCS to the EM service as a signed XML file containing the configuration settings used to apply the mitigation. 

After the EM service has been installed, it checks the OCS for available mitigations every hour. The EM service subsequently downloads the XML and validates the signature to verify that the XML was not tampered with by checking the issuer, the Extended Key Usage, and the certificate chain. After successful validation, the EM service applies the mitigation.

Each mitigation is a temporary, interim fix until you can apply the Security Update that fixes the vulnerability. The EM service is not a replacement for Exchange SUs. However, it is the fastest and easiest way to mitigate the highest risks to Internet-connected, on-premises Exchange servers before updating.

### List of mitigations released

The following is the respository of all released mitigations.

|Serial number|Mitigation ID|Description|Lowest version applicable|Highest version applicable|Rollback procedure|
|:-----|:-----|:-----|:-----|:-----|:-----|
 1|PING1|EEMS heartbeat probe. Does not modify any Exchange settings.|Exchange 2019: September 2021 CU</br></br>Exchange 2016: September 2021 CU| - |No rollback required.|


## Prerequisites

If these prerequisites are not already on the Windows Server where Exchange is installed or to be installed, Setup will prompt you to install these prerequisites during the readiness check:

- [IIS URL Rewrite Module](https://www.iis.net/downloads/microsoft/url-rewrite)
- [Universal C Runtime in Windows (KB2999226)](https://support.microsoft.com/en-us/topic/update-for-universal-c-runtime-in-windows-c0514201-7fe6-95a3-b0a5-287930f3560c) for Windows Server 2012 and Windows Server 2012 R2


## Connectivity

The EM service needs outbound connectivity to the OCS to check for and download mitigations. If outbound connectivity to the OCS is not available during the installation of Exchange Server, Setup issues a Warning during readiness check.

While the EM service can be installed without connectivity to the OCS, it must have connectivity to the OCS in order to download and apply the latest mitigations. The OCS must be reachable from the computer on which Exchange Server is installed for the EM service to function correctly.

|Endpoint|Address|Port|Description|
|:-----|:-----|:-----|:-----|
|Office Config Service|officeclient.microsoft.com/*| 443|Required endpoint for the Exchange EM service|

If a network proxy is deployed in the environment for outbound connectivity, admins need to configure the InternetWebProxy parameter using Set-ExchangeServer.

```Powershell

Set-ExchangeServer -Identity <ServerName> -InternetWebProxy <proxy.contoso.com:port>
```

## Test-MitigationServiceConnectivity script

You can verify that an Exchange server has connectivity to the OCS by using the **Test-MitigationServiceConnectivity.ps1** script (available in the Scripts folder) from the Exchange server.

If the server has connectivity, the output is:

```Powershell
Result: Success.
Message: The Mitigation Service endpoint is accessible from this computer.
```

If the server doesn’t have connectivity, the output is:

```Powershell
Result: Failed.
Message: Unable to connect to the Mitigation Service endpoint from this computer. To learn about connectivity requirements, see https://aka.ms/HelpConnectivityEEMS.
```

## Disabling auto apply of Mitigations through EM Service
One of the EM service functions is downloading mitigations from the OCS and automatically applying them to the Exchange Server. If your organization has an alternate means of mitigating a known threat, you may choose to disable automatic applications of mitigations. You can enable or disable automatic mitigation at an organizational level or  Exchange server level.
 
To disable automatic mitigation for your entire organization, the following cmdlet can be used. By default, MitigationsEnabled is set to "True". When set to "False", the EM service still checks for mitigations hourly but won’t automatically apply mitigations to any Exchange server in the organization, regardless of the value of MitigationsEnabled at the server level.

```powershell

Set-OrganizationConfig -MitigationsEnabled $false

```

To disable automatic mitigation on a specific server, use the following cmdlet. By default, MitigationsEnabled is set to "True". When set to "False", the EM service checks for mitigations hourly but won’t automatically apply them to the specified server.

```Powershell
Set-ExchangeServer -Identity <ServerName> -MitigationsEnabled $false
```

The combination of these two settings determines the behavior of the EM service on each Exchange server in the organization, as shown here:

|Org Setting|Server setting|Behavior|
|:-----|:-----|:-----|
|True|True|EM service will automatically apply mitigations to the Exchange server.|
|True|False|EM service will not automatically apply mitigations to a specific Exchange server.|
|False|False|EM service will not automatically apply mitigations to any Exchange server.|

>[!Note]
>The MitigationsEnabled parameter automatically applies to all servers in an organization and is set to True, as soon as the first Exchange server in your organization is upgraded to the September 2021 (or later) CU. This is by design, and only when other Exchange servers in the organization are upgraded with the September 2021 (or later) CU will the EM service honor the value of MitigationsEnabled.  


### Viewing Applied Mitigations

Once mitigations are applied to a server, you can view the applied mitigations using following cmdlet. 

```powershell
Get-ExchangeServer -Identity <ServerName> | fl name, MitigationsApplied
```

```Powershell
Name			:	Server1
MitigationsApplied	:	{M01.1, M01.2, M01.3} 
```

The same cmdlet can also be used to see the list of applied mitigations across your environment as shown below.

```powershell
Get-ExchangeServer | fl name, MitigationsApplied
```

```powershell
Name			:	Server1
MitigationsApplied	:	{M01.1, M01.2, M01.3}

Name			:	Server2
MitigationsApplied	:	{M01.1, M01.2, M01.3}
```

## Reapplying a Mitigation
If you accidentally reverse a mitigation, the EM service will reapply it when it performs its hourly check for new mitigations. To manually reapply any mitigation, restart the EM service. Ten minutes after restarting, the EM service will run its check and apply any mitigations.

### Blocking or Removing Mitigations
If a mitigation critically affects the functioning of your Exchange server, you can block the mitigation and manually reverse it. 

To block any mitigation, add the Mitigation ID in the **MitigationsBlocked** parameter:

```powershell
Set-ExchangeServer -Identity <Servername> -MitigationsBlocked @("M1")
```
The above operation would block M1 mitigation, which would ensure EM service will not reapply this mitigation in next hourly cycle.

If there is more than one mitigation to be blocked, please use the following:

```powershell
Set-ExchangeServer -Identity <Servername> -MitigationsBlocked @("M1", "M2")
```

Blocking a mitigation does not automatically remove it, but after blocking a mitigation, an admin can manually remove it. How a mitigation is removed depends on the type of mitigation. For example, to remove an IIS rewrite rule mitigation, delete the rule in IIS Manager. To remove a service or app pool mitigation, start the service or app pool manually.

You can also remove one or more mitigations from the blocked mitigations list by removing the **Mitigation ID** in the **MitigationsBlocked** parameter in the same cmdlet.

For example:

```powershell
Set-ExchangeServer -Identity <Servername> -MitigationsBlocked @()
```

After a mitigation is removed from the blocked mitigations list, the mitigation will be reapplied by the EM service on its next run. To manually reapply the mitigation, stop and restart the EM service. Ten minutes after restarting, the EM service will run its check and apply any mitigations.

>!Important]
>Refrain from making any changes to the **MitigationsApplied** parameter, as it is used by the EM service to store and track mitigation status.


## Viewing Applied and Blocked Mitigations
You can view both applied and blocked mitigations for all Exchange servers in your organization by using the **Get-ExchangeServer** cmdlet.

To view the list of applied and blocked mitigations for all the servers:

```powershell
Get-ExchangeServer | fl name, MitigationsApplied, MitigationsBlocked
```

```powershell
Name			:	Server1
MitigationsApplied	:	{M01.1, M01.3}
MitigationsBlocked	:	{M01.2}

Name			:	Server2
MitigationsApplied	:	{M01.1, M01.2}
MitigationsBlocked	:	{M01.3}
```

To view the list of applied and blocked mitigations on a per-server basis:


```powershell
Get-ExchangeServer -Identity <ServerName> | fl name, *Mitigations*
```

```powershell
Name			:	Server1
MitigationsEnabled	:	True
MitigationsApplied	:	{M01.1, M01.3}
MitigationsBlocked	:	{M01.2}
```


## Get-Mitigation Script
You can use the **Get-Mitigations.ps1** script to analyze and track the mitigations provided by Microsoft. This script is available in the "\V15\Scripts" folder under the Exchange Server installation directory. 

The script displays the ID, type, description, and status of each mitigation. The list includes any applied, blocked, or failed mitigations.

To view the details of a specific server, provide server name in the Identity field such as <span><span>".\Get-Mitigations.ps1 -Identity <<span><span>Server<span><span>>".  To view the status of all the servers in your organization, simply omit the Identity parameter.

**Example:** Export the list of applied mitigations and their descriptions to a CSV file by using the ExportCSV parameter:

```powershell
.\Get-Mitigations.ps1 -Identity <Server> -ExportCSV "C:\temp\CSVReport.csv"
```

>[!Important]
>The Get-Mitigations script needs PowerShell version 4.0.

## Removing Mitigations after SU or CU upgrade
After an SU or a CU has been installed, an admin must manually remove any mitigations that are no longer needed. For example, if a Mitigation named **M1** is no longer relevant after installing an SU, the EM service will stop applying it, and it will be removed from the list of applied mitigations. Depending on the type of mitigation, it can be removed from the server if required. 

## Audit and Logging

Any mitigations blocked by an admin will be logged in the Windows Application Event Log. In addition to logging blocked mitigations, the EM service also logs details about service startup, shutdown, and termination (like all services running on Windows) and details of its actions and any errors encountered by the EM service. For example, Events 1005 and 1006 with a source of "MSExchange Mitigation Service" will be logged for successful actions such as when a mitigation is applied. Event 1008 with the same source, will be logged for any encountered errors, such as when the EM service cannot reach the OCS.

You can use **Search-AdminAuditLog** to review actions taken by yourself or other admins, including enabling and disabling automatic mitigations.

The EM service maintains a separate log file in the "\V15\Logging\MitigationService" folder under the Exchange Server installation directory. This log details the tasks performed by the EM service, including fetched, parsed, and applied mitigations and details about the information sent to the OCS (if sending diagnostic data is enabled).


## Diagnostic Data
When data sharing is enabled, the EM service sends diagnostic data to the OCS. This data is used to identify and mitigate threats. To learn more about what is collected and how to disable data sharing, see [Diagnostic Data collected for Exchange Server](diagnostic-data-exchange-server.md). 
