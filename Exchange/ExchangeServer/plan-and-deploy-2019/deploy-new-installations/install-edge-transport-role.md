---
title: "Install Exchange 2019 Edge Transport servers using the Setup wizard"
ms.author: chrisda
author: chrisda
manager: serdars
ms.date: 4/19/2018
ms.audience: ITPro
ms.topic: get-started-article
ms.prod: exchange-server-it-pro
localization_priority: Priority
ms.collection: Strat_EX_Admin
ms.assetid: 
description: "Summary: Learn how to use the Setup wizard in Exchange 2019 to install the Edge Transport server role on a computer."
---

# Install Exchange 2019 Edge Transport servers using the Setup wizard

 **Summary**: Learn how to use the Setup wizard in Exchange 2019 to install the Edge Transport server role on a computer.
  
Before you install an Exchange Server 2019 Edge Transport server, verify the following prerequisites:
  
- We recommend that you install Edge Transport servers in a perimeter network that's outside of your organization's internal Active Directory forest. Installing the Edge Transport server role on domain-joined computers only enables domain management of Windows features and settings. Edge Transport servers don't directly access Active Directory. Instead, they use Active Directory Lightweight Directory Services (AD LDS) to store configuration and recipient information. For more information about the Edge Transport role, see [Edge Transport servers](../../architecture/edge-transport-servers/edge-transport-servers.md).

- Verify the network, computer hardware, operating system, and software requirements at [Exchange 2019 system requirements](../../plan-and-deploy-2019/system-requirements.md) and [Exchange 2019 prerequisites](../../plan-and-deploy-2019/prerequisites.md).

- Verify the local account on the targer computer is a member of the local Administrators group.

- Verify that you've read the release notes at [Release notes for Exchange 2019](../../release-notes-2019.md).
    
For more information about planning and deploying Exchange 2019, see [Planning and deployment for Exchange 2019](../../plan-and-deploy-2019/plan-and-deploy-2019.md).
  
To install the Mailbox role on a computer, see [Install Exchange 2019 Mailbox servers using the Setup wizard](install-mailbox-role.md). The Edge Transport role can't be installed on the same computer as the Mailbox server role.
 
## What do you need to know before you begin?

- Estimated time to complete: 40 minutes
    
- You need to configure the primary DNS suffix on the computer. For example, if the fully qualified domain name of your computer is edge.contoso.com, the DNS suffix for the computer is contoso.com. For more information, see [Primary DNS Suffix is missing [ms.exch.setupreadiness.FqdnMissing]](../../plan-and-deploy-2019/deployment-ref/ms-exch-setupreadiness-fqdnmissing.md).
    
- For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](../../about-documentation/exchange-admin-center-keyboard-shortcuts.md).
    
> [!CAUTION]
> After you install Exchange on a server, you must not change the server name. Renaming a server after you've installed an Exchange server role is not supported.
  
## Install Exchange Server 2019

1. Use the information in [Updates for Exchange 2019](../../new-features-2019/updates.md) to download the latest version of Exchange 2019 on the computer where you want to install Exchange.
    
2. In File Explorer, right-click on the Exchange ISO image file that you downloaded, and then select **Mount**. In the resulting virtual DVD drive that appears, start Exchange 2019 Setup by double-clicking `Setup.exe`.
    
3. The Exchange Server 2019 Setup wizard opens. On the **Check for Updates?** page, choose one of the following options, and then click **Next** to continue: 
    
  - **Connect to the Internet and check for updates**: We recommend this option, which searches for updates to the version of Exchange 2019 that you're installing (it doesn't detect newer Exchange 2019 Cumulative Updates). This option takes you to the **Downloading Updates** page that searches for updates. Click **Next** to continue.
    
  - **Don't check for updates right now**
    
    ![Exchange 2016 Setup, Check for Updates page](../../media/f0ca225e-b88f-45e9-a8cb-21adaabe984e.png)

4. The **Copying Files** page shows the progress of copying files to the local hard drive. Typically, the files are copied to `%WinDir%\Temp\ExchangeSetup`, but you can confirm the location in the Exchange Setup log at `C:\ExchangeSetupLogs\ExchangeSetup.log`.

    ![Exchange 2016 Setup, Copying Files page](../../media/78813be2-745d-4a58-8da8-883c43aa2650.png)
  
5. On the **Introduction** page, we recommend that you visit the Exchange Server 2019 deployment planning links if you haven't already reviewed them. Click **Next** to continue.

    ![Exchange 2016 Setup, Introduction page](../../media/9f605305-979a-4667-a042-38854677cf0b.png)
  
6. On the **License Agreement** page, review the software license terms, select **I accept the terms in the license agreement**, and then click **Next** to continue.

    ![Exchange 2016 Setup, License Agreement page](../../media/2bb6bfaa-1b39-4052-9420-a7a053b07d58.png)
  
7. On the **Recommended Settings** page, choose one of the following settings: 
    
   - **Use recommended settings**: Exchange automatically sends error reports and information about your computer hardware and how you use Exchange to Microsoft. For information about what's sent to Microsoft and how it's used, click **?** or the help links on the page.
    
    - **Don't use recommended settings**: These settings are disabled, but you can enable them at any time after Setup completes.
    
    Click **Next** to continue.

    ![Exchange 2016 Setup, Recommended Settings page](../../media/26af58f0-52ab-4482-8710-9a7cd2e7a6c3.png)

8. On the **Server Role Selection** page, configure the following options: 
    
    - **Edge Transport role**: Select this option, which also automatically installs the **Management Tools**.
    
    - **Automatically install Windows Server roles and features that are required to install Exchange**: Select this option to have the Setup wizard install the required Windows prerequisites. You might need to reboot the computer to complete the installation of some Windows features. If you don't select this option, you need to install the Windows features manually.
    
      **Note**: Selecting this option installs only the Windows features that are required by Exchange. You need to install other prerequisites manually. For more information, see [Exchange 2019 prerequisites](../../plan-and-deploy-2019/prerequisites.md).
    
    Click **Next** to continue.

9. On the **Installation Space and Location** page, either accept the default installation location (`C:\Program Files\Microsoft\Exchange Server\V15`), or click **Browse** to choose a new location. Make sure that you have enough disk space available in the location where you want to install Exchange. Click **Next** to continue.

    ![Exchange 2016 Setup, Installation Space and Location page](../../media/7ae7f248-3cdc-4453-9d7d-e99edc300d16.png)    
    
12. On the **Readiness Checks** page, verify that the organization and server role prerequisite checks completed successfully. If they haven't, the only option on the page is **Retry**, so you need to resolve the errors before you can continue.

    ![Exchange 2016 Setup, Readiness Check page with errors detected](../../media/d4ee435a-a383-4be6-8233-da4cc2a19eea.png)
  
    After you resolve the errors, click **Retry** to run the prerequisite checks again. You can fix some errors without exiting Setup, while the fix for other errors requires you to restart the computer. If you restart the computer, you need to start over at Step 1.
    
    When no more errors are detected on the **Readiness Checks** page, the **Retry** button changes to **Install** so you can continue. Be sure to review any warnings, and then click **Install** to install Exchange 2016.

    ![Exchange 2016 Setup, Readiness Check page with errors resolved](../../media/a9aca4d0-19ac-4783-8071-cdd435b1658d.png)
  
13. On the **Setup Progress** page, a progress bar indicates how the installation is proceeding.

    ![Exchange 2016 Setup, Setup Progress page](../../media/8fddda28-6e29-44c1-b1bc-149fa7798460.png)
  
14. On the **Setup Completed** page, click **Finish**, and then restart the computer.

    ![Exchange 2016 Setup, Setup Completed page](../../media/b2646172-8088-4d8a-a7f0-888f786c29cf.png)

## Next steps

- To verify that you've successfully installed Exchange 2019, see [Verify an Exchange 2019 installation](../../plan-and-deploy-2019/post-installation-tasks/verify-installation.md).
 
- Complete your deployment by performing the tasks provided in [Exchange 2019 post-installation tasks](../../plan-and-deploy-2019/post-installation-tasks/post-installation-tasks.md).

- Having problems? Ask for help in the Exchange forums. Visit the forums at: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkId=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkId=267542), or [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkId=285351).
