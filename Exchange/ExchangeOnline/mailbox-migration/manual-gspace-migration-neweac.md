---
title: "Perform manual Google Workspace migration in new Exchange Admin Center"
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
description: Instructions for manually migrating from Google Workspace to Microsoft 365 or Office 365 in stages by migrating users in batches in new EAC.
ms.custom: seo-marvel-jun2021
---

# Perform Google Workspace Migration to Microsoft 365 or Office 365 in new EAC

The migration process takes several steps and can take from several hours to a couple of days depending on the amount of data you are migrating.

## Prerequisites:

Before you begin Google Workspace migration:

1. Ensure you are signed into Google Workspace as a project creator.
1. You have completed the following procedures:
    1. Create a subdomain for mail routing to Microsoft 365 or Office 365
    1. Create a subdomain for mail routing to your Google Workspace domain
    1. Provision users in Microsoft 365 or Office 365
    
For more information, see [Prerequisites](googleworkspace-migration-prerequisites.md).

## Start a Google Workspace migration batch with the new Exchange admin center (New EAC)

> [!IMPORTANT]
> Microsoft's data migration tool is currently unaware of tools enforcing messaging records management (MRM) or archival policies. Because of this, any messages that are deleted or moved to archive by these policies will result in the migration process flagging these items as "missing". The result is perceived data loss rather than actual data loss, which makes it much harder to identify actual data loss during any content verification checks. <br/><br/>Therefore, Microsoft strongly recommends disabling all MRM and archival policies before attempting any data migration to mailboxes.

1. In the new [Exchange Admin center](https://admin.exchange.microsoft.com/#/), navigate to **Migration**, and click **Add migration batch**.

2. Under **Add migration batch**:
    1. Enter the unique batch name, select the mailbox migration path and click **Next**.
    1. From the **Select the migration type** drop-down list, select **Google Workspace (Gmail) migration** and click **Next**.
   ![Migration Onboarding](../media/migration-onboarding-selection.png)
    3. In **Prerequisites** section, perform the following procedures to manually configure G-Suite for migration:
        1. [Create a Google Service Account](#create-a-google-service-account)
        1. [Enable API Usage in your project](#enable-api-usage-in-your-project)
        1. [Grant access to the service account for your Google tenant](#grant-access-to-the-service-account-for-your-google-tenant)
        For detailed information on the procedures, see [Manually configuring G-Suite for migration](manually-configuring-gsuite-for-migration.md).
    1. In **Set A migration endpoint** section, you can do one of the following:
        1. If you have already created an endpoint, select the migration endpoint from the drop-down list.
        1. If you are a first time user, then select **Create a new migration endpoint** and click **Next**.
         ![Set endpoint](../media/migration-endpoint-selection.png)

        > [!NOTE]
        > To migrate Gmail mailboxes successfully, Microsoft 365 or Office 365 needs to connect and communicate with Gmail. To do this, Microsoft 365 or Office 365 uses a migration endpoint. Migration endpoint is a technical term that describes the settings that are used to create the connection so you can migrate the mailboxes.
        1. Under **General Information**. provide a **Migration Endpoint Name**. The fields for **Maximum concurrent migrations** and **Maximum concurrent incremental syncs** have the default values. You can either retain them or change them as per your requirement. 
        1. Click **Next**.
        1. Under **Gmail migration configuration**, enter the **Email address**. This is the same email address that you signed in to the Google Workspace.
        1. Click **Import JSON**, and select the downloaded JSON file, and then click **Next**.
        Once the endpoint is successfully created, it will be listed under **Select migration endpoint** drop-down.
        1. Select the endpoint from the drop-down list, and click **Next**.
        1.  In **Add user mailboxes** section, click **Import CSV file** and navigate to the folder where you have saved the CSV file.
        Create a CSV file containing the set of all of the users you want to migrate. You will need its filename below. The allowed headers are:

            - EmailAddress (required). Contains the primary email address for an existing Microsoft 365 or Office 365 mailbox.

            - Username (optional). Contains the Gmail primary email address, if it differs from EmailAddress.

              ```CSV
              EmailAddress
              will@fabrikaminc.net
              user123@fabrikaminc.net
              ```
6. In **Move configuration** section, enter the details and click **Next**.

7. In **Schedule batch migration** section, verify all the details, click **Save**, and then click **Done**.

    ![Schedule batch migration](../media/schedule-batch1-migration.png)

    Once the batch status changes from **Syncing** to **Synced**, you need to complete the batch.

To learn more about:

- Completion of migration batch, see [Completion of migration batch in new EAC](completion-gspace-migration-batch-neweac.md).

- How the migration happens in backend, see [Overview of the process](how-it-all-works-in-the-backend.md).


