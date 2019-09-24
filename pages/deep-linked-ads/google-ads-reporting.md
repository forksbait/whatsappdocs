!!! info "<img src="../../../_assets/img/pages/deep-linked-ads/google/google-ads-logo.png" width="50"/> Google Ads Resources"
		- [Overview](/deep-linked-ads/google-ads-overview/)
		- [Enabling the Integration](/deep-linked-ads/google-ads-enable/)
		- **Reporting & Discrepancies (this page)**
		- [Customization & Edge Cases](/deep-linked-ads/google-ads-customization/)

## Enabling and Segmenting View-Through Conversions in Reporting

By default, Google Ads includes View-Through Conversion counts in a separate column in reporting. If you have impression windows enabled in Branch, we can also attribute VTC installs and events (when there is not a matching click from another partner). Those will be grouped into the install and event counts, and can be segmented using the 'last attributed touch type' compare by in Branch reporting. You can manage settings to enable this attribution within the attribution settings tab of the Google AdWords partner management or by reaching out to support@branch.io

!!! warning "Not Yet Supported"
	Viewing click/impression/cost data in your Branch dashboard is not yet supported for App Engagement campaigns.

## Cost Data

{! ingredients/deep-linked-ads/cost-data.md !}

{! ingredients/deep-linked-ads/cost-data-discrepancies.md !}

## Click Reporting

#### Universal App Campaigns (UAC) - Limited Campaign Information
These campaign parameters are not supported by UAC and will not be available in reports:

Google parameter | Branch parameter
--- | ---
keyword | ~keyword_id
placement | ~placement
ad_group_id | ~ad_set_id
creative_id | ~creative_id

{! ingredients/deep-linked-ads/adwords-valuetrack-info.md !}

#### Universal App Campaigns (UAC)
- As links are not accepted into the Google Ads UAC UI, we will only report on clicks in aggregate (via Google's reporting API)
- Individual UAC clicks will not appear in Branch's liveview dashboard, webhooks, or exports
- 'Unique' UAC data cannot be viewed on the ads analytics dashboard (Non-UACs, like regular Search campaigns, will report on clicks in all Branch dashboards)
- Reporting on UAC clicks is done every 3 hours
- Branch only reports on clicks from an Google Ads campaign that led to an install or app engagement

#### My click data is missing or duplicated for my web campaign

**A:** Click data for web campaigns is available with full breakdowns, but there are specific requirements for setting up web campaigns. Please see the [SAN Web Tracking](/deep-linked-ads/san-web-tracking) guide for more information on setting up web campaigns.

## Conversions

#### My campaign is reporting a number of conversions much higher than the number of conversions shown in the conversion table in Google Ads

**A:** When viewing a campaign, it shows the sum of all conversion events that apply to it. To view by conversion, navigate to `Segment` > `Conversions` > `Conversion name`, in order to clearly see the breakdown of your campaign's conversions.

<img src="/_assets/img/pages/deep-linked-ads/google-conversions/conversion-segment.png" alt="Google Ads Conversion Segment" class="center">

#### Post-install events are attributed to Google Ads in the Branch dashboard but are not appearing in Google Ads

**A:** Ensure that, in the [Google Ads dashboard, you have imported all Branch events](/deep-linked-ads/google-ads-overview/#import-events-in-adwords) that you want to see in Google Ads.

#### I'm seeing a discrepancy between conversion counts in Branch and Google Ads

**A:** While we should always expect around a 5% discrepancy due to time zone differences and the like, if you are seeing significant discrepancies, it could be an indication of a broader problem.

The first thing to do is to make sure you have enabled the `Use Ad Partner Attribution Windows` setting for Google Ads. Go to [Link Settings](https://dashboard.branch.io/ads/partner-management/a_google_adwords?tab=attribution_windows), and navigate down to the Attribution Windows section. Here, you should set the attribution window for `click to install`, `click to session start`, and `click to conversion event` to be 30, 90, and 90 days respectively. This aligns with Google's default attribution windows, but if you'd like to make them shorter, feel free.

Another source of discrepancies is the fact that attribution is based upon *click* time in Google Ads, whereas it is based upon *conversion* time in the Branch dashboard. This isn't a discrepancy per se, but will sometimes show different numbers in the two dashboards. This usually does not affect install numbers (because install usually happens same day as click) but will especially have impact on downstream events, where events can sometimes occur and be attributed up to 90 days after click.

Google will send attribution data for almost every app conversion that they count on their end, with the exception of iOS Search traffic within UAC, and they also do not currently confirm standalone (outside of UAC) YouTube TrueView conversions to Branch - this is estimated to be available Q4 2019.

Finally, Google Ads can delay reporting up to 24 hours. It's best to measure campaigns in a trailing manner.

#### My UAC data looks misaligned when I compare by certain filters

**A:** Google _installs_ should have the full range of compare by options in the dashboard. However, _clicks, impressions and cost_ data for UAC are imported via the Google Ads Reporting API, as noted above. The Google Ads Reporting API does not necessarily provide the same breakdowns that Branch can create with raw install events, so there may be cases where the Branch Dashboard cannot compare by the same dimensions for clicks vs installs.
