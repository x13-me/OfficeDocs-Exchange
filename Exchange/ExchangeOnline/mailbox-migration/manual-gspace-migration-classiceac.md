---
title: "Perform manual Google Workspace migration in Classic Exchange Admin Center"
ms.author: v-aiyengar
author: AshaIyengar21
manager: serdars
audience: Admin
ms.topic: conceptual
ms.service: exchange-online
localization_priority: Normal
search.appverid: MET150
f1.keywords:
- NOCSH
description: Instructions for manually migrating from Google Workspace to Microsoft 365 or Office 365 in stages by migrating users in batches in Classic EAC.
ms.custom: seo-marvel-jun2021
---

# Perform Google Workspace Migration to Microsoft 365 or Office 365 in Classic EAC

The migration process takes several steps and can take from several hours to a couple of days depending on the amount of data you are migrating.

The process to manually migrate Google Workspace involves following steps:

1. [Create a Google Service Account](#create-a-google-service-account)
1. [Enable API Usage in your project](#enable-api-usage-in-your-project)
1. [Grant access to the service account for your Google tenant](#grant-access-to-the-service-account-for-your-google-tenant)
1. [Create a subdomain for mail routing to Microsoft 365 or Office 365](#create-a-subdomain-for-mail-routing-to-microsoft-365-or-office-365)
1. [Create a subdomain for mail routing to your Google Workspace domain](#create-a-subdomain-for-mail-routing-to-your-google-workspace-domain)
1. [Provision users in Microsoft 365 or Office 365](#provision-users-in-microsoft-365-or-office-365)
1. [Start a Google Workspace migration batch with the Classic Exchange admin center (Classic EAC)](#start-a-google-workspace-migration-batch-with-the-classic-exchange-admin-center-classic-eac)

## Create a Google Service Account

1. Using a Chrome browser, sign into your Google Workspace admin console at [admin.google.com](https://admin.google.com). 
1. In a new tab or window, navigate to the [Service Accounts](https://console.developers.google.com/iam-admin/serviceaccounts) page. 
1. Select **Create project**, name the project and choose **Create**. 
1. Select **+ Create service account**, enter a name, choose **Create** and then **Done**. 
1. Open the **Actions** menu, select **Edit**, and take note of the Unique ID. You’ll need this ID later in the process. 
1. Open the **Show domain-wide delegation** section. 
1. Select **Enable G Suite Domain-wide Delegation**, enter a product name for the consent screen, and choose **Save**.
> [!NOTE]
> The product name is not used by the migration process, but is needed to save in the dialog.
8. Open the **Actions** menu again and select **Create key**. 
1. Choose **JSON**, then **Create**. 
   The private key is saved to the download folder on your device.
1. Select **Close**. 

## Enable API usage in your project

If your project doesn't already have all of the required APIs enabled, you must enable them.

1. Go to the [Developer page for API Library](https://console.developers.google.com/apis/library) and sign in as the Google user you used above in **Create a Google Service Account**.

2. Select the project that you used above.

3. Search for the following APIs; each one must be enabled. Select **Enable** to enable them for your project:

   - Gmail API
   - Google Calendar API
   - Contacts API
   - People API

## Grant access to the service account for your Google tenant

1. Go to the [Google Workspace Admin page](https://admin.google.com/AdminHome) and sign in as Google Workspace admin for your tenant.

2. Click **Security**, then click **API Controls**, and then click **Manage Domain Wide Delegation**.

3. Next to the **API Clients** list, click **Add new**.

4. In **Client ID**, type the ClientId for the service account you created in the [Create a Google Service Account](#create-a-google-service-account) section above.

   ![Add new API client](../media/add-a-new-client-id-im7.png)

5. In **OAuth Scopes**, add the required scopes in comma-separated format, with no spaces in between. For example: </br></br> `https://mail.google.com/,https://www.googleapis.com/auth/calendar,https://www.google.com/m8/feeds/,https://www.googleapis.com/auth/gmail.settings.sharing,https://www.googleapis.com/auth/contacts` 

    If the OAuth Scopes are entered incorrectly, the resulting list won't match and the migration process will fail later, after you start the migration batch.

6. Click **Authorize**. Verify that the resulting list shows the expected four (4) OAuth scopes.

   > [!Important]
   > It may take anywhere from 15 minutes to 24 hours for these settings to propogate.

## Create a subdomain for mail routing to Microsoft 365 or Office 365

1. Go to the [Google Workspace Admin page](https://admin.google.com/AdminHome) and sign in as a Google Workspace admin for your tenant.

2. Click **Domains**, then **Manage domains**, and then click **Add a domain**.

   > [!NOTE]
   > The option _Add a domain_ will not be available if using the legacy free edition of G Suite.

3. Enter the domain that you will use for routing mails to Microsoft 365 or Office 365, then click **Continue and verify domain ownership**. A subdomain of your primary domain is recommended (such as "o365.fabrikaminc.net" when "fabrikaminc.net" is your primary domain) so that it will be automatically verified. Keep track of the name of the domain you enter because you will need it for the following steps, and later in the instructions as the Target Delivery Domain when you [Create a migration batch in Microsoft 365 or Office 365](perform-gspace-migration-powershell.md#create-a-migration-batch-in-microsoft-365-or-office-365).

   > [!NOTE]
   > A sub-domain of your primary domain is recommended. If another domain (such as "fabrikaminc.onmicrosoft.com") is set, Google will send emails to each individual address with a link to verify the permission to route mail. Migration won't complete until the verification is completed.

   ![Add domain](../media/add-a-new-domain-im8.png)

4. Follow any subsequent steps that are then required to verify your domain, making sure that the status is shown as **Active**. If you chose a subdomain of your primary domain in step 3 above, your new domain may have been verified automatically.

   ![Verify domain](../media/verify-ownership-im9.png)

5. Log into your DNS provider and update your DNS records so that you have an MX record at the domain you created above in step 3, pointing to Microsoft 365 or Office 365. Ensure that this domain that you created above is an accepted domain in Microsoft 365 or Office 365. Follow the instructions in [Add a domain to Microsoft 365](/microsoft-365/admin/setup/add-domain) to add the Microsoft 365 or Office 365 routing domain ("o365.fabrikaminc.net") to your organization and to configure DNS to route mail to Microsoft 365 or Office 365.

> [!NOTE]
> The migration process won't be able to complete if a routing domain is used that is not verified as described above. Choosing the built-in "tenantname.onmicrosoft.com" domain for routing mail to Office 365 instead of a sub-domain of the primary Google Workspace domain occasionally causes issues that Microsoft is not able to assist with besides to recommend that the user manually verify the forwarding address or contact Google support.

## Create a subdomain for mail routing to your Google Workspace domain

1. Go to the [Google Workspace Admin page](https://admin.google.com/AdminHome) and sign in as a Google Workspace admin for your tenant.

2. Click **Domains**, then **Manage domains**, and then click **Add a domain alias**.

3. Enter the domain that you will use for routing mails to Google Workspace, then click **Continue and verify domain ownership**. A subdomain of your primary domain is recommended (such as "gsuite.fabrikaminc.net" when "fabrikaminc.net" is your primary domain) so that it will be automatically verified.

   ![Add domain alias](../media/add-a-new-domain-alias-im10.png)

4. Follow any subsequent steps that are then required to verify your domain, making sure that the status is shown as **Active**. If you chose a subdomain of your primary domain in step 3 above, your new domain may have been verified automatically.

   ![Verify domain](../media/verify-ownership-im9.png)

5. Follow Google's instructions to [Set up MX records for Google Workspace Gmail](https://support.google.com/a/answer/140034) for this domain.

   > [!NOTE]
   > It may take up to 24 hours for Google to propagate this setting to all of the users in your organization.

   > [!IMPORTANT]
   > If you are using non-default Transport settings in your Microsoft 365 or Office 365 organization, you should check that mail flow will work from Office 365 to Google Workspace. Be sure that either your default Remote Domain ("\*") has Automatic Forwarding enabled, or that there is a new Remote Domain for your Google Workspace routing domain (e.g. "gsuite.fabrikaminc.net") that has Automatic Forwarding enabled.

## Provision users in Microsoft 365 or Office 365

Once your Google Workspace environment has been properly configured, you can complete your migration in the Exchange admin center or through the Exchange Online PowerShell.

Before proceeding with either method, make sure that Mail Users have been provisioned for every user in the organization who will be migrated (either now or eventually). If any users aren't provisioned, provision them using the instructions in [Manage mail users](../recipients-in-exchange-online/manage-mail-users.md).

For more advanced scenarios, you may be able to deploy Azure Active Directory (Azure AD) Connect to provision your Mail Users. See [Deploy Microsoft 365 Directory Synchronization in Microsoft Azure](/office365/enterprise/deploy-office-365-directory-synchronization-dirsync-in-microsoft-azure) for an overview, and [Set up directory synchronization for Microsoft 365](/office365/enterprise/set-up-directory-synchronization) for setup instructions. Then, you need to deploy an Exchange server in your on-premises environment for user management, and mail-enable your users using this server. For more information, see [How and when to decommission your on-premises Exchange servers in a hybrid deployment](../../ExchangeHybrid/decommission-on-premises-exchange.md) and [Manage mail users](/Exchange/ExchangeServer/recipients/mail-users.md). Once the Mail Users have been created in Microsoft 365, the Azure AD Connect may need to be disabled in order to allow the migration process to convert these users into mailboxes - see [Turn off directory synchronization for Microsoft 365](/office365/enterprise/turn-off-directory-synchronization).

We recommend that the primary address (sometimes referred to as the "User ID") for each user be at the primary domain (such as "will@fabrikaminc.net"). Typically, this means that the primary email address should match between Microsoft 365 or Office 365 and Google Workspace. If any user is provisioned with a different domain for their primary address, then that user should at least have a proxy address at the primary domain. Each user should have their `ExternalEmailAddress` point to the user in their Google Workspace routing domain ("will@gsuite.fabrikaminc.net"). The users should also have a proxy address that will be used for routing to their Microsoft 365 or Office 365 routing domain (such as "will@o365.fabrikaminc.net").

> [!NOTE]
> We recommend that the Default MRM Policy and Archive policies be disabled for these users until after their migration has been completed.  When such features remain enabled during migration, there is a chance that some messages will end up being considered "missing" during the content verification process.

## Start a Google Workspace migration batch with the Classic Exchange admin center (Classic EAC)

1. In the Exchange Admin center, click **recipients**, and then click **migration**.

2. Click "New"  ![New](../media/ITPro_EAC_AddIcon.gif) to create a new migration batch, and then click **Migrate to Exchange Online**.

3. In the New Migration Batch window, select **G Suite (Gmail) migration**, and then click **Next**.

   ![Choose Gsuite](../media/gsuite-mig-13-eac-choose-gsuite.png)

4. Create a CSV file containing the set of all of the users you want to migrate. You will need its filename below. The allowed headers are:

   - EmailAddress (required). Contains the primary email address for an existing Microsoft 365 or Office 365 mailbox.

   - Username (optional). Contains the Gmail primary email address, if it differs from EmailAddress.

   ```CSV
   EmailAddress
   will@fabrikaminc.net
   user123@fabrikaminc.net
   ```

5. Under **Select the users**, click **Choose File** and navigate to the CSV file of all the users you are migrating in this batch. If your CSV file contains more columns besides the two mentioned above, click to select **Allow unknown columns in the CSV file**.

   ![Csv file](../media/gsuite-mig-14-eac-csv.png)

6. After selecting the CSV file, click **Open**. Back on the **new migration batch** page, click **Next**.

7. Enter the email address for the super admin within the Google Workspace environment. This is not the service account you just created, it should be the email address of the Google Workspace admin. This email address will be used to test connectivity between Google Workspace and Microsoft 365 or Office 365.

8. Under **Specify the service account credentials using the JSON key file**, click **Choose File**, and then select the JSON file that was downloaded automatically when you created your service account. This file contains the private key for the service account. Click **Open** to select the file, and then, back on the **new migration batch** page, click **Next**.

   ![user email address](../media/gsuite-mig-15-eac-user.png)

   > [!NOTE]
   > Click to select **Skip verification** if you don't want to verify the migration endpoint.

9. In the fields under **Move configuration**, name your migration batch, and enter the target delivery domain, which is the domain [you created](#create-a-subdomain-for-mail-routing-to-microsoft-365-or-office-365) for routing mail to the Microsoft 365 or Office 365 target organization from the Google Workspace source organization. Optionally, you can also specify any folders that should be excluded from the migration. When done, click **Next**.

   ![batch name](../media/gsuite-mig-16-eac-batch.png)

   > [!NOTE]
   > The target delivery domain you will want to use will not automatically show up in the dropdown - instead you should click within the text box and type it in. The target delivery domain must be different from the primary domain of the users in Google Workspace.

1. Decide how you want to begin and complete the migration batch.
 
To learn more about:

- Completion of migration batch, see [Completion of migration batch in Classic EAC](completion-gspace-migration-batch-classiceac.md).

- How the migration happens in backend, see [Overview of the process](how-it-all-works-in-the-backend.md).
