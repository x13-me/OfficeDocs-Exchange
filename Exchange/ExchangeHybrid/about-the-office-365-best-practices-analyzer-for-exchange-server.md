---
title: "About the Office 365 Best Practices Analyzer for Exchange Server"
ms.author: chrisda
author: chrisda
manager: serdars
ms.audience: Admin
ms.topic: article
ms.service: exchange-online
localization_priority: Normal
ms.collection: Adm_O365
ms.custom:
- Adm_O365
- httpsfix
- MiniMaven
search.appverid:
- MET150
- MOE150
ms.assetid: c137e46e-c05d-4bdc-b968-67fe5ae68765
description: "The Office 365 Best Practices Analyzer is an automated tool that evaluates the health and readiness of your on-premises Exchange environment. You can run the Office 365 Best Practices Analyzer at any time to assess the state of your Exchange configuration."
---

# About the Office 365 Best Practices Analyzer for Exchange Server

The Office 365 Best Practices Analyzer is an automated tool that evaluates the health and readiness of your on-premises Exchange environment. You can run the Office 365 Best Practices Analyzer at any time to assess the state of your Exchange configuration.
  
## Overview

You can use the Office 365 Best Practices Analyzer in the following environments:
  
- On-premises Exchange server only (Exchange 2013 or later)
    
- Hybrid configuration (with Exchange 2013 or later)
    
You'll need an Office 365 or Azure Active Directory user ID to install and use the tool. After you have installed and run the Office 365 Best Practices Analyzer, you won't be required to sign-in to the Office 365 admin center to re-run the checks (although you might be prompted to sign-in again).
  
## How to use the Office 365 Best Practices Analyzer

|**Task**|**Actions**|
|:-----|:-----|
|Step 1: Log on and sign in  <br/> | Remote Desktop into your on-premises Exchange server and open the Exchange admin center (EAC). For example, https://localhost/ecp.  <br/>  If you're an Office 365 Enterprise or Office 365 Midsize Business admin:  <br/>  Open Internet Explorer and browse to the [About the Office 365 admin center](https://support.office.com/article/758befc4-0888-4009-9f14-0d147402fd23).  <br/> [About the Office 365 admin center](https://support.office.com/article/758befc4-0888-4009-9f14-0d147402fd23) with your Office 365 user ID.  <br/>  If you don't have Office 365 yet, you can sign up [here](https://products.office.com/en-us/business/get-latest-office-365-for-your-business-with-2016-apps?wt.srch=1&amp;wt.mc_id=AID522514_SEM_5SOqeNbs#HkUqPOQJp8YtVfDE.97).  <br/> |
|Step 2: Install the Best Practices Analyzer  <br/> |
In the EAC, click Tools on the left navigation (feature) pane. On the Checks tab, click Check your on-premises Exchange Server with the Office 365 Best Practices Analyzer. Click Run when you're prompted to download or run the Office 365 Best Practices Analyzer. Click Accept on the end user license agreements for each of the required prerequisites (the Microsoft Online Services Sign-in Assistant, the .NET Framework, and the Windows Azure Active Directory Module for Windows PowerShell). In the Application Install - Security Warning dialog, click Install. In the Terms of Use for the Office 365 Best Practices Analyzer, click Accept. |
|Step 3: Run the Best Practices Analyzer  <br/> |
After the Office 365 Best Practices Analyzer is installed for the first time, it should start automatically. You can also run it later by selecting Microsoft Office 365 Best Practices Analyzer (Beta) from the Start menu. On the Welcome page, click Next. On the New best practices scan page, click Start scan. If an Office 365 Credentials dialog appears, enter your Office 365 user ID and password. Wait for the scan to complete. |
|Step 4: Learn more about any warnings or failures  <br/> |
On the Best practices scan results summary page, click View details to open the Detailed scan results page, or click Save scan results and open the saved .html file. Click the Learn more link next to any problems that are detected. **Note**: If you saved your results, and you can't see the **Learn more** links in the .html file, click **Allow blocked content** in the popup: **Internet Explorer restricted this webpage from running scripts or ActiveX controls**.  <br/> |
   
## Next steps

After fixing any reported problems, you can run the Office 365 Best Practices Analyzer again from your Exchange server.
  
Please [send us feedback](mailto:o365bpafeedback@microsoft.com) about your Office 365 Best Practices Analyzerexperience so that we can continue to make improvements. 
  

