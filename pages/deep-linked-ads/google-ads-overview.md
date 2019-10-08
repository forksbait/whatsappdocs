!!! info "<img src="../../../_assets/img/pages/deep-linked-ads/google/google-ads-logo.png" width="50"/> Google Ads Resources"
		- **Overview (this page)**
		- [Enabling the Integration](/deep-linked-ads/google-ads-setup/)
		- [Reporting & Discrepancies](/deep-linked-ads/google-ads-reporting/)
		- [Customization & Edge Cases](/deep-linked-ads/google-ads-customization/)

## Overview

With Branch, you can integrate with **[Google Ads](https://ads.google.com/home/)**, improving conversion rates and letting you measure the impact of your campaigns right on the Branch dashboard.

![image](/_assets/img/pages/deep-linked-ads/google/google-ads-overview.png)

!!! warning "Branch Linking Supported but Not Recommended"
	For non-app campaigns, use you can use Branch links.  However, they are not required and we recommend their usage only in custom edge cases.  Learn more about [Customization & Edge Cases](/deep-linked-ads/google-ads-customization/) for using Branch links.

## Campaign Support

Our integration with Google Ads supports the following:

### App Install Campaigns
- Full attribution for:
	- App Installs
- No 3rd Party Links
- No Deep Linking
- Destinations:
	- App Stores only

!!! info "No Branch Links"
	As all App Install Campaigns direct users to the respective app store, please make sure you complete the following.

	* [x] Branch SDK integrated into your app.
	* [x] Collect the IDFA on iOS, or the AAID on Android. For specifics, refer to the set up guide for [iOS](/apps/ios/#install-branch) and [Android](/apps/android/#install-branch) respectively.
	* [x] Track all necessary events through the SDKs, with instructions [here](#forwarding-events-to-google-ads).
	* [x] Have admin access to your Google Ads account; required for generating Link IDs in Google Ads.

Please follow Google Ads' documentation on how to [set up an App Install Campaign](https://support.google.com/google-ads/answer/6291545?co=ADWORDS.IsAWNCustomer%3Dtrue&oco=0).

For more detailed information, please see [Google Ads' help documentation](https://support.google.com/google-ads/answer/6247380?hl=en).

### App Engagement Campaigns
- Full attribution for:
	- In-app Events
- No 3rd Party Links
- Deep Linking via Universal Links (iOS), App Links (Android), custom URI Scheme
- Destinations:
	- In-app experiences

Please follow Google Ads' documentation on how to [set up an App Engagement Campaign](https://support.google.com/google-ads/answer/9234102).

!!! info "Required for App Engagement Campaigns"
	* [x] Have [assets such as text, video and image](https://support.google.com/google-ads/answer/9234183).
	* [x] Have a universal deep link (iOS), an app link (Android), or custom URI scheme.
	* [x] Use an [audience list](https://support.google.com/google-ads/answer/9234182) of app users.
	* [x] Have [mobile app conversion tracking](https://support.google.com/google-ads/answer/6100665) set up and [a supported third party](https://support.google.com/google-ads/answer/7382633) (Branch) to track conversions.

!!! warning "Dynamic Remarketing Campaigns for Apps"
	App Engagement Campaigns do not include dynamic remarketing campaigns for apps.  If you want to set up dynamic remarketing campaigns for people who have previously engaged with your app, you must create a **Web-based Ad** using the **Display Network**.

For more detailed information, please see [Google Ads' help documentation](https://support.google.com/google-ads/answer/9234180).

### Web-based Ads (non-App Campaigns)

!!! info "Non-App Campaigns"
	The integration is mostly designed to strongly support app install campaigns and app engagement campaigns. However, you can also still run non-app campaigns and Google will confirm when a supported app conversion occurs.

- Includes **Search**, **Display**, **Shopping** and **Video** Campaign types
	- Dynamic Remarketing campaigns for Apps
- Full attribution for:
	- App conversions (opens & in-app events)
		- iOS web app conversion not supported
	- Web (Mobile & Desktop) conversions
- Deep Linking via Branch Links
- Destinations:
	- Web (Mobile & Desktop) Only
		- Requires the [Branch Web SDK](/web/integrate/)
	- Deep Link into App (if installed)
		- Requires [Universal Links](/deep-linking/universal-links/) and/or [App Links](/deep-linking/android-app-links/)
			- If you don't have Universal Links or App links enabled, use [Branch's custom deep linking solution](/deep-linked-ads/google-ads-customization/).

## Data Mapping between Google Ads & Branch

Branch maps the following data fields from Google Ads to Branch.

Google Data | Branch Data | Definition | Possible Values
--- | --- | --- | ---
campaign_id | ~campaign_id | The numeric campaign ID of the campaign that produced the ad event. This value is guaranteed unique. | Google Ads Campaign ID
campaign_name | ~campaign  | The advertiser-defined campaign name of the campaign that produced the ad event. This value is not guaranteed unique. | Google Ads Campaign Name
ad_type | ~ad_format | The type of ad that resulted in the ad event. This value can be used to distinguish between various types of inventory as follows. | ClickToDownload<br/>AppDeepLink<br/>AppDeepLinkContinue<br/> Unknown
network_type | ~channel | This field will identify the Google Ads advertising network the ad event occurred on. | Search<br/>Display<br/>YouTube
network_subtype | ~secondary_publisher | This field will identify the “subtype” of the Google Ads advertising network the ad event occurred on. The possible values vary by primary network type. | Google Search, Search Partners, mGDN, Google AdMob, YouTubeVideos, YouTubeSearch, VideoPartners; `null` when campaign_type is UAC and network_type is Display.
campaign_type | ~tags | This field will identify the type of campaign that produced the ad event. | UAC, UACe, Search, Display, Video, Shopping
ad_group_id | ~ad_set_id | The numeric ID of the ad group that produced with the ad event. Only provided when campaign_type is not UAC. | Google Ads Ad Group ID
creative_id | ~ad_id | The numeric ID of the creative ad unit that produced the ad event. Only provided when campaign_type is not UAC. | Google Ads Creative ID
keyword | ~keyword | The search keyword associated with the ad event. Only provided when network_type is Search and campaign_type is not UAC. | Google Ads Keyword

## Forwarding Events to Google Ads

Once you begin tracking events through the Branch SDK, you can select which events to import in Google Ads. Google Ads has pre-defined events that map to pre-defined Branch events, listed below. Reference this [doc](https://developers.google.com/app-conversion-tracking/api/) for more information.

Regardless of campaign type, Branch will forward in-app events to Google Ads for campaign optimization. In addition, Branch will receive attribution data for rich analysis in the Branch dashboard.

Google Event | Branch Event
--- | ---
first_open | install
session_start | open
in_app_purchase | purchase
view_item_list | view_items
view_item | view_item
view_search_results | search
add_to_cart | add_to_cart
ecommerce_purchase | purchase
custom | any custom event tracked through Branch

In order to track these events, please refer to this document for further [information](/apps/v2event/#v2-event).

## General FAQs

### What is Parallel Tracking?

!!! warning "Since October 30, 2018, parallel tracking is required for all Google Ads accounts."

In the past, Google Ads' non-UAC campaign clicks were tracked through “sequential tracking” (i.e. a client-side redirect). When an ad was clicked, the customer’s browser would go to the tracking URL, and then the tracking URL was responsible for forwarding the browser on to the Final URL.

![image](/_assets/img/pages/deep-linked-ads/google/legacy-sequential-tracking.png)

With the change to “parallel tracking”, Google sends the customer directly to the Final URL, and uses the new Beacon API to "click" the Tracking URL (including following any server side redirects) in the background. The key here is that the Tracking URL (and redirects) are still being visited by the end user's browser, but because this happens “in parallel” (i.e., not visible to the customer), the user experience is better. For browsers without Beacon API support, Google will fall back to legacy sequential tracking.

![image](/_assets/img/pages/deep-linked-ads/google/new-parallel-tracking.png)

#### How Does Parallel Tracking Work?

If you are running a Universal App Install Campaign, parallel tracking does not come into play as this campaign type directs users solely to the respective app store and does not include a third party link.

If you are running a non-UAC Web-based Ad (Display, Search, Shopping, Video), and using a Branch link as either the `Final URL` or `Tracking Template`, parallel tracking ensures your users are directly routed to the final destination while also allowing Branch to properly measure and attribute the resulting actions/conversions.

![image](/_assets/img/pages/deep-linked-ads/google/google-ads-non-uac.png)

#### How Does This Impact Me?

Attribution is unaffected because, although the Branch link is no longer the referring URL to the domain, parallel tracking still allows Branch link clicks to happen. This means the Branch Match ID parameter is still appended to the link that is being "clicked", and Branch can still store (and access) the Match ID in local storage because the web SDK can still load and read query parameters, even in the background.

Furthermore, this is in line with Google & Safari’s expectations of how clicks should be tracked (i.e., using query parameters instead of third-party cookies), and is compliant with current policy.

### Why is my ad being disapproved on Google Ads?

**A:** For Video Campaigns, sometimes your ad may be disapproved if the Branch link does not re-direct to Google Play or App Store when clicked on a desktop. Please ensure that for the Branch link you're using to track installs, Deepviews are disabled and a desktop redirect is set to either the App / Play store.

For Cross Platform campaigns, sometimes your ad may be disapproved if the Branch link does not re-direct to your Final destination URL specified in the ad. Please ensure that your Branch link redirects to your Final URL specified in your ad. To ensure install tracking is functional please ensure that for the Branch link you're using to track installs, Deepviews are disabled and your Branch link's iOS/Android redirects are set to their respective App / Play Store.
