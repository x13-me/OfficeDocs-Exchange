---
ms.localizationpriority: high
description: Diagnostic Data collected for Exchange Server
ms.topic: overview
author: joannehendrickson
ms.author: jhendr
ms.reviewer: 
title: Diagnostic Data collected for Exchange Server
ms.collection:
- Strat_EX_Admin
- exchange-server
f1.keywords:
- NOCSH
audience: ITPro
ms.prod: exchange-server-it-pro
manager: serdars
---
# Diagnostic Data collected for Exchange Server

Microsoft collects diagnostic data to keep Exchange Server secure and up to date, find and fix problems, and identify and mitigate threats. When Exchange Server 2016 or 2019 September 2021 (or a later) CU is installed, the Server will have the ability to send diagnostic data related to Exchange Security to Office Config Service in cloud. There is a change to the License Agreement acceptance process to allow you to choose whether to share diagnostic data with Microsoft.  

## Change in License Term acceptance process 

When using the GUI version of the Exchange setup, a new License Agreement screen, as shown below. 

![New Exchange server license agreement](../../media/exchange-license-acceptance-new.png)


Choose one of the following:  

|Option|Explanation|
|:-----|:-----|
|**I accept the license agreement and will share diagnostic data with Microsoft**|This is the default option which accepts the license agreement and enables sending data to Microsoft.|  
|**I accept the license agreement, but I’m not ready to share diagnostic data with Microsoft**| This option accepts the license agreement but disables sending data to Microsoft.| 
|**I do not accept the license agreement**|If you don’t accept the EULA, you cannot install the CU.|


These options are also available via an unattended command-line setup using the new setup switches:  

|Option|Explanation|
|:-----|:-----|
|**/IAcceptExchangeServerLicenseTerms_DiagnosticDataON**|Use this switch to accept the license terms and send optional data to Microsoft when the EM service requests mitigations.|  
|**/IAcceptExchangeServerLicenseTerms_DiagnosticDataOFF**|**Use this new Setup switch to accept the license terms and disable sending optional data to Microsoft.|  

 

>[!Important]
>**/IAcceptExchangeServerLicenseTerms** has been removed from Exchange server command-line Setup and replaced with the two new setup switches shown above.  

 

## Diagnostic Data collected 

When diagnostic data collection is enabled, your Exchange server sends the following information to the Office Config Service: 

|Data|Explanation|
|:-----|:-----|
|Exchange build number|The server version (CU and SU build information)|  
|Emergency Mitigation service state|Information about the admin-configured behavior of the EM service (for example, whether to send data and/or automatically mitigate). | 
|Immutable Device ID|Unique identification for the Server |
|Immutable Org ID|Unique identification for each Exchange organization|
|Applied mitigations|A list of all mitigations that were applied| 
|Blocked mitigations|A list of all mitigations that were blocked by an admin.|  

 
## How to configure the Diagnostic Data setting after installation is complete 

After the setup has completed, you can enable and disable sending the diagnostic data to the OCS on any Exchange server using **Set-ExchangeServer** cmdlet. 


To disable sending optional data to Microsoft: 

```Powershell
Set-ExchangeServer -Identity <ServerName> -DataCollectionEnabled:$false  
```
 

To enable sending optional data to Microsoft, use the following cmdlet: 

```Powershell
Set-ExchangeServer -Identity <ServerName> -DataCollectionEnabled:$true  
```
 
```Powershell
Set-ExchangeServer -Identity <ServerName> -DataCollectionEnabled:$false  
```
 

To enable sending optional data to Microsoft, use the following cmdlet:  

```Powershell
Set-ExchangeServer -Identity <ServerName> -DataCollectionEnabled:$true  
```