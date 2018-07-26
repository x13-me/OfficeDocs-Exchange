---
title: "Delegate the installation of Exchange 2019 servers"
ms.author: chrisda
author: chrisda
manager: serdars
ms.date: 7/23/2018
ms.audience: ITPro
ms.topic: get-started-article
ms.prod: exchange-server-it-pro
localization_priority: Normal
ms.collection: Strat_EX_Admin
ms.assetid: 
description: "Summary: Learn how to configure Exchange 2019 server objects in Active Directory so users who aren't Exchange administrators can install Exchange 2019 servers"
---

# Delegate the installation of Exchange 2019 servers

 **Summary**: Learn how to configure Exchange 2019 server objects in Active Directory so users who aren't Exchange administrators can install Exchange 2019 servers.
  
In large companies, people who install and configure new Windows servers often aren't Exchange administrators. In Exchange 2019, these users can still install Exchange on Windows servers _after_ an Exchange administrator *provisions* the Exchange server in Active Directory. Provisioning an Exchange server makes all of the required changes to Active Directory independently of the actual installation of Exchange 2019 on a computer. An Exchange administrator can provision a new server in Active Directory hours or even days before Exchange is installed on the new computer.

After an Exchange administrator provisions the server, the only requirement for the user that's installing Exchange is membership in the [Delegated Setup](https://technet.microsoft.com/library/dd876881(v=exchg.150).aspx) role group. The Delegated Setup role group only allows members to install the Exchange Server software on provisioned servers. If this sounds like something you want to do, then this topic is for you.
    
## What do you need to know before you begin?

- Estimated time to complete this procedure: Less than 10 minutes.

- You can only provision an Exchange 2019 server from the command line (Unattended Setup). You can't use the Setup Wizard.

- You can't provision the first Exchange 2019 server in your organization for the installation of Exchange by a delegate. An Exchange administrator needs to install the first Exchange 2019 server in the organization. After that, you can provision _additional_ Exchange 2019 servers so users who aren't Exchange administrators can install _additional_ Exchange servers using delegated setup.

- A delegated user can't uninstall an Exchange server. To uninstall an Exchange server, you need to be an Exchange administrator.

- Download and use the latest available release of Exchange 2019 from [Updates for Exchange 2019](../../new-features/updates.md).

- You need to be a member of the [Organization Management](https://technet.microsoft.com/library/dd335087(v=exchg.150).aspx) role group to provision an Exchange server.

- Having problems? Ask for help in the Exchange forums. Visit the forums at: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkId=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkId=267542), or [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkId=285351).


## Use the Command Prompt to provision Exchange 2019 servers

You can do the following steps on the Windows server where the delegated user is eventually going to install Exchange, or from another computer that's a member of the domain.

1. In File Explorer, right-click on the Exchange 2019 ISO image file that you downloaded, and then select **Mount**. Note the virtual DVD drive letter that's assigned.
  
2. Opwn a Windows Command Prompt window. For example:

    - Press the Windows key + 'R' to open the **Run** dialog, type cmd.exe, and then press **OK**.

    - Press **Start**. In the **Search** box, type **Command Prompt**, then in the list of results, select **Command Prompt**.

3. In the Command Prompt window, run one of the following commands based on where you did the previous steps:
    
  - **You're running Setup on the computer that's being provisioned**:
    
    ```
    <Virtual DVD drive letter>:\Setup.exe /NewProvisionedServer /IAcceptExchangeServerLicenseTerms
    ```

    For example:

    ```
    E:\Setup.exe /NewProvisionedServer /IAcceptExchangeServerLicenseTerms
    ```

  - **You're running Setup on another computer**:
    
    ```
    <Virtual DVD drive letter>:\Setup.exe /NewProvisionedServer:<ComputerName> /IAcceptExchangeServerLicenseTerms
    ```

    For example:

    ```
    E:\Setup.exe /NewProvisionedServer:Mailbox01.contoso.com /IAcceptExchangeServerLicenseTerms
    ```

4. Add the appropriate users to the Delegated Setup role group so they can install Exchange on the provisioned server. To add users to a role group, see [Add members to a role group](../../permissions/role-group-members.md#add).
    
  
## How do you know this worked?

After you've completed the previous steps, a delegate can install Exchange 2019 on the provisioned server as described in [Install the Exchange 2019 Mailbox role using the Setup wizard](install-mailbox-role.md).

To verfiy that you've successfully provisioned an Exchange 2019 server for a delegate installation of Exchange, do the following steps:
  
1. Open Active Directory Users & Computers.
    
2. Select **Microsoft Exchange Security Groups**, double-click **Exchange Servers**, and then select the **Members** tab.
    
3. On the **Members** tab, verify the server that you provisioned is listed as a member of the security group. A member of the Delegated Setup role group can now install Exchange on the server.
    
## More information

The changes in Active Directory that are made by the typical installation of or the provisioning of an Exchange server are desribed in the following list: 
  
- A server object is created in the **CN=Servers,CN=Exchange Administrative Group (FYDIBOHF23SPDLT),CN=Administrative Groups,CN=\<Organization Name\>,CN=Microsoft Exchange,CN=Services,CN=Configuration,DC=\<Root Domain\>** configuration partition.
    
- The following access control entries (ACEs) are added to the server object within the configuration partition for the Delegated Setup role group:
    
  - Full Control on the server object and its child objects
    
  - Deny access control entry for the Send As extended right
    
  - Deny access control entry for the Receive As extended right
    
  - Deny CreateChild and DeleteChild permissions for Exchange Public Folder Store objects
    
     **Note**: Public folders are administered at an organizational level; therefore, the creation and deletion of public folder stores is restricted to Exchange administrators.
  
- The Active Directory computer account for the server is added to the Exchange Servers group.
    
- The server is added as a provisioned server in the Exchange admin center (EAC).

Only members of the Organization Management role group in Exchange have the permissions required to make these changes to Active Directory.
 