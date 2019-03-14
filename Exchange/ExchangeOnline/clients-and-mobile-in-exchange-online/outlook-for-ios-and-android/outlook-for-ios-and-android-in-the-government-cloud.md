---
localization_priority: Normal
description: 'Summary: How organizations in the Office 365 U.S. Government Community Cloud (GCC) can enable Outlook for iOS and Android for their users.'
ms.topic: article
author: msdmaguire
ms.author: dmaguire
ms.assetid: 73b693d9-39bb-4689-a1ff-4be505a5945b
ms.date: 
title: Using Outlook for iOS and Android in the Government Community Cloud
ms.collection: 
- exchange-online
- M365-email-calendar
ms.reviewer: smithre4
ms.audience: ITPro
ms.service: exchange-online
manager: serdars

---

# Using Outlook for iOS and Android in the Government Community Cloud

 **Summary**: How organizations in the Office 365 U.S. Government Community Cloud (GCC) can enable Outlook for iOS and Android for their users.

Outlook for iOS and Android is fully architected in the Microsoft Cloud and meets the security and compliance requirements needs of all United States Government customers. 

For customers operating in Government Community Cloud (GCC) Moderate, Outlook for iOS and Android's [architecture](https://docs.microsoft.com/exchange/clients-and-mobile-in-exchange-online/outlook-for-ios-and-android/outlook-for-ios-and-android)  routes data through Azure Government Community data centers (the Azure Government Community Cloud). This solution is FedRAMP-compliant and approved, which means the Outlook for iOS and Android architecture and underlying translation protocol service now meet the data-handling requirements for GCC tenants (these requirements are defined by NIST Special Publication 800-145). 

For customers operating GCC High or Department of Defense, Outlook for iOS and Android leverages the [native Microsoft sync technology](https://docs.microsoft.com/exchange/clients-and-mobile-in-exchange-online/outlook-for-ios-and-android/outlook-for-ios-and-android). This architecture meets GCC High and DoD requirements DISA SRG Level 4 (GCC-High) and Level 5 (DoD), Defense Federal Acquisition Regulations Supplement (DFARS), and International Traffic in Arms Regulations (ITAR), which have been approved by a third-party assessment organization and are FISMA compliant based on the NIST 800-53 rev 4.

For more information, please see the Office 365 FedRAMP System Security plan located in the FedRAMP Audit Reports section of the [Microsoft Service Trust Portal](https://servicetrust.microsoft.com/).

This article covers how to:

- Enable Outlook for iOS and Android for Office 365 GCC High and Department of Defense customers.

- Enable Outlook for iOS and Android for new Office 365 GCC Moderate customers.

- Unblock Outlook for iOS and Android for existing Office 365 GCC Moderate customers who were blocked from the Microsoft Azure public cloud.

- Migrate Office 365 GCC Moderate mobile users from the Azure public cloud to the O365 GCC compliant solution. This applies to tenants who had been previously unblocked from the Azure public cloud through signing a waiver with Microsoft Support.

## Enabling Outlook for iOS and Android for Office 365 GCC High and Department of Defense customers

GCC High and Department of Defense customers can leverage Outlook for iOS and Android without any special configuration.

## Enabling Outlook for iOS and Android for Office 365 GCC Moderate customers

For Office 365 GCC Moderate customers who are not currently using Outlook for iOS and Android, enabling the app requires unblocking Outlook for iOS and Android in the organization, downloading the app on users' devices, and having end-users enable GCC mode on their devices.

 **1. Unblock Outlook for iOS and Android**

Remove any restrictions placed within your Exchange environment that may be blocking Outlook for iOS and Android. This means you'll need to update your Exchange Web Services application policies, your Exchange mobile device access rules, or any relevant Azure Active Directory Conditional Access policies so that the app is no longer blocked. See [Securing Outlook for iOS and Android in Exchange Online](secure-outlook-for-ios-and-android.md) for information about enabling Outlook as the only mobile messaging client in an organization.

 **2. Download and install Outlook for iOS and Android**

End users need to install the app on their devices. How the installation happens depends on whether or not the devices are enrolled in a mobile device management (MDM) solution, such as Microsoft Intune. Users with enrolled devices can install the app through their MDM solution, like the Intune Company Portal. Users with devices that are not enrolled in an MDM solution can search for "Microsoft Outlook" in the Apple App Store or Google Play Store and download it from one of those locations.

> [!NOTE]
> To leverage app-based conditional access policies, the Microsoft Authenticator app must be installed on iOS devices. For Android devices, the Intune Company Portal app is leveraged. For more information, see [App-based conditional access with Intune](https://docs.microsoft.com/intune/app-based-conditional-access-intune).

 **3. Have end users enable GCC mode on their devices**

> [!IMPORTANT]
> GCC High and DoD customers must not use the GCC mode option as that will prevent connectivity to Office 365. The GCC mode toggle will be removed from Outlook for iOS and Android by April 1st.

Share the following instructions with your end-users so that they can enable GCC mode on their devices. The instructions depend on the operating system of each device.

For iOS devices:

1. Open Settings in iOS, scroll to find Outlook, and then tap to select it.

2. In Outlook settings, slide the toggle beside **Restrict app to GCC accounts** so that the feature is enabled. If you're asked to remove existing accounts, say Yes. Then, exit Settings.

3. Open Outlook, and then add your Office 365 GCC account by following the on-screen instructions, using your Office 365 GCC email account and credentials.

For Android devices that have a new installation of Outlook for Android (i.e. no existing email accounts):

1. Open Outlook on the Android device.

2. On the initial screen, tap to select **Restrict app to GCC mode**.

3. Add your Office 365 GCC account by following the on-screen instructions, using your Office 365 GCC email account and credentials.

For Android devices that already have Outlook for Android installed:

1. Open Outlook, and then go to Settings.

2. Slide the toggle beside **GCC mode** so that the feature is enabled. You will get a pop-up message informing you that your accounts and settings will be removed and that you'll only be able to add GCC accounts. Tap **Apply**.

3. The app should automatically re-start. If it doesn't, manually close and re-start the app.

4. Follow the on-screen instructions to add your Office 365 GCC account, making sure GCC mode is on.

## Services and features not available

By default, certain services and features of Outlook for iOS and Android are disabled automatically for the Office 365 U.S. Government Community Cloud (GCC) because they do not meet FedRAMP requirements:

- **In-app support**: Users will not be able to submit support tickets from within the app. They should contact their internal help desk and provide logs (via the Share Diagnostics Logs option in Setting -> Help). If necessary, the organization's IT department can then contact Microsoft Support directly.

- **In-app feature requests**: Users will not be able to submit in-app feature requests. Instead, users will be directed to use [Outlook Uservoice](http://outlook.uservoice.com).

- **Multiple accounts**: Only the user's Office 365 GCC account and OneDrive for Business account can be added to a single device. Personal accounts cannot be added. Customers can use another device for personal accounts, or an ActiveSync client from another provider.

- **Calendar Apps**: Calendar apps (Facebook, Wunderlist, Evernote, Meetup) are not available with GCC accounts.

- **Add-Ins**: Add-ins are not available with GCC accounts.

- **Storage Providers**: Only the GCC user's OneDrive for Business storage account can be added within Outlook for iOS and Android. Third-party storage accounts (e.g., Dropbox, Box) cannot be added.

- **Location services**: Bing location services are not available with GCC accounts. Features that rely on location services, like Cortana Time To Leave, are also unavailable.

- **Favorites**: Favorite folders, groups and people are not available with GCC accounts.

- **MailTips**: The External recipients MailTip is not available with GCC accounts.

- **Office Lens**: Office Lens technology (e.g., scanning business cards, taking pictures) included in Outlook for iOS and Android is not available with GCC accounts.

Executing the below Exchange Online cmdlet will enable GCC Moderate, High, or DoD customers using Outlook for iOS and Android access to features and services that are not FedRAMP compliant:

 ```
  Set-OrganizationConfig -OutlookMobileGCCRestrictionsEnabled $false
 ```

> [!NOTE]
> Setting OutlookMobileGCCRestrictionsEnabled to false currently does not remove the service and feature restrictions placed on Outlook for iOS and Android. This behavior is planned to change in April 2019.

At any time, access can be revoked by resetting the parameter back to the default value:

 ```
  Set-OrganizationConfig -OutlookMobileGCCRestrictionsEnabled $true
 ```

Changing this setting typically takes affect within an hour. As this is an tenant-based change, all Outlook for iOS and Android users in the GCC organization will be affected. 

> [!NOTE]
> After April 2019, users will not need to leverage the GCC mode option within the client with the above Exchange Online setting.

For more information on the cmdlet, please see [Set-OrganizationConfig](https://docs.microsoft.com/powershell/module/exchange/organization/set-organizationconfig?view=exchange-ps). 
