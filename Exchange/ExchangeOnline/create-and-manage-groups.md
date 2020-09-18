---
title: "Create and manage groups in the new Exchange admin center"
ms.author: v-bshilpa
author: Benny
manager: Serdars
audience: ITPro
f1.keywords:
ms.topic: article
ms.service: exchange-online
localization_priority: Normal
search.appverid:
ms.collection:  
ms.custom:
description: Create and manage groups in the new Exchange admin center.
---

# Create and manage groups in the new Exchange admin center

Use the new Exchange admin center (EAC) to create, modify, export or remove groups in your Exchange Online organization.

There are three types of groups that can be used to distribute messages:

- Microsoft 365 groups (formerly known as Office 365 groups) is used for collaboration between teams, both inside and outside your company. By giving them a group email and a shared workspace for conversations, files, and calendars.

  >[!NOTE]
  > Microsoft 365 groups is the recommended group as it provides the teams a shared workspace to communicate, share files, appointments, emails, contacts and other mailbox items.

- Distribution list groups is used for sending emails/notifications to a group of people.

- Mail-enabled security groups is used for granting access to resources such as OneDrive, SharePoint, and emailing notifications to those users.

For more information see, [groups](https://docs.microsoft.com/en-us/microsoft-365/admin/create-groups/compare-groups?view=o365-worldwide).

See one of the following topics for managing groups in the new Exchange admin center:

- [Create and manage distribution groups](https://docs.microsoft.com/en-us/Exchange/recipients-in-exchange-online/manage-distribution-groups/manage-distribution-groups)

- [Manage mail-enabled security groups](https://docs.microsoft.com/en-us/Exchange/recipients-in-exchange-online/manage-mail-enabled-security-groups)

## Create a Microsoft 365 groups

1. Navigate to the [new Exchange admin center](https://admin.exchange.microsoft.com/#/).

2. In new Exchange admin center, expand **Recipients**, and then click **Groups**. 

   The **Active groups** page is displayed.

3. Click **Add a group**.

4. In **Add a group** details pane, under the following tabs:

   a. In **Group type** tab, do the following:
   
      -	Under **Choose a group type**, select **Microsoft 365 (recommended)**.
      
      -	Click **Next**.

   b.	In **Basics** tab, do the following:
   
      -	Enter a **Name** (mandatory).
      
      -	Enter **Description** (optional).
      
      -	Click **Next**.

   c.	In **Owners** tab, do the following:
   
      -	Under **Owners**, you can either enter a name/email address or select the owners from the list. 
        
        >[!NOTE]
        > It is recommended to have at least two owners in a group.
        
      -	Click **Next**.
        
   d. In **Settings** tab, do the following:
   
      -	Enter the **Group email address** (mandatory).
      
      -	Set the **Privacy** status of the group as **Public** or **Private**.
      
      -	Under **Add Microsoft Teams to your group**, check the confirmation box to ensure a team is created for this group.
        
        >[!NOTE]
        > Microsoft Teams can be added to only a Microsoft 365 group. This option is not available for the other groups. To create a team, all group owners must have a license that includes Teams.
        
        >[!NOTE]
        > Some settings like **Allow External Senders**, or **Send Copies of Group Conversations to Members’ Inboxes** can only be set after the group is created.  
        > For more information see, [Create a group]( https://docs.microsoft.com/en-US/microsoft-365/admin/create-groups/create-groups?view=o365-worldwide)
        
      - Click **Next**.
        
   e.	In **Finish** tab, do the following:
   
      - Review/edit the contents to ensure the provided information is correct. 
      
      - Click **Create group**.
      
      For more information see, [Use groups to collaborate effectively]( https://support.microsoft.com/en-us/office/learn-about-microsoft-365-groups-b565caa1-5c40-40ef-9915-60fdb2d97fa2?WT.mc_id=365AdminCSH&ui=en-US&rs=en-US&ad=US)

5. Click **Close**.

## Create a Distribution list group

1. Navigate to the [new Exchange admin center](https://admin.exchange.microsoft.com/#/).

2. In new Exchange admin center, expand **Recipients**, and then click **Groups**. 

    The **Active groups** page is displayed.

3. Click **Add a group**.

4. In **Add a group** details pane, under the following tabs:

   a.	In **Group type** tab, do the following:
   
      -	Under **Choose a group type**, select **Distribution**.
      
      -	Click **Next**.

   b.	In **Basics** tab, do the following:
   
      -	Enter a **Name** (mandatory).
      
      -	Enter **Description** (optional).
      
      -	Click **Next**.

   c.	In **Settings** tab, do the following:
   
      -	Enter the **Group email address** (mandatory).
      
      -	Under **Communication**, check the confirmation box to allow people from outside the organization send email to this distribution group.

   d.	In **Finish** tab, do the following:
   
      - Review/edit the contents to ensure the provided information is correct. 
      
      - Click **Create group**.

5. Click **Close**.

## Create a Mail-enabled security group

1. Navigate to the [new Exchange admin center](https://admin.exchange.microsoft.com/#/).

2. In new Exchange admin center, expand **Recipients**, and then click **Groups**. 

   The **Active groups** page is displayed.

3. Click **Add a group**.

4. In **Add a group** details pane, under the following tabs:

   a. In **Group type** tab, do the following:
   
      -	Under **Choose a group type**, select **Mail-enabled security group**.
      
      -	Click **Next**.

   b.	In **Basics** tab, do the following:
   
      -	Enter a **Name** (mandatory).
      
      -	Enter **Description** (optional).
      
      -	Click **Next**.

   c.	In **Settings** tab, do the following:
   
      -	Enter the **Group email address** (mandatory).
      
      -	Under **Communication**, check the confirmation box to allow people from outside the organization send email to this distribution group.

   d. In **Finish** tab, do the following:
   
      - Review/edit the contents to ensure the provided information is correct. 
      
      - Click **Create group**.

5. Click **Close**.

## Settings
 
1.	Click **Filter** in the toolbar and choose from the drop-down list to apply **Standard filters**.

2.	Click  ![view-op](media/view-option.PNG) > **Normal list**/**Compact list** to switch the list view.

3. Click the group you want to edit from the list view, use the following options in the details pane:

   - In **General** tab, you can edit the **Basic information** and the **Email address** of the group.
   
   - In **Members** tab, you can view, manage, and add **Owners** and **Members** to the group.
   
   - In **Settings** tab, you can do the following:
   
      a. For **Microsoft 365** groups, you can edit/check the confirmation boxes under **General settings**, change the status in **Privacy** settings, and then click **Save**          to save the changes.
      
      b. For **Distribution list** group and **Mail-enabled security** group, you can edit/check the confirmation box to allow external senders to email this group and then              click **Advanced Settings** to edit/manage more settings in the **Exchange admin center**.
   
   - In **Microsoft Teams** tab, you can manage your **Teams** settings in **Microsoft Teams admin center**.
   
     >[!NOTE]
     > Microsoft Teams can be added to only a Microsoft 365 group. This option is not available for the other groups. To create a team, all group owners must have a license that includes Teams.

4.	Select the group from the list view, use the following options in the toolbar:

    -	Click **Export groups** to export group details in csv file format and view them in **Excel**.
    
    -	Click **…** > **Edit name and description** to edit the information.
    
    -	Click **…** > **Edit email address** to edit **Primary**/ **Aliases** email address.
    
    -	Click **…** > **Delete group** to delete the group.


