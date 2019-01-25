---
title: "Block legacy authentication in Exchange 2019 hybrid"
ms.author: chrisda
author: chrisda
manager: serdars
ms.date: 
ms.audience: Developer
ms.topic: article
ms.prod: exchange-server-it-pro
localization_priority: Normal
ms.collection:
- Strat_EX_EXOBlocker
- Ent_O365_Hybrid
- Hybrid
ms.assetid: 
description: "Administrators can learn how to block legacy authentication methods for clients connecting to Exchange Server 2019."
---

# Block legacy authentication in Exchange 2019 hybrid

In Exchange Server 2019, we provide a way to block legacy authentication for user accounts so that enterprises can use modern authentication in their Organization.

Following the release of [Hybrid Modern Auth](https://blogs.technet.microsoft.com/exchange/2017/12/06/announcing-hybrid-modern-authentication-for-exchange-on-premises/) there are many customers that want to deploy it, but they require the logical next step of disabling legacy authentication. These customers want to enforce Modern Authentication for supported email clients and completely disable legacy authentication methods for Exchange Server access.

The following legacy authentication methods can be used to access Exchange 2019 servers:

1. Basic Authentication

2. Digest

3. Windows Authentication (NTLM and Kerberos)

This topic describes how to disable these legacy authentication methods for users in Exchange 2019.

## How Legacy authentication is blocked in Exchange Server 2019

You block legacy authentication in Exchange Server 2019 Hybrid setup by creating and assigning authentication policies to individual users. The policies define the client protocols where legacy authentication is blocked and assigning the policy to one or more users blocks their legacy authentication requests for the specified protocols.

THe following example show how to block the Basic, Digest, NTLM and Kerberos authentication methods for the Exchange ActiveSync (EAS) protocol:

1. Create an authentication policy to block legacy authentication for ActiveSync:

   ```
   New-AuthenticationPolicy -Name "Block Legacy Auth" -BlockLegacyAuthActiveSync
   ```

2. Assign the authentication policy to the user (laura@contoso.com in this example).

   ```
   Set-User -Identity laura@contoso.com -AuthenticationPolicy "Block Legacy Auth"
   ```

## Authentication policy procedures in Exchange Server 2019

You manage all aspects of authentication policies in the Exchange Management PowerShell. The protocols and services in Exchange 2019 that you can block legacy authentication for are described in the following table.

|**Protocol or service**|**Description**|**Parameter name**|
|:-----|:-----|:-----|
|Exchange Active Sync (EAS)|Used by some email clients on mobile devices.|*BlockLegacyAuthActiveSync*|
|Autodiscover|Used by Outlook and EAS clients to find and connect to mailboxes in Exchange Online|*BlockLegacyAuthAutodiscover*|
|IMAP|Used by IMAP email clients.|*BlockLegacyAuthImap*|
|MAPI over HTTP (MAPI/HTTP)|Used by Outlook 2013 and later.|*BlockLegacyAuthMapi*|
|Offline Address Book (OAB)|A copy of address list collections that are downloaded and used by Outlook.|*BlockLegacyAuthOfflineAddressBook*|
|POP3|Used by POP email clients.|*BlockLegacyAuthPop*|
|Outlook Anywhere (RPC over HTTP)|Used by Outlook 2016 and earlier.|*BlockLegacyAuthRpc*|
|Exchange Web Services (EWS)|A programming interface that's used by Outlook, Outlook for Mac, and third-party apps.|*BlockLegacyAuthWebServices*|

## What do you need to know before you begin?

- Estimated time to complete each procedure: 3 minutes.

- To open the Exchange Management Shell, see [Open the Exchange Management Shell](http://technet.microsoft.com/library/63976059-25f8-4b4f-b597-633e78b803c0.aspx).

- You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Outlook on the web mailbox policies" entry in the [Clients and mobile devices permissions](../../permissions/feature-permissions/client-and-mobile-device-permissions.md) topic.

- Verify that modern authentication is enabled in your Exchange environment.

- Verify your email clients and apps support modern authentication.

- Verify that your Outlook desktop clients are running the minimum required updates.

> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkId=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkId=267542), or [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkId=285351).

## Create and apply authentication policies

The steps to create and apply authentication policies to block legacy authentication in Exchange Server 2019 are:

1. Create the authentication policy.

2. Assign the authentication policy to users.

These steps are described in the following sections.

### Step 1: Create the authentication policy

To create a policy that blocks legacy authentication for all available client protocols in Exchange 2019 (the recommended configuration), use the following syntax:

```
New-AuthenticationPolicy -Name "<Descriptive Name>" -BlockLegacyAuth<Protocol>
```

This example creates an authentication policy named Block legacy Auth to block legacy auth for the Exchange Active Sync protocol.

```
New-AuthenticationPolicy -Name "Block Legacy Auth" -BlockLegacyAuthActiveSync
```

### Step 2: Assign the authentication policy to users

There are two basic methods you can use to assign authentication policies to users:

- **Individual user accounts**: Use the following syntax:

  ```
  Set-User -Identity <UserIdentity> -AuthenticationPolicy <PolicyIdentity>
  ```

  This example assigns the policy named Block Legacy Auth to the user account laura@contoso.com.

  ```
  Set-User -Identity laura@contoso.com -AuthenticationPolicy "Block Legacy Auth"
  ```

- **Configure the default authentication policy**

  The default authentication policy is assigned to all users who don't already have a specific policy assigned to them. Note that the authentication policies assigned to users take precedence to the default policy. To configure the default authentication policy for the organization, use this syntax:

  ```
  Set-OrganizationConfig -DefaultAuthenticationPolicy \<PolicyIdentity\>
  ```

  This example configures the authentication policy named "Block Legacy Auth" as the default policy.

  ```
  Set-OrganizationConfig -DefaultAuthenticationPolicy "Block Legacy Auth"
  ```

## Supported cmdlets and parameters

The following tables describe the cmdlets and parameters that are available to block legacy authentication.

|**Cmdlet**|**Parameter**|
|:-----|:-----|
|New-AuthenticationPolicy|Name|
||BlockLegacyAuthActiveSync|
||BlockLegacyAuthAutodiscover|
||BlockLegacyAuthMapi|
||BlockLegacyAuthOfflineAddressBook|
||BlockLegacyAuthWebServices|
||BlockLegacyAuthRpc|
||BlockLegacyAuthImap|
||BlockLegacyAuthPop|
||Confirm|
||WhatIf|
|Remove-AuthenticationPolicy|Identity|
||Confirm|
||WhatIf|
|Set-AuthenticationPolicy|Identity|
||BlockLegacyAuthActiveSync|
||BlockLegacyAuthAutodiscover|
||BlockLegacyAuthMapi|
||BlockLegacyAuthOfflineAddressBook|
||BlockLegacyAuthWebServices|
||BlockLegacyAuthRpc|
||BlockLegacyAuthImap|
||BlockLegacyAuthPop|
||Confirm|
||WhatIf|
|Get-AuthenticationPolicy|Identity|

|**Cmdlet**|**Parameter**|
|:-----|:-----|
|Set-User|AuthenticationPolicy|
|Set-OrganizationConfig|DefaultAuthenticationPolicy|
