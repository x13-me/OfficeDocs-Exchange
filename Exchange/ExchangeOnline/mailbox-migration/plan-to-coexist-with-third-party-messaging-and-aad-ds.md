---
localization_priority: Normal
ms.topic: conceptual
author: msdmaguire
ms.author: dmaguire
ms.assetid: 3bce1321-0bff-40dc-92e1-52c5b955cdf5
ms.date: 
description: "Admins can lear about cross-premises email with an on-premises email system other than Exchange and Exchange Online."
title: Plan to coexist with a third-party messaging system using Active Directory Domain Services
ms.collection: 
- exchange-online
- M365-email-calendar
search.appverid:
- MET150
- MOE150
- MED150
- MBS150
- BCS160
ms.audience: Admin
ms.custom: Adm_O365
ms.service: exchange-online
manager: serdars
---

# Plan to coexist with a third-party messaging system using Active Directory Domain Services

Most of the email migration support for Exchange assumes that you're running a on-premises version of Exchange Server in your organization. This topic is written for organizations that are using Active Directory to manage user resources but aren't running Exchange Server.

In the following scenario, the goal is to support cross-premises email coexistence. A third-party mail system (IBM Lotus Notes, Novell GroupWise, etc.) remains in the on-premises organization and shares an email namespace with Exchange Online in the cloud. A unified address book in the cloud shows all users across both the on-premises email system and Exchange Online. Email coexistence may be a short-term or long-term solution.

Active Directory Federation Services (AD FS 3.0 and AD FS 2.0) can also be optionally deployed to allow single sign-on for users.

**Scenario goals**:

- Users with on-premises mailboxes should be represented in the global address list (GAL) as mail-enabled users.

- Mail routing from Exchange Online to the on-premises email organization uses a shared domain namespace.

- Alternatively, as part of a migration strategy, the mail-enabled users in the cloud may be licensed with Exchange Online mailboxes.

- Cross-premises coexistence may last indefinitely. The Exchange Online address list, proper mail routing, and message format fidelity all meet business-class requirements.

**Requirements**:

- Subscription to Office 365 (must be an enterprise subscription).

- On-premises organization must be running Active Directory with the Microsoft Exchange 2013 database schema updates.

- Exchange Management Shell and the Exchange Server Active Directory schema are required for managing email-related users in this scenario. To meet these requirements, you must install the Exchange 2013 Client Access and Mailbox server roles on a server in your on-premises organization. A license for Hybrid Edition of Exchange Server 2013 is available with your Office 365 subscription for enterprises. Information about acquiring and installing the hybrid server is included later in this topic.

- Every mailbox in third-party system needs to have corresponding user object in local Active Directory.

## Technical Overview

To enable any cross-premises messaging scenario, you must determine how you will route email between the on-premises organization and the cloud. From an implementation perspective, the choice comes down to where inbound mail goes first: to the on-premises messaging system or to the cloud. The one you choose depends on the goals of the cross-premises deployment.

### Shared namespace configuration

Generally speaking, if you plan to move all your messaging to the cloud—employing a cross-premises deployment as part of a longer-term mail migration strategy—configuring your mail exchanger record (MX record) to direct inbound email to the cloud first, is a logical choice. Mail forwarding to the on-premises mailboxes is configured in the cloud. In this configuration, you can also take advantage of Office 365/Forefront Online Protection message *hygiene filtering*, referred to as *Active Messaging Protection*, for all email bound to your organization. It's worth noting that the namespace configuration requires you to purchase a FOPE license for all mailboxes in your on-premises environment.

Otherwise, if your long-term goal is to maintain a cross-premises messaging environment indefinitely, and you are not interested in the front-end Active Messaging Protection service provided by FOPE, configuring your mail exchange record (MX record) to direct inbound email to the on-premises messaging environment may be a better choice.

### Email routing in a cross-premises environment

Regardless of where your inbound mail enters the cross-premises deployment, mail-routing requires that users with mailboxes in your on-premises messaging system are represented by mail-enabled users in the cloud messaging system. The mail-enabled user object in the cloud directory is configured with a target SMTP address of the corresponding recipient mailbox in the on-premises organization.

The process of creating mail-enabled users with the correct target address requires installing the Azure Active Directory Sync tool in your on-premises Active Directory. The Azure Active Directory Sync tool creates mail-enabled users in the cloud for each mail-enabled user in the Active Directory with a target address value that matches the verified domain of Office 365.

For example, if you have verified the domain, such as contoso.com, in your Office 365 deployment, the Azure Active Directory Sync tool creates mail-enabled users for any mail-enabled user objects in your Active Directory that have a target address with contoso.com in the SMTP address.

The use of the Exchange tool set provides the ability to manage all the Exchange recipient properties, including the target address, for the mail-users in the cloud.

### Mail formatting

Because you will be configuring Exchange Online to send email to your on-premises mail system, you'll have to make an additional configuration in the cloud to avoid mail formatting issues.

By default, Exchange Online sends messages back to the on-premises system in rich text or Transport Neutral Encapsulation Format (TNEF), which may result in your users receiving plain text emails with Winmail.dat attachments. As a result, you must configure Exchange Online to send all mail to your on-premises system in non-TNEF format (HTML or text). To do this, you must specify the on-premises primary SMTP domain as a *remote domain* in Exchange Online. You can then disable TNEF formatting for all email that is sent to the remote domain.

### Hybrid Edition of Exchange Server

Your Office 365 subscription includes a license to run the Hybrid Edition of Exchange Server 2013 in your on-premises organization. Installing the hybrid server for this scenario is a requirement.

In addition to updating your Active Directory schema with the Exchange email attribute set, the hybrid server provides a tool set to create mail-enabled users and to manage their mail-forwarding settings.

## Implementation

In many cases, the links refer to configuration particulars for an on-premises Exchange messaging system. You will have to translate the goals of the Exchange Server configurations to specific configurations of your third-party messaging solution. As an example, mail-forwarding is a straightforward goal, but it's an area where configuration differs widely across messaging systems.

The following steps outline the process for implementing third-party messaging coexistence with Office 365:

- [Step 1: Sign up for Office 365](#step-1-sign-up-for-office-365)

- [Step 2: Update on-premises Active Directory with Exchange 2013 schema](#step-2-update-on-premises-active-directory-with-exchange-2013-schema)

- [Step 3: Install the Hybrid Edition of Exchange 2013 Server](#step-3-install-the-hybrid-edition-of-exchange-2013-server)

- [Step 4: Enable mail-enabled users in your on-premises Active Directory](#step-4-enable-mail-enabled-users-in-your-on-premises-active-directory)

- [Step 5: Run the Azure Active Directory Sync tool\> to create mail-enabled users in the cloud](#step-5-run-the-azure-active-directory-sync-tool-to-create-mail-enabled-users-in-the-cloud)

- [Step 6: Configure shared namespace routing](#step-6-configure-shared-namespace-routing)

- [Step 7: Disable TNEF to your on-premises messaging system](#step-7-disable-tnef-to-your-on-premises-messaging-system)

- [Step 8: Set up Active Directory Federation Services 3.0 and single sign-on (optional)](#step-8-set-up-active-directory-federation-services-30-and-single-sign-on-optional)

## Step 1: Sign up for Office 365

You must subscribe to Office 365 to create a service tenant that is used in the deployment with your on-premises email system. Office 365 provides you with an Exchange organization in the cloud.

When you subscribe, be sure to verify the primary SMTP domain in your organization with Office 365. The process of verifying a domain proves that you own the domain. The verified domain is also the domain that the Azure Active Directory Sync tool uses to provision objects in the cloud.

Learn more at [Sign up for Office 365](https://office.microsoft.com/en-us/).

## Step 2: Update on-premises Active Directory with Exchange 2013 schema

[Download Exchange Server 2013](https://www.microsoft.com/en-us/download/details.aspx?id=41994)

Exchange Server 2013 includes the Exchange database schema updates, which updates your Active Directory when you run Setup (assuming you run Setup with an account that has sufficient forest-wide permissions). You can also update the schema without installing Exchange by running **Setup with the /PrepareAD** switch.

For more information, see [Prepare Active Directory and Domains](https://go.microsoft.com/fwlink/p/?linkid=253098).

## Step 3: Install the Hybrid Edition of Exchange 2013 Server

Obtain a Hybrid Edition license for Exchange 2013. This is available with your Office 365 subscription. After you install Exchange Server 2013, you'll have 120 days to enter the product key.

You can obtain a free Exchange Server product key for use in configuring your hybrid deployment by using the Hybrid Edition Product Key tool

After obtaining your product key, see [Enter Product Key](https://technet.microsoft.com/en-us/library/bb124582\(v=exchg.150\).aspx) for product key installation guidance.

The hybrid server must have one of the following operating systems installed:

- Windows Server 2012 R2 Standard or Datacenter

- Windows Server 2012 Standard or Datacenter

- Windows Server 2008 R2 Standard with Service Pack 2

- Windows Server 2008 R2 Enterprise with Service Pack 2

- Windows Server 2008 R2 Datacenter RTM or later

For more information about installing Exchange, see [Deploy a New Installation of Exchange 2013](https://go.microsoft.com/fwlink/p/?linkid=247416).

To support coexistence with a third-party mail system, you must install the Exchange 2013 Client Access and Mailbox server roles on a server in your on-premises organization.

## Step 4: Enable mail-enabled users in your on-premises Active Directory

After you have updated your Active Directory with the Exchange schema, you can now *mail-enable* existing users in your Active Directory. In the context of this scenario, mail-enabled users represent the users (that have mailboxes) in your on-premises messaging system that you want to represent in the cloud address book.

Using Exchange Management Shell, run [Enable-MailUser](https://go.microsoft.com/fwlink/p/?linkid=247419) for each user that you want to be displayed in the cloud address book and who has a mailbox in your on-premises messaging organization.

The **Enable-Mailuser** cmdlet only takes the *ExternalEmailAddress* parameter. This parameter updates the target SMTP address for the mail-enabled user, which enables cross-premises mail flow.

The *ExternalEmailAddress* parameter is an email address that you enter for a given user. The email address must meet the following criteria:

- It must be the valid primary SMTP address of the user recipient in your on-premises organization

- The domain address (follows the @ sign) must match the verified domain in Office 365

- The domain address (follows the @ sign) must match the UPN domain for the user in the on-premises directory

Here's an example of how an **Enable-Mailuser** command might look.

```
Enable-MailUser -Identity John -ExternalEmailAddress john@contoso.com
```

To learn more about how to open and use the Exchange Management Shell, see [Open the Exchange Management Shell](https://docs.microsoft.com/powershell/exchange/exchange-server/open-the-exchange-management-shell?view=exchange-ps).

If you must create new users in your on-premises Active Directory, see the following topics:

- [New-MailUser](https://go.microsoft.com/fwlink/p/?linkid=247420)

- [How to Create a New Mail-Enabled User](https://go.microsoft.com/fwlink/p/?linkid=247421)

## Step 5: Run the Azure Active Directory Sync tool\> to create mail-enabled users in the cloud

If your verified domain matches the SMTP domain that is specified in the **targetAddress** attribute of your on-premises mail-enabled user objects, the Directory Sync tool creates mail-enabled users for these objects in the cloud. The cloud address book is also populated with these users.

> [!IMPORTANT]
> During the deployment of the directory synchronization, you must run the Azure Active Directory Sync tool. When you run this wizard, do not select the **Enable Hybrid Deployment** option.

For more information, see [Active Directory synchronization: Roadmap](https://msdn.microsoft.com/en-us/library/azure/hh967642.aspx).

## Step 6: Configure shared namespace routing

In the context of this cross-premises email scenario, a *shared namespace* refers to an SMTP addressing namespace. When you configure a shared namespace, you define how messages will be routed between your on-premises mail system and the cloud, and how messages will be routed between your on-premises system, the cloud, and the Internet.

The procedure for implementing a shared namespace depends on which on-premises email system you have deployed. Another variable is whether you will be configuring your DNS MX record to point to your on-premises system or to the cloud mail system.

In either implementation case, the cloud-based Exchange Online configurations are similar. After you have configured a shared namespace, you should be able to send email between the two messaging systems.

## Step 7: Disable TNEF to your on-premises messaging system

As previously mentioned, Exchange Online will, by default, send TNEF-encoded messages to the on-premises system. To disable this functionality, see [Manage TNEF Message Formatting with Remote Domains](https://go.microsoft.com/fwlink/p/?linkid=247422).

## Step 8: Set up Active Directory Federation Services 3.0 and single sign-on (optional)

For more information, see [Single sign-on roadmap](https://msdn.microsoft.com/en-us/library/azure/hh967643.aspx).

## Mailbox migration

This section provides links to more information about migrating mailboxes from your on-premises organization to the cloud.

### Moving messaging-related data

As previously noted, the majority of messaging migration tools that are included with Office 365 are designed to work with Exchange Server. However, Office 365 also includes the [IMAP migration tool](https://go.microsoft.com/fwlink/p/?linkid=242041) for generic email data migration.

For organizations that use Outlook as a mail client, the [PST Capture tool](https://go.microsoft.com/fwlink/p/?linkid=246929) may also be used to migrate messaging data to the cloud.

For other messaging migration solutions, you may need to work with a third-party solution provider.

Here are some third-party migration tools and partners that can assist with Exchange migrations from third-party platforms:

- [**Binary Tree**](https://binarytree.com/) Provider of cross-platform messaging migration and coexistence software, with products that provide for the analysis of and the coexistence and migration between on-premises and online enterprise messaging and collaboration environments based on IBM Lotus Notes and Domino and Microsoft Exchange and Microsoft SharePoint.

- [**BitTitan**](https://www.bittitan.com/) Provider of migration solutions to Exchange Online.

- [**Dell**](https://software.dell.com/platforms/office-365/) Provider of on-premises and hosted migration and coexistence software, including pre-migration analysis and complete user and application coexistence. Full-featured migrations from on-premises Microsoft Exchange, IBM Domino, Novell GroupWise, Zimbra and other environments to Microsoft Office 365, Exchange Online, and SharePoint Online.

- [**Metalogix**](https://www.metalogix.com/) Provider of migration solutions to Exchange Online and SharePoint Online.

- [**Transvault**](http://www.transvault.com/) Provider of migration solutions to Exchange Online.

### Converting cloud users to mailbox-enabled users

If you've already deployed a cross-premises mail routing environment as described in this document, the users that you have created in the cloud with directory synchronization are mail-enabled users.

To provision mailboxes for these users, license them for Exchange Online in the Office 365 admin console. For more information, see [Activate synced users](https://msdn.microsoft.com/en-us/library/azure/hh967617.aspx).
