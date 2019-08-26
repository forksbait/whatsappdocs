## Overview

Many mobile devices come pre-installed with apps already installed, which is great for the user experience because users do not need to launch an app store to download and install these pre-loaded apps. But how do you attribute the pre-loaded app install when there is no ad click to use for attributing the install (to the appropriate advertising partner)?

Branch solves this problem by allowing you to set all of the relevant partner/publisher information in the app itself, which we then collect during the install request.

For example, you have agreed with a wireless carrier (such as AT&T) to pre-install your mobile app on their devices. Because AT&T is the advertising partner who promotes your mobile app (by having it pre-installed), AT&T is the party who gets credit for the attribution. Therefore, you can set the AT&T partner info in your app so that the Branch SDK can collect it on first app open. Branch then uses this info to attribute the app install to AT&T.

!!! info "Android Only"
	The following functionality is applicable to Android apps only.

!!! warning "Pre-Install Overrides Attribution"
	If you include pre-install data via the SDK, it will always override any attribution info Branch receives from the Branch link itself.

## SDK Implementation

Branch provides the following two methods to set the relevant information in the app for pre-install attribution and analytics:

- Set the Data in the Pre-loaded APK
- Read the Pre-loaded Data from the Android System properties

!!! warning "Only for the First App Open"
	Make sure you use the setter ONLY for the first app open event, and not subsequent events/requests. If you include the hard-coded attribution parameters for all measure sessions or other requests, then all requests are attributed accordingly (to the same hard-coded partner, such as AT&T).

### Set Data in the Pre-Loaded APK

!!! warning "Pre-loaded Data in the APK"
	If you set the preloaded data in the APK, it will override the system props data.

After initialization, call these setters to set the data in the APK:

```
Branch.setPreinstallCampaign(“My Campaign Name”)
Branch.setPreinstallPartner(“My Partner Name”)
```

If those values are non-null and this is a first time open for the device, the request should look like this:

```
{
  …
  preinstall_campaign: “My Campaign Name”
  preinstall_partner: “My Partner Name”
  …
}
```

!!! info "Multiple Partners Pre-Installing Your App"
	If multiple partners are pre-installing your mobile app, then you can create a partner-specific build of your app for distribution to each publishing partner (where each build includes different partner settings, respective to the particular partner). The partner-specific build is what the partner pre-installs onto the desired devices.

### Read Pre-loaded Data from the Android system properties

1. Create a json file `pre_install_apps.branch` as follows:
	```
	{
	    "apps": {
	        "application.package.name": {
	            "preinstall_partner": "partner_to_attribute",
	            "preinstall_campaign": "campaign_to_attribute"
	        }
	    }
	}
	```
2. Ask the device manufacturer to add the file in the OS level file system.
3. Set the file path in the build.props as below:
	`io.branch.preinstall.apps.path=/pre_install_apps.branch`
4. The SDK checks if the APK has the pre-install data; if it's included, Branch uses the pre-install to override the link click data for attribution.
