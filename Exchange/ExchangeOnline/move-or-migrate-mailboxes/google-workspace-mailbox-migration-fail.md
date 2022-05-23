---
title: Can't migrate Google Workspace mailboxes to Microsoft 365
description: Unable to migrate mailboxes from Google Workspace to Microsoft 365 because the app passwords aren't set for these mailboxes. 
author: MaryQiu1987
ms.author: v-maqiu
manager: dcscontentpm
audience: ITPro
ms.topic: troubleshooting
localization_priority: Normal
ms.custom: 
  - CI 163330
  - Exchange Online
  - CSSTroubleshoot
ms.reviewer: shahmul, ninob
appliesto: 
  - Exchange Online
  - Microsoft 365
search.appverid: MET150
ms.date: 5/23/2022
---
# Error during mailbox migration from Google Workspace to Microsoft 365

## Symptoms

When you perform a mailbox migration from Google Workspace to Microsoft 365, the migration fails with the following error message:

> Error MigrationPermanentException: Special credentials are required in order to access this IMAP account. --> Imap server reported an error during LOGIN with the following alert: 'Application-specific password required: `https://support.google.com/accounts/answer/185833` (Failure).

If you generate a diagnostic report about the migration, you'll see the same error message listed in it as well.

## Cause

To migrate a mailbox from Google Workspace to Microsoft 365, you must set up 2-step verification and an app password for the mailbox.

If the Google Workspace mailbox isn't set up with an app password, the Microsoft 365 migration service is unable to access it during the migration and displays an error.

## Resolution

To resolve this issue, set up the app password for the Google Workspace mailbox.

1. Sign in to the Google Workspace mailbox.
2. Select the mailbox account (profile), and then select **Manage your Google Account**.

    :::image type="content" source="media/google-workspace-mailbox-migration-fail/google-profile.png" alt-text="Screenshot of the account page with the Manage your Google Account button.":::

3. Select the **Security** tab.

    :::image type="content" source="media/google-workspace-mailbox-migration-fail/google-account.png" alt-text="Screenshot of the Google Account page. The Security menu is selected.":::

4. Under **Signing in to Google**, select **App passwords**.

    :::image type="content" source="media/google-workspace-mailbox-migration-fail/app-password.png" alt-text="Screenshot of the Signing into Google page. The App passwords option is highlighted.":::

5. Enter the password to sign in to your Google Workspace account.

6. In the **Select app** drop-down list, select **Other *(Custom name)***.

    :::image type="content" source="media/google-workspace-mailbox-migration-fail/select-app.png" alt-text="Screenshot of the App passwords page. The Other (custom name) option is highlighted in the Select app drop-down list.":::

7. Enter a name, such as *Migration*, and then select **GENERATE**.
8. Make a note of the generated app password and select **DONE**.

    :::image type="content" source="media/google-workspace-mailbox-migration-fail/generate-password.png" alt-text="Screenshot of the Generated app password page with the password.":::

9. In the CSV file for the migration, add the generated app password in the **Password** column.

    :::image type="content" source="media/google-workspace-mailbox-migration-fail/migration-csv.png" alt-text="Screenshot of the migration CSV file. The Password column has no app password.":::

10. Launch the migration wizard in the Exchange admin center.
11. Locate the failed migration batch, select the affected mailbox, and then select **Resume migration**.

    :::image type="content" source="media/google-workspace-mailbox-migration-fail/resume-migration.png" alt-text="Screenshot of the migration batches page. The Resume migration button is highlighted.":::

The migration should complete successfully.

:::image type="content" source="media/google-workspace-mailbox-migration-fail/migration-synced.png" alt-text="Screenshot of a successful migration example that shows the status Synced":::

[!INCLUDE [Third-party information disclaimer](../../../includes/third-party-information-disclaimer.md)]