--
title: "What's new in Exchange 2019"
ms.author: dmaguire
author: msdmaguire
manager: serdars
ms.date: 7/27/2018
ms.audience: ITPro
ms.topic: overview
ms.prod: exchange-server-it-pro
localization_priority: Critical
ms.assetid: 97501135-2149-4590-8373-98e638ac8eb1
description: "Summary: Learn about the new features that are available in Exchange 2019 when you upgrade from previous versions of Exchange."
monikerRange: "=exchserver-2019"
---

# What's new in Exchange 2019

Exchange Server 2019 brings a new set of technologies, features, and services to Exchange Server, the messaging platform that provides email, scheduling, and tools for custom collaboration and messaging service applications. Its goal is to support people and organizations as their work habits evolve from a communication focus to a collaboration focus. At the same time, Exchange 2019 helps lower the total cost of ownership whether you deploy Exchange 2019 on-premises or provision your mailboxes in the cloud.

Choose the section below that matches the version of Exchange that you're upgrading from. If you want to know about features that have been removed or replaced in Exchange 2019, see [What's discontinued in Exchange 2019](discontinued-features.md).

For more information about deploying Exchange 2019, see [Planning and deployment for Exchange Server](../plan-and-deploy/plan-and-deploy.md).

## What's new when upgrading from Exchange 2016 to Exchange 2019?

### Security

- **Windows Server Core support**: Running Exchange on a Windows deployment with less surface area means less attack surface area and fewer components to service.

- **Block external access to Exchange admin center (EAC) and the Exchange Management Shell**: You can use Client Access Rules to only allow administration of Exchange from the internal network instead of using complex network and firewall rules.

### Performance 

- **Improved search infrastructure**: The completely rebuilt search infrastructure for cloud scale and reliability in Exchange Online is now avaialble in Exchange 2019. This new search infrastructure allows for indexing of bigger files, simpler management, and better search performance.

- **Faster, more reliable failovers**:The changes to the search architecture result in significantly faster and more reliable failover over between servers.

- **Metacache database**: Improvements at the core of Exchange's database engine enable better overall performance and take advantage of the latest storage hardware, including larger disks and SSDs.

- **Modern hardware support**: Exchange now supports up to 256 GB of memory and 48 CPU cores.

- **Dynamic database cache**: The information store process employs dynamic memory cache allocation optimizing memory usage to active database usage.

### Clients

- **Calendar - Do Not Forward**: This is similar to Iformation Rights Managment (IRM) for caleindar items without the IRM deployment requirements. Attendees can't forward the invitation to other people, and only the organizer can invite additional attendees.

- **Calendar - Better Out of Office**: Additional options when you won't be in the office. Key options include: add an event to your calendar that shows you as Away/Out of Office, and a quick option to cancel/decline meetings that will happen while you're away.

- **Calendar - Remove-CalendarEvents cmdlet**: Enables administrators to cancel meetings that were organized by a user that has left the company. Previously, conference rooms or meeting attendees would have these defunct meetings permanently on their calendars.

- **Assign delegate permission via PowerShell**: Updates to the Add-FolderPermissions cmdlet so administrators can assign delegate permissions.

- **Email address internationalization (EAI)**: Email addresses that contain non-English characters can now be routed and delivered natively.

## What's new when upgrading from Exchange 2013 to Exchange 2019?

### Exchange 2019 architecture

Today, CPU horsepower is significantly less expensive and is no longer a constraining factor. With that constraint lifted, the primary design goal for Exchange 2019 is for simplicity of scale, hardware utilization, and failure isolation. With Exchange 2019, we reduced the number of server roles to two: the Mailbox and Edge Transport server roles.

Unified Messaging (UM) has been removed from Exchange 2019. Other than that, the Mailbox server in Exchange 2019 includes all of the server components from the Exchange 2013 Mailbox and Client Access server roles:

- Client Access services provide authentication, limited redirection, and proxy services. Client Access services don't do any data rendering and offer all the usual client access protocols: HTTP, POP and IMAP, and SMTP.

- Mailbox services include all the traditional server components found in the Exchange 2013 Mailbox server role except Unified Messaging: the backend client access protocols, Transport service, and Mailbox databases. The Mailbox server handles all activity for the active mailboxes on that server.

 The Edge Transport role is typically deployed in your perimeter network, outside your internal Active Directory forest, and is designed to minimize the attack surface of your Exchange deployment. By handling all Internet-facing mail flow, it also adds additional layers of message protection and security against viruses and spam, and can apply mail flow rules (also known as transport rules) to control message flow.

For more information about the Exchange 2019 architecture, see [Exchange architecture](../architecture/architecture.md).

Along with the new Mailbox role, Exchange 2019 now allows you to proxy traffic from Exchange 2013 Client Access servers to Exchange 2019 mailboxes. This new flexibility gives you more control in how you move to Exchange 2019 without having to worry about deploying enough front-end capacity to service new Exchange 2019 servers.

### Clients

#### Outlook on the web (formerly known as Outlook Web App)

Outlook Web App is now known as Outlook on the web, which continues to let users access their Exchange mailbox from almost any web browser.

> [!NOTE]
> Supported Web browsers for Outlook on the web in Exchange 2019 are Microsoft Edge, Internet Explorer 11, and the most recent versions of Mozilla Firefox, Google Chrome, and Apple Safari.

The former Outlook Web App user interface has been updated and optimized for tablets and smart phones, in addition to desktop and laptop computers. New Exchange 2019 features include:

- **Platform-specific experiences for phones** for both iOS and Android.

- **Premium Android experience** using Chrome on devices running Android version 4.2 or later.

- **Email improvements**, including a new single-line view of the Inbox with an optimized reading pane, archiving, emojis, and the ability to undo mailbox actions like deleting a message or moving a message.

- **Contact linking** the ability for users to add contacts from their LinkedIn accounts.

- **Calendar** has an updated look and new features, including email reminders for Calendar events, ability to propose a new time in meeting invitations, improved search, and birthday calendars.

- **Search suggestions and refiners** for an improved search experience that helps users find the information they want, faster. Search suggestions try to anticipate what the user's looking for and returns results that might be what the user is looking for. Search refiners will help a user more easily find the information they're looking for by providing contextually-aware filters. Filters might include date ranges, related senders, and so on.

- **New themes** Thirteen new themes with graphic designs.

- **Options** for individual mailboxes have been overhauled.

- **Link preview** which enables users to paste a link into messages, and Outlook on the web automatically generates a rich preview to give recipients a peek into the contents of the destination. This works with video links as well.

- **Inline video** player saves the user time by keeping them in the context of their conversations. An inline preview of a video automatically appears after inserting a video URL.

- **Pins and Flags** which allow users to keep essential emails at the top of their inbox (Pins) and mark others for follow-up (Flags). Pins are now folder specific, great for anyone who uses folders to organize their email. Quickly find and manage flagged items with inbox filters or the new Task module, accessible from the app launcher.

- **Performance improvements** in a number of areas across Outlook on the web, including creating calendar events, composing, loading messages in the reading pane, popouts, search, startup, and switching folders.

- **New Outlook on the web action pane** that allows you to quickly click those actions you most commonly use such as New, Reply all, and Delete. A few new actions have been added as well including Archive, Sweep, and Undo.

#### MAPI over HTTP

MAPI over HTTP is now the default protocol that Outlook uses to communicate with Exchange. MAPI over HTTP improves the reliability and stability of the Outlook and Exchange connections by moving the transport layer to the industry-standard HTTP model. This allows a higher level of visibility of transport errors and enhanced recoverability. Additional functionality includes support for an explicit pause-and-resume function, which enables supported clients to change networks or resume from hibernation while maintaining the same server context.

 **Note**: MAPI over HTTP isn't enabled in organizations where the following conditions are both true:

- You're installing Exchange 2019 in an organization that already has Exchange 2013 servers installed.

- MAPI over HTTP wasn't enabled in Exchange 2013.

While MAPI over HTTP is now the default communication protocol between Outlook and Exchange, clients that don't support it will fall back to Outlook Anywhere (RPC over HTTP).

For more information, see [MAPI over HTTP in Exchange Server](../clients/mapi-over-http/mapi-over-http.md).

#### Document collaboration

Exchange 2019, along with SharePoint Server 2019, enables Outlook on the web users to link to and share documents that are stored in OneDrive for Business in an on-premises SharePoint server instead of attaching files to messages. Users in an on-premises environment can collaborate on files in the same manner that's used in Office 365.

For more information about SharePoint Server 2019, see [New and improved features in SharePoint Server 2016](https://go.microsoft.com/fwlink/p/?LinkId=627299).

When an Exchange 2019 user receives a Word, Excel, or PowerPoint file in an email attachment, and the file is stored in OneDrive for Business or on-premises SharePoint, the user will now have the option of viewing and editing that file in Outlook on the web alongside the message. To do this, you'll need a separate computer in your on-premises organization that's running Office Online Server. For more information, see [Install Office Online Server in an Exchange organization](../plan-and-deploy/install-office-online-server.md).

Exchange 2019 also brings the following improvements to document collaboration:

- Saving files to OneDrive for Business.

- Uploading a file to OneDrive for Business.

- Most Recently Used lists populated with both local and online files.

### Office 365 hybrid

The Hybrid Configuration Wizard (HCW) that was included with Exchange 2013 is moving to become a cloud-based application. When you choose to configure a hybrid deployment in Exchange 2019, you'll be prompted to download and install the wizard as a small app. The wizard will function the same in previous versions of Exchange, with a few new benefits:

- The wizard can be updated quickly to support changes in the Office 365 service.

- The wizard can be updated to account for issues detected when customers try to configure a hybrid deployment.

- Improved troubleshooting and diagnostics to help you resolve issues that you run into when running the wizard.

- The same wizard will be used by everyone configuring a hybrid deployment who's running Exchange 2013 or later.

In addition to Hybrid Configuration Wizard improvements, multi-forest hybrid deployments are being simplified with Azure Active Directory Connect (AADConnect). AADConnect introduces management agents that will make it significantly easier to synchronize multiple on-premises Active Directory forests with a single Office 365 tenant. For more information about AADConnect, see [Integrating your on-premises identities with Azure Active Directory](https://go.microsoft.com/fwlink/p/?LinkID=527969).

Exchange ActiveSync clients will be seamlessly redirected to Office 365 when a user's mailbox is moved to Exchange Online. To support this, ActiveSync clients need to support HTTP 451 redirect. When a client is redirected, the profile on the device is updated with the URL of the Exchange Online service. This means the client will no longer attempt to contact the on-premises Exchange server when trying to find the mailbox.

### Messaging policy and compliance

There are several new and updated message policy and compliance features in Exchange 2019.

#### Data loss prevention

To comply with business standards and industry regulations, organizations need to protect sensitive information and prevent its inadvertent disclosure. Examples of sensitive information that you might want to prevent from leaking outside your organization include credit card numbers, social security numbers, health records, or other personally identifiable information (PII). With a DLP policy and mail flow rules (also known as transport rules) in Exchange 2019, you can now identify, monitor, and protect 80 different types of sensitive information with new conditions and actions:

- With the new condition **Any attachment has these properties, including any of these words**, a mail flow rule can match messages where the specified property of the attached Office document contains specified words. This condition makes it easy to integrate your Exchange mail flow rules and DLP policies with SharePoint, Windows Server 2012 R2 File Classification Infrastructure (FCI), or a third-party classification system.

- With the new action **Notify the recipient with a message**, a mail flow rule can send a notification to the recipient with the text you specify. For example, you can inform the recipient that the message was rejected by a mail flow rule, or that it was marked as spam and will be delivered to their Junk Email folder.

- The action **Generate incident report and send it to** has been updated to enable the notification of multiple recipients by allowing a group address to be configured as the recipient.

To learn more about DLP, see [Data loss prevention in Exchange Server](../policy-and-compliance/data-loss-prevention/data-loss-prevention.md).

#### In-place Archiving, retention, and eDiscovery

Exchange 2019 includes the following improvements to In-Place Archiving, retention, and eDiscovery to help your organization meet its compliance needs:

- **Public folder support for In-Place eDiscovery and In-Place Hold**: Exchange 2019 integrates public folders into the In-Place eDiscovery and Hold workflow. You can use In-Place eDiscovery to search public folders in your organization, and you can put an In-Place Hold on public folders. And similar to placing a mailbox on hold, you can place a query-based and a time-based hold on public folders. Currently, you can only search and place a hold on all public folders. In later releases, you'll be able to choose specific public folders to search and place on hold. For more information, see [Search and place a hold on public folders using In-Place eDiscovery](../policy-and-compliance/ediscovery/search-public-folders.md).

- **Compliance Search**: Compliance Search is a new eDiscovery search tool in Exchange 2019 with new and improved scaling and performance capabilities. You can use it to search very large numbers of mailboxes in a single search. In fact, there's no limit on the number of mailboxes that can be included in a single search, so you can search all mailboxes in your organization at once. There's also no limit on the number of searches that can run at the same time. For In-Place eDiscovery in Exchange 2019, the limits are the same as in Exchange 2013: you can search up to 10,000 mailboxes in a single search and your organization can run a maximum of two In-Place eDiscovery searches at the same time.

    In Exchange 2019, Compliance Search is only available by using the Exchange Management Shell. For information about using the Compliance Search cmdlets, see the following topics:

  - [Get-ComplianceSearch](http://technet.microsoft.com/library/3bf7edeb-7674-464e-abad-4b1b8858114d.aspx)

  - [New-ComplianceSearch](http://technet.microsoft.com/library/433d1602-a026-4d63-be5e-605dd6b7b0d0.aspx)

  - [Remove-ComplianceSearch](http://technet.microsoft.com/library/6f952437-7ddd-42f8-b10b-5ab4e5562141.aspx)

  - [Set-ComplianceSearch](http://technet.microsoft.com/library/49464588-9e57-442f-97ec-ab9d9927983a.aspx)

  - [Start-ComplianceSearch](http://technet.microsoft.com/library/17ef8cc9-d716-446c-a8b9-b9109a6cab5a.aspx)

  - [Stop-ComplianceSearch](http://technet.microsoft.com/library/675934e6-8a55-4615-8c46-a20bc656afdc.aspx)

    > [!NOTE]
    > To have access to the Compliance Search cmdlets, an administrator or eDiscovery manager must be assigned the Mailbox Search management role or be a member of the Discovery Management role group.

For more information, see [Messaging policy and compliance in Exchange Server](../policy-and-compliance/policy-and-compliance.md).

#### Improved performance and scalability

In Exchange 2019, the search architecture has been redesigned. Previously, search was a synchronous operation that was not very fault-tolerant. The new architecture is asynchronous and decentralized. It distributes the work across multiple servers and keeps retrying if any servers are too busy. This means that we can return results more reliability, and faster.

Another advantage of the new architecture is that search scalability is improved. The number of mailboxes you can search at once using the console has increased from 5k to 10k for both mailboxes and archive mailboxes, allowing you to search a total of 20k mailboxes at the same time.
