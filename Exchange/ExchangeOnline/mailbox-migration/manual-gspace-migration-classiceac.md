---
title: Perform manual Google Workspace migration in Classic Exchange admin center in Exchange Online
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

# Perform Google Workspace Migration to Microsoft 365 or Office 365 in Classic EAC in Exchange Online

The migration process takes several steps and can take from several hours to a couple of days depending on the amount of data you are migrating.

## Prerequisites

Before you begin Google Workspace migration:

1. Ensure you are signed into Google Workspace as a project creator.
2. You have completed the following procedures:
    1. Create a subdomain for mail routing to Microsoft 365 or Office 365
    2. Create a subdomain for mail routing to your Google Workspace domain
    3. Provision users in Microsoft 365 or Office 365

For more information, see [Prerequisites](googleworkspace-migration-prerequisites.md).

## Manual Google Workspace migration process

The process to manually migrate Google Workspace involves following steps:

1. [Create a Google Service Account](#create-a-google-service-account)
2. [Enable API Usage in your project](#enable-api-usage-in-your-project)
3. [Grant access to the service account for your Google tenant](#grant-access-to-the-service-account-for-your-google-tenant)
4. [Start a Google Workspace migration batch with the Classic Exchange admin center (Classic EAC)](#start-a-google-workspace-migration-batch-with-the-classic-exchange-admin-center-classic-eac)

### Create a Google Service Account

1. Using a Chrome browser, sign into your Google Workspace admin console at [admin.google.com](https://admin.google.com).
2. In a new tab or window, navigate to the [Service Accounts](https://console.developers.google.com/iam-admin/serviceaccounts) page.
3. Select **Create project**, name the project and choose **Create**.
4. Select **+ Create service account**, enter a name, choose **Create** and then **Done**.
5. Open the **Actions** menu, select **Edit**, and take note of the Unique ID. You'll need this ID later in the process.
6. Open the **Show domain-wide delegation** section.
7. Select **Enable G Suite Domain-wide Delegation**, enter a product name for the consent screen, and choose **Save**.

   > [!NOTE]
   > The product name is not used by the migration process, but is needed to save in the dialog.

8. Open the **Actions** menu again and select **Create key**.
9. Choose **JSON**, then **Create**.
   The private key is saved to the download folder on your device.
10. Select **Close**.

### Enable API usage in your project

If your project doesn't already have all of the required APIs enabled, you must enable them.

1. Go to the [Developer page for API Library](https://console.developers.google.com/apis/library) and sign in as the Google user you used above in **Create a Google Service Account**.

2. Select the project that you used above.

3. Search for the following APIs; each one must be enabled. Select **Enable** to enable them for your project:
   - Gmail API
   - Google Calendar API
   - Contacts API
   - People API

### Grant access to the service account for your Google tenant

1. Go to the [Google Workspace Admin page](https://admin.google.com/AdminHome) and sign in as Google Workspace admin for your tenant.

2. Click **Security**, then click **API Controls**, and then click **Manage Domain Wide Delegation**.

3. Next to the **API Clients** list, click **Add new**.

4. In **Client ID**, type the ClientId for the service account you created in the [Create a Google Service Account](#create-a-google-service-account) section above.

   ![Add new API client.](../media/add-a-new-client-id-im7.png)

5. In **OAuth Scopes**, add the required scopes in comma-separated format, with no spaces in between. For example: </br></br> `https://mail.google.com/,https://www.googleapis.com/auth/calendar,https://www.google.com/m8/feeds/,https://www.googleapis.com/auth/gmail.settings.sharing,https://www.googleapis.com/auth/contacts`

    If the OAuth Scopes are entered incorrectly, the resulting list won't match and the migration process will fail later, after you start the migration batch.

6. Click **Authorize**. Verify that the resulting list shows the expected four (4) OAuth scopes.

   > [!Important]
   > It may take anywhere from 15 minutes to 24 hours for these settings to propogate.

### Start a Google Workspace migration batch with the Classic Exchange admin center (Classic EAC)

1. In the Exchange Admin center, click **recipients**, and then click **migration**.

2. Click "New"  ![New.](../media/ITPro_EAC_AddIcon.gif) to create a new migration batch, and then click **Migrate to Exchange Online**.

3. In the New Migration Batch window, select **G Suite (Gmail) migration**, and then click **Next**.

   ![Choose Gsuite.](../media/gsuite-mig-13-eac-choose-gsuite.png)

4. Create a CSV file containing the set of all of the users you want to migrate. You will need its filename below. The allowed headers are:

   - EmailAddress (required). Contains the primary email address for an existing Microsoft 365 or Office 365 mailbox.

   - Username (optional). Contains the Gmail primary email address, if it differs from EmailAddress.

   ```CSV
   EmailAddress
   will@fabrikaminc.net
   user123@fabrikaminc.net
   ```

5. Under **Select the users**, click **Choose File** and navigate to the CSV file of all the users you are migrating in this batch. If your CSV file contains more columns besides the two mentioned above, click to select **Allow unknown columns in the CSV file**.

   ![Csv file.](../media/gsuite-mig-14-eac-csv.png)

6. After selecting the CSV file, click **Open**. Back on the **new migration batch** page, click **Next**.

7. Enter the email address for the super admin within the Google Workspace environment. This is not the service account you just created, it should be the email address of the Google Workspace admin. This email address will be used to test connectivity between Google Workspace and Microsoft 365 or Office 365.

8. Under **Specify the service account credentials using the JSON key file**, click **Choose File**, and then select the JSON file that was downloaded automatically when you created your service account. This file contains the private key for the service account. Click **Open** to select the file, and then, back on the **new migration batch** page, click **Next**.

   ![user email address.](../media/gsuite-mig-15-eac-user.png)

   > [!NOTE]
   > Click to select **Skip verification** if you don't want to verify the migration endpoint.

9. In the fields under **Move configuration**, name your migration batch, and enter the target delivery domain, which is the [domain you created](googleworkspace-migration-prerequisites.md#create-a-subdomain-for-mail-routing-to-microsoft-365-or-office-365) for routing mail to the Microsoft 365 or Office 365 target organization from the Google Workspace source organization. Optionally, you can also specify any folders that should be excluded from the migration. When done, click **Next**.

   ![batch name.](../media/gsuite-mig-16-eac-batch.png)

   > [!NOTE]
   > The target delivery domain you will want to use will not automatically show up in the dropdown - instead you should click within the text box and type it in. The target delivery domain must be different from the primary domain of the users in Google Workspace.

10. Decide how you want to begin and complete the migration batch.

To learn more about:

- Completion of migration batch, see [Completion of migration batch in Classic EAC](completion-gspace-migration-batch-classiceac.md).
- How the migration happens in backend, see [Overview of the process](how-it-all-works-in-the-backend.md).
