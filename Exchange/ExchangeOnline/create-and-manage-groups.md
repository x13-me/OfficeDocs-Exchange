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

- **Microsoft 365 group** (formerly known as Office 365 groups), is used for collaboration between teams, both inside and outside your company; by giving them a group email and a shared workspace for conversations, files, and calendars.

  >[!NOTE]
  > **Microsoft 365 group** is the recommended group as it provides the teams a shared workspace to communicate, share files, appointments, emails, contacts and other mailbox items.

- **Distribution list group** is used for sending emails/notifications to a group of people.

- **Mail-enabled security group** is used for granting access to resources such as OneDrive, SharePoint, and emailing notifications to those users.

For more information see, [groups](https://docs.microsoft.com/microsoft-365/admin/create-groups/compare-groups?view=o365-worldwide).

See one of the following topics for managing groups in the new Exchange admin center:

- [Create and manage distribution groups](https://docs.microsoft.com/Exchange/recipients-in-exchange-online/manage-distribution-groups/manage-distribution-groups)

- [Manage mail-enabled security groups](https://docs.microsoft.com/Exchange/recipients-in-exchange-online/manage-mail-enabled-security-groups)

## Create a group

1. Login to the [new Exchange admin center](https://admin.exchange.microsoft.com/#/), and navigate to **Recipients** > **Groups**.
  
     The **Active groups** page is displayed.

2. Click **Add a group** and do the following in the details pane:

   - In **Group type** tab, under **Choose a group type**, select one of the group types, and and then click **Next**.
   
      >[!NOTE]
      > You can create a group under the following group types:
      > - **Microsoft 365** (recommended): To allow collaboration between teams by giving them the group email and a shared workspace.
      > - **Distribution**: To allow sending emails to all members of the list.
      > - **Mail-enabled security**: With functionality of a distribution list and access to OneDrive and SharePoint.
      
   - In **Basics** tab, under **Set up the basics**, enter **Name**, and **Description**, and then click **Next**.   
      
   - In **Owners** tab, under **Assign Owners**, you can either enter a name or email address or select the owners from the list, and then click **Next**.
   
      >[!NOTE]
      > This option is applicable only if **Microsoft 365** (recommended) is selected as a group type. It is recommended to have at least two owners in a group.
        
   - In **Settings** tab, under **Edit Settings**, provide the details. The details are displayed based on the group type you selected. 
           
      >[!NOTE]
      > **Microsoft Teams** can be added to only a **Microsoft 365 group**. This option is not available for the other groups. To create a team, all group owners must have a license that includes **Teams**.
        
      >[!NOTE]
      > Some settings like **Allow External Senders** or **Send Copies of Group Conversations to Members’ Inboxes** can only be set after the group is created.  
       
      For more information see, [Create a group](https://docs.microsoft.com/microsoft-365/admin/create-groups/create-groups?view=o365-worldwide)
       
   - In **Finish** tab, under **Review and finish adding group**, verify all the details, and then click **Create group**.
            
      For more information see, [Use groups to collaborate effectively](https://support.microsoft.com/office/learn-about-microsoft-365-groups-b565caa1-5c40-40ef-9915-60fdb2d97fa2?WT.mc_id=365AdminCSH&ui=en-US&rs=en-US&ad=US)
      
3. Click **Close**.

## Edit a group

1. From the list view, select the group that you want to edit, and click the selected group name.
  
2. In the details pane, do the following:

   - In **General** section, you can edit the **Basic information** and the **Email address** of the group.
   
   - In **Members** section, you can view, manage, and add **Owners** and **Members** to the group.
   
   - In **Settings** section, you can do the following:
   
     a. For **Microsoft 365 group**, you can edit/check the confirmation boxes under **General settings**, change the status in **Privacy** settings, and then click                   **Save** to save the changes.
      
     b. For **Distribution list group** and **Mail-enabled security group**, you can edit/check the confirmation box to allow external senders to email this group and    
          then click **Advanced Settings** to edit/manage more settings in the **Exchange admin center**.
   
   - In **Microsoft Teams** section, you can manage your **Teams** settings in **Microsoft Teams admin center**.
    
   >[!NOTE]
   > **Microsoft Teams** can be added to only a **Microsoft 365 group**. This option is not available for the other groups. To create a team, all group owners must have a license that includes **Teams**.

## Export a group

You can export group details in a .csv file format and then view them in **Excel**.

1. Select the group from the list view that you want to export and click **Export groups**.

   The dialog box to confirm the export is displayed.
   
2. Click **Continue**.

   The csv format of the group details file is downloaded.

## Naming policy

You can add prefixes and suffixes to your group names.

1. Click **Add naming policy**.

2. In **Edit group naming policy** details pane, do the following:

   - In **Policy** section, provide the details. 
   
   - In **Blocked words**, add specific words that you want to block from being used in group names and aliases.
   
3. Click **Save**.

## Upgrade distribution group

You can upgrade a **Distribution list group** to **Microsoft 365 group**.

1. Select the group from the list view that you want to upgrade and click **Upgrade distribution group**.

   The dialog box to confirm the export is displayed.
   
2. Click **Continue**.

   >[!NOTE]
   > The upgrade is a permanent change and can not be reversed.
 
## Other actions

1. Click **Refresh** to update the list of groups page after adding a group or editing the details of a group.

2. Click **...** to perform the following actions:

   - Click **Edit name and description** to edit the group information.
    
   - Click **Edit email address** to edit **Primary** and **Aliases** email address.
    
   - Click **Delete group** to delete the selected group.
  
3. Click **Filter** to filter the groups based on the displayed options in the drop-down list.
  
4. Enter information in the **Search** box to search a group, group email id, or other details.


