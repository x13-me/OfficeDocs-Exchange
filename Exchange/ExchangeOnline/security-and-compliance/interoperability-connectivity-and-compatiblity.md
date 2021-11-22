---
title: "Interoperability, connectivity, and compatibility"
ms.author: office365servicedesc
author: pamelaar
manager: gailw
audience: ITPro
ms.topic: reference
f1_keywords:
- 'exchange-online-interoperability-connectivity-compatibility'
ms.service: o365-administration
ms.localizationpriority: medium
ms.custom: Adm_ServiceDesc
ms.assetid: cdfe686d-a059-4f4d-bb8d-9c2c0ebfa423
description: Learn about the interoperability, connectivity, and compatibility between Microsoft products.
---

# Interoperability, connectivity, and compatibility

## Interoperability with other Microsoft products

### Skype for Business Online

For customers who have deployed Microsoft Lync Server 2010, Lync Server 2013 or Microsoft Office Communications Server 2007 R2 on-premises, Microsoft Office Communicator can connect to Microsoft Exchange Online by using Exchange Web Services to access out-of-office messages and calendar data.
  
On-premises Lync Server 2010 and Lync Server 2013 can interoperate with Exchange Online in two additional ways:
  
- IM and presence interoperability in Outlook on the web
    
- Voice mail interoperability
    
For more information about how to configure Skype for Business Server 2015 with Exchange Online, see [Configuring On-premises Skype for Business Server 2015 Integration with Exchange Online](/skypeforbusiness/deploy/integrate-with-exchange-server/outlook-web-app). For hybrid configurations, see [Supported Skype for Business Server 2015 hybrid configurations](/skypeforbusiness/skype-for-business-hybrid-solutions/integration-with-exchange-and-sharepoint).
  
### Microsoft SharePoint

For customers who have deployed Microsoft SharePoint Server or SharePoint Online as part of an subscription plan, SharePoint can connect to Exchange Online for integrated services.
  
For more information about connecting SharePoint to Exchange Online, see [Use SharePoint Online on a custom domain together with other services](https://go.microsoft.com/fwlink/?LinkId=271805).
  
## Features for external connectivity

Exchange Online offers the following features for connecting with external applications and devices:
  
- **Through messaging protocols such as MAPI over HTTP, SMTP, POP3, IMAP4, or Exchange Web Services** External applications that are running on-premises, in Azure, or in other hosted services can access data stored with Exchange Online by using messaging protocols such as MAPI over HTTP, SMTP, POP3, and IMAPv4. Exchange Web Services or the Exchange Web Services Managed API is recommended for application development. 
    
- **As an SMTP relay** Exchange Online can be set up as an SMTP delivery service to relay email messages sent from fax gateways, network appliances, and custom applications. 
    
### Exchange Web Services

Exchange Web Services (EWS) is the preferred development API for Exchange Server and Exchange Online. Using EWS or the EWS Managed API, administrators can access data stored with Exchange Online from applications that are running on-premises, in Azure, or in other hosted services. EWS lets administrators perform specialized actions, such as querying the contents of a mailbox, posting a calendar event, creating a task, or triggering a specific action based on the content of an email message. Exchange Online enables EWS functionality by granting application permissions to customer accounts. These permissions allow the customer application to access the application mailbox and add content. Exchange Impersonation is one method used to grant application permissions. For details about how to use Exchange Web Services with Exchange Online, refer to the technical articles at the Exchange Online Developer Center.
  
### SMTP relay

Exchange Online can be used as an SMTP delivery service to relay email messages sent from fax gateways, network appliances, and custom applications. For example, if a line-of-business application sends email alerts to users, it can be configured to use Exchange Online as the mail delivery system. The application or service must authenticate with the username and password of a valid, licensed Exchange Online mailbox, and connect by using Transport Layer Security (TLS).
  
## Feature availability

To view feature availability across plans, standalone options, and on-premises solutions, see [Exchange Online service description](exchange-online-service-description/exchange-online-service-description.md).
