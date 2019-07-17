## Overview

The "Export" level of access applies specifically to the [Sensitive Data](/dashboard/sensitive-data-access/) level of access and allows users to export sensitive data from pages they've been given view access to.

!!! warning ""
	Users with export access to sensitive data, can export **log-level data** via the **Export** section.

## Granting a User Export Access

!!! info ""
 By default, any user with the `Admin` access level includes both access to `Sensitive Data` and `Export Access`.

 To give export access to non-Admin users (both creating new and editing existing):

 1. Using the **Access Level** drop-down, select **Custom**.
 2. Select the **Export** box next to the Access-level setting.
 3. Select the **Sensitive Data - View** setting.
 4. Select the following resource settings as you see fit.
	 - **Link-level Settings** - Settings or features that can impact functionality for single links.
	 - **Channel-level Settings** - Settings or features that can impact functionality across a marketing channel.
	 - **App-level Settings** - Settings or features that can impact functionality app-wide.
	 - **Aggregate Data** - Summary data that contains no granular data.
5. Click **Save**.

![image](/_assets/img/pages/dashboard/access-levels/export-access.png)

## Agency Access to Export Sensitive Data via API

By default, third parties - including Agencies - do not have access to export sensitive (i.e.log-level) data via the [Custom Export API](/exports/custom-export-api/).

However, agencies may be [given access to the Custom Export API](/exports/custom-export-api/#providing-agencies-api-access) by contacting their advertiser or emailing [support@branch.io](mailto:support@branch.io).
