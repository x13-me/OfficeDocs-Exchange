---
title: "Enable or disable modern authentication in Exchange Online"
ms.author: chrisda
author: chrisda
ms.date: 8/1/2017
ms.audience: Admin
ms.topic: article
ms.service: o365-administration
localization_priority: Normal
ms.collection: Adm_O365
ms.custom:
- Adm_O365
- Adm_O365_FullSet
- MiniMaven
search.appverid:
- BCS160
- MOE150
- MED150
ms.assetid: 58018196-f918-49cd-8238-56f57f38d662
description: "Modern authentication in Office 365 enables authentication features like multi-factor authentication (MFA) using smart cards, certificate-based authentication (CBA), and third-party SAML identity providers. Modern authentication is based on the Active Directory Authentication Library (ADAL) and OAuth 2.0."
---

# Enable or disable modern authentication in Exchange Online

Modern authentication in Office 365 enables authentication features like multi-factor authentication (MFA) using smart cards, certificate-based authentication (CBA), and third-party SAML identity providers. Modern authentication is based on the [Active Directory Authentication Library](https://go.microsoft.com/fwlink/p/?LinkId=717281) (ADAL) and OAuth 2.0. 
  
When you enable modern authentication in Exchange Online, Outlook 2016 and Outlook 2013 (version 15.0.4753 or later, with a required registry setting) use modern authentication to log in to Office 365 mailboxes. For more information, see [How modern authentication works for Office 2013 and Office 2016 client apps](https://support.office.com/article/e4c45989-4b1a-462e-a81b-2a13191cf517).
  
When you disable modern authentication in Exchange Online, Outlook 2016 and Outlook 2013 use basic authentication to log in to Office 365 mailboxes. They don't use modern authentication.
  
 **Notes**
  
- Modern authentication is enabled by default in Exchange Online, Skype for Business Online and SharePoint Online.
    
- Other Outlook clients that are available in Office 365 (for example, Outlook Mobile and Outlook for Mac 2016) always use modern authentication to log in to Office 365 mailboxes.
    
- You should synchronize the state of modern authentication in Exchange Online with Skype for Business Online to prevent multiple log in prompts in Skype for Business clients. For instructions, see [https://aka.ms/SkypeModernAuth](https://aka.ms/SkypeModernAuth).
    
## Enable or disable modern authentication in Exchange Online

1. Connect to Exchange Online PowerShell as shown [here](https://go.microsoft.com/fwlink/p/?LinkID=534121).
    
2. Do one of these steps:
    
  - Run this command to enable modern authentication in Exchange Online:
    
  ```
  Set-OrganizationConfig -OAuth2ClientProfileEnabled $true
  ```

  - Run this command to disable modern authentication in Exchange Online:
    
  ```
  Set-OrganizationConfig -OAuth2ClientProfileEnabled $false
  ```

3. To verify that the change was successful, run this command:
    
  ```
  Get-OrganizationConfig | Format-Table -Auto Name,OAuth*
  ```

## See also

[Using Office 365 modern authentication with Office clients](https://support.office.com/article/776c0036-66fd-41cb-8928-5495c0f9168a)

