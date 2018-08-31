---
title: "Deploying Outlook for iOS and Android app configuration settings"
ms.author: dmaguire
author: msdmaguire
ms.reviewer: smithre4
manager: serdars
ms.date: 8/31/2018
ms.audience: ITPro
ms.topic: article
ms.service: exchange-online
localization_priority: Normal
ms.assetid: e8a034f6-39b8-4dea-a3bc-9421aaa75d1d
description: "Summary: How to customize the behavior of Outlook for iOS and Android in your Exchange organization."
---

# Deploying Outlook for iOS and Android app configuration settings

 **Summary**: How to customize the behavior of Outlook for iOS and Android in your Exchange organization.
  
Outlook for iOS and Android supports app settings that allow Office 365 and mobile device management (MDM), like Intune, administrators to customize the behavior of the app. 

Outlook for iOS and Android supports the following configuration scenarios:

- Account setup configuration
- Organization allowed accounts mode
- Data protection settings

Each configuration scenario will highlight its specific requirements; for example, whether the configuration scenario requires device enrollment, and thus work with any MDM provider, or requires Intune App Protection Policies.
 
## Account setup configuration settings
Outlook for iOS and Android offers administrators the ability to "push" account configurations to their Office 365 users. This capability only works with enrolled devices, however, it is supported with any MDM provider. If you are not using Intune, you will need to consult with your MDM documentation on how to deploy these settings.

|**Key**|**Value**|**Device Enrollment Type**|
|:-----|:-----|:-----|
|com.microsoft.outlook.EmailProfile.EmailAddress  <br/> |This value specifies the email address to be used for sending and receiving mail.  <br/> **Value type**: String  <br/> **Accepted values**: Email address  <br/> **Default if not specified**: \<blank\>  <br/> **Required**: Yes  <br/> **Example**: user@companyname.com  <br/> **Intune Token**<sup>*</sup>: {{mail}}  <br/> |Managed devices  <br/> |
|com.microsoft.outlook.EmailProfile.EmailUPN  <br/> |This value specifies the User Principal Name or username for the email profile that will be used to authenticate the account.  <br/> **Value type**: String  <br/> **Accepted values**: UPN Address or username  <br/> **Default if not specified**: \<blank\>  <br/>**Required**: Yes  <br/> **Example**: userupn@companyname.com  <br/> **Intune Token**<sup>*</sup>: {{userprincipalname}}  <br/> |Managed devices  <br/> |
|com.microsoft.outlook.EmailProfile.AccountType  <br/> |This value specifies the account type being configured based on the authentication model.  <br/> **Value type**: String  <br/> **Accepted values**: ModernAuth  <br/> **Required**: Yes  <br/> **Example**: ModernAuth  <br/> |Managed devices  <br/> |

## Organization allowed account mode settings
Outlook for iOS and Android offers administrators the ability to restrict email and storage provider accounts to only corporate accounts. This capability only works with enrolled devices, however, it is supported with any MDM provider. If you are not using Intune, you will need to consult with your MDM documentation on how to deploy these settings.

|**Key**|**Value**|**Platform**|**Device Enrollment Type**|
|:-----|:-----|:-----|:-----|
|IntuneMAMAllowedAccountsOnly  <br/> |This value specifies the whether organization allowed account mode is active.  <br/> **Value type**: Boolean  <br/> **Accepted values**: True, False  <br/> **Required**: Yes  <br/> **Value**: True  <br/> |iOS  <br/> |Managed devices  <br/> |
|IntuneMAMUPN  <br/> |This value specifies the User Principal Name for the account.  <br/> **Value type**: String  <br/> **Accepted values**: UPN Address  <br/> **Required**: Yes  <br/> **Example**: userupn@companyname.com  <br/> **Intune Token**<sup>*</sup>: {{userprincipalname}}  <br/>  |iOS  <br/> |Managed devices  <br/> |
|com.microsoft.intune.mam.AllowedAccountUPNs  <br/> |This delimited value specifies the UPNs allowed for organization allowed account mode.  <br/> **Accepted values**: UPN Address  <br/> **Required**: Yes  <br/> **Example**: userupn@companyname.com  <br/> |Android  <br/> |Managed devices  <br/> |

## Data protection settings
Outlook for iOS and Android supports app configuration policies for the following data protection settings when the app is managed by Intune:
- Managing the use of wearable technology
- Managing the contact fields synced to the native contacts app

These settings can be deployed to the app regardless of device enrollment status.

### Configure Wearables for Outlook for iOS and Android

By default, Outlook for iOS and Android supports wearable technology, allowing the user to receive message notifications and event reminders, and the ability to interact with messages and view daily calendars. Organizations that want to disable the ability to access corporate data on wearables can deploy the following key via App configuration policies.
  
|**Key**|**Value**|**Device Enrollment Type**|
|:-----|:-----|:-----|
|com.microsoft.intune.mam.areWearablesAllowed  <br/> |This value specifies if Outlook data can be synchronized to a wearable device. Setting the value to False disables wearable synchronization.  <br/> **Accepted values**: True, False  <br/> **Default if not specified**: True  <br/> **Example**: False  <br/> |Managed apps  <br/> |
   
### Configure Contact Field Sync to native Contacts for Outlook for iOS and Android
<a name="contacts"> </a>

The settings in the following table allow you to control the contact fields that will sync between Outlook on iOS and Android and the native Contacts applications.
  
> [!NOTE]
> Outlook for Android supports bi-directional contact synchronization. If a user edits a field in the native contacts app that is restricted (such as the **Notes** field), then that data will not synchronize back into Outlook for Android. 
  
|**Key**|**Value**|**Device Enrollment Type**|
|:-----|:-----|:-----|
|com.microsoft.outlook.ContactSync.AddressAllowed  <br/> |This value specifies if the contact's address should be synchronized to native contacts.  <br/> **Accepted values**: True, False  <br/> **Default if not specified**: True  <br/> **Example**: True  <br/> |Managed apps  <br/> |
|com.microsoft.outlook.ContactSync.BirthdayAllowed  <br/> |This value specifies if the contact's birthday should be synchronized to native contacts.  <br/> **Accepted values**: True, False  <br/> **Default if not specified**: True  <br/> **Example**: True  <br/> |Managed apps  <br/> |
|com.microsoft.outlook.ContactSync.CompanyAllowed  <br/> |This value specifies if the contact's company name should be synchronized to native contacts.  <br/> **Accepted values**: True, False  <br/> **Default if not specified**: True  <br/> **Example**: True  <br/> |Managed apps  <br/> |
|com.microsoft.outlook.ContactSync.DepartmentAllowed  <br/> |This value specifies if the contact's department should be synchronized to native contacts.  <br/> **Accepted values**: True, False  <br/> **Default if not specified**: True  <br/> **Example**: True  <br/> |Managed apps  <br/> |
|com.microsoft.outlook.ContactSync.EmailAllowed  <br/> |This value specifies if the contact's email address should be synchronized to native contacts.  <br/> **Accepted values**: True, False  <br/> **Default if not specified**: True  <br/> **Example**: True  <br/> |Managed apps  <br/> |
|com.microsoft.outlook.ContactSync.InstantMessageAllowed  <br/> |This value specifies if the contact's instant messaging address should be synchronized to native contacts.  <br/> **Accepted values**: True, False  <br/> **Default if not specified**: True  <br/> **Example**: True  <br/> |Managed apps  <br/> |
|com.microsoft.outlook.ContactSync.JobTitleAllowed  <br/> |This value specifies if the contact's job title should be synchronized to native contacts.  <br/> **Accepted values**: True, False  <br/> **Default if not specified**: True  <br/> **Example**: True  <br/> |Managed apps  <br/> |
|com.microsoft.outlook.ContactSync.NicknameAllowed  <br/> |This value specifies if the contact's nickname should be synchronized to native contacts.  <br/> **Accepted values**: True, False  <br/> **Default if not specified**: True  <br/> **Example**: True  <br/> |Managed apps  <br/> |
|com.microsoft.outlook.ContactSync.NotesAllowed  <br/> |This value specifies if the contact's notes should be synchronized to native contacts.  <br/> **Accepted values**: True, False  <br/> **Default if not specified**: True  <br/> **Example**: True  <br/> |Managed apps  <br/> |
|com.microsoft.outlook.ContactSync.PhoneHomeAllowed  <br/> |This value specifies if the contact's home phone number should be synchronized to native contacts.  <br/> **Accepted values**: True, False  <br/> **Default if not specified**: True  <br/> **Example**: True  <br/> |Managed apps  <br/> |
|com.microsoft.outlook.ContactSync.PhoneHomeFaxAllowed  <br/> |This value specifies if the contact's home fax number should be synchronized to native contacts.  <br/> **Accepted values**: True, False  <br/> **Default if not specified**: True  <br/> **Example**: True  <br/> |Managed apps  <br/> |
|com.microsoft.outlook.ContactSync.PhoneMobileAllowed  <br/> |This value specifies if the contact's mobile phone number should be synchronized to native contacts.  <br/> **Accepted values**: True, False  <br/> **Default if not specified**: True  <br/> **Example**: True  <br/> |Managed apps  <br/> |
|com.microsoft.outlook.ContactSync.PhoneOtherAllowed  <br/> |This value specifies if the contact's other phone number should be synchronized to native contacts.  <br/> **Accepted values**: True, False  <br/> **Default if not specified**: True  <br/> **Example**: True  <br/> |Managed apps  <br/> |
|com.microsoft.outlook.ContactSync.PhonePagerAllowed  <br/> |This value specifies if the contact's pager phone number should be synchronized to native contacts.  <br/> **Accepted values**: True, False  <br/> **Default if not specified**: True  <br/> **Example**: True  <br/> |Managed apps  <br/> |
|com.microsoft.outlook.ContactSync.PhoneWorkAllowed  <br/> |This value specifies if the work phone number should be synchronized to native contacts.  <br/> **Accepted values**: True, False  <br/> **Default if not specified**: True  <br/> **Example**: True  <br/> |Managed apps  <br/> |
|com.microsoft.outlook.ContactSync.PhoneWorkFaxAllowed  <br/> |This value specifies if the contact's work fax number should be synchronized to native contacts.  <br/> **Accepted values**: True, False  <br/> **Default if not specified**: True  <br/> **Example**: True  <br/> |Managed apps  <br/> |
|com.microsoft.outlook.ContactSync.PrefixAllowed  <br/> |This value specifies if the contact's name prefix should be synchronized to native contacts.  <br/> **Accepted values**: True, False  <br/> **Default if not specified**: True  <br/> **Example**: True  <br/> |Managed apps  <br/> |
|com.microsoft.outlook.ContactSync.SuffixAllowed  <br/> |This value specifies if the contact's name suffix should be synchronized to native contacts.  <br/> **Accepted values**: True, False  <br/> **Default if not specified**: True  <br/> **Example**: True  <br/> |Managed apps  <br/> |
   
## Deploying the configuration scenarios with Microsoft Intune

If you are using Microsoft Intune as your mobile device management provider, the following steps will allow you to create an app configuration policy. After the configuration is created, you can assign its settings to groups of users.

> [!NOTE]
> Intune managed apps will check-in with an interval of 30 minutes for Intune App Configuration Policy status, when deployed in conjunction with an Intune App Protection Policy. If an Intune App Protection Policy isn't assigned to the user, then the Intune App Configuration Policy check-in interval is set to 720 minutes.

### Create an app configuration policy for Outlook for iOS and Android
  
1. Sign in to the Azure portal.
    
2. Select **More Services** \> **Monitoring + Management** \> **Intune**.
    
3. On the **Mobile apps** blade of the Manage list, select **App configuration policies**.
    
4. On the **App Configuration policies** blade, choose **Add**. 
    
5. On the **Add app configuration** blade, enter a **Name**, and optional **Description** for the app configuration settings. 
    
6. For **Device enrollment** type, choose **Managed apps** or **Managed devices** depending on the configuration scenario you are deploying (see the specific configuration scenario for more information).
    
7. If you chose **Managed devices** you will have another option, **Platform**. For **Platform**, choose either **iOS** or **Android**.

8. For **Associated app**, choose **Select the required app**, and then, on the **Targeted apps** blade, choose **Outlook**. If you specified, **Managed apps**, select both the iOS and Android platform Outlook apps. 
    
    > [!NOTE]
    > If Outlook is not listed as an available app, then you must add it by following the instructions in [Add Android store apps to Microsoft Intune](https://docs.microsoft.com/intune/store-apps-android) and [Add iOS store apps to Microsoft Intune](https://docs.microsoft.com/intune/store-apps-ios). 
  
9. Click **OK** to return to the **Add app configuration** blade. 
    
10. Choose **Configuration Settings**. On the **Configuration** blade, define the key and value pairs that will supply configurations for Outlook for iOS and Android. The key and value pairs you can define are described in the following sections. 
    
11. When you are done, choose **OK**.
    
12. On the **Add app configuration** blade, choose **Add**.
    
The newly created configuration will be displayed on the **App configuration** blade. 

>[!NOTE]
> If you selected **Managed devices**, you will need to create a separate app configuration policy for each platform.
  
### Assign the configuration settings that you created

You assign the settings to groups of users in Azure Active Directory. When a user has the Microsoft Outlook app installed, the app will be managed by the settings you have specified. To do this:
  
1. From the **Intune** blade, on the **Mobile apps** blade of the Manage list, select **App configuration policies**.
    
2. From the list of app configuration policies, select the one you want to assign.
    
3. On the next blade, choose **Assignments**.
    
4. On the **Assignments** blade, select the Azure AD group to which you want to assign the app configuration, and then choose **OK**.
