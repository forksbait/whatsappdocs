## Overview

![9Apps](/_assets/img/pages/app-stores/9apps-logo.jpg)

This guide will walk you through how to attribute pre-installed users to **[9Apps](https://www.9apps.com/)** using the Branch SDK.

Learn more about [Pre-Install Attribution](/activity-reports-analytics/ads-pre-install-analytics/).

!!! info "Android Only"
	The following functionality is applicable to Android apps only.

!!! info "Pre-Install Overrides Attribution"
	If you include pre-install data via the SDK, it will always override any attribution info Branch receives from the Branch link itself.

### Set Data in the Pre-Loaded APK

!!! info "Pre-loaded Data in the APK"
	If you set the preloaded data in the APK, it will override the system props data.

After initialization, call these setters to set the data in the APK:

```
Branch.setPreinstallCampaign(“My Campaign Name”)
Branch.setPreinstallPartner(“a_9apps_alibaba”)
```

### Read Pre-loaded Data from the Android system properties

1. Create a json file `pre_install_apps.branch` as follows:
	```
	{
			"apps": {
					"application.package.name": {
							"preinstall_partner": "a_9apps_alibaba",
							"preinstall_campaign": "campaign_to_attribute"
					}
			}
	}
	```
2. Ask the device manufacturer to add the file in the OS level file system.
3. Set the file path in the build.props as below:
	`io.branch.preinstall.apps.path=/pre_install_apps.branch`
4. The SDK checks if the APK has the pre-install data; if it's included, Branch uses the pre-install to override the link click data for attribution.
