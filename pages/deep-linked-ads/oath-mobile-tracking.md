## Overview

![Oath](https://cdn.branch.io/branch-assets/ad-partner-manager/386574786681131050/oath-1544044998484.png)

This guide will walk you through how to setup your campaigns with **[Oath](https://gemini.yahoo.com/advertiser/home)** using Branch Universal Ads and track ad conversions across **every device, platform, and channel**.

{! ingredients/deep-linked-ads/overview-steps.md !}

## Campaign Support

| **Campaign Type** | **Attribution supported** |
| - | - |
| Gemini/Native/Search | Yes (using Branch links) |
| DSP | No (reporting only available in Oath) |

Oath Ad Platforms has two main products/channels relevant to mobile advertising and attribution - (Yahoo!) Gemini/Native & Search, and the (formerly Brightroll) DSP.

Branch currently attributes only Gemini inventory using Branch links, and is able to send all event data to Oath which can attribute both Gemini and DSP inventory. 

## Setup

{! ingredients/deep-linked-ads/integrate-branch-sdk.md !}

{! ingredients/deep-linked-ads/conversion-events-tracking.md !}

{! ingredients/deep-linked-ads/enable-partner.md !}

![image](/_assets/img/pages/deep-linked-ads/oath/oath-enable.png)

{! ingredients/deep-linked-ads/enable-partner-tip.md !}

![image](/_assets/img/pages/deep-linked-ads/oath/oath-postbacks.png)

!!! warning "Send All Events"
	By default, postbacks to Oath are enabled to send all events to Oath, not just those events attributed to them. This allows Oath to attribute on Gemini and DSP inventory. Please ensure this setting remains set to `All Events`.

{! ingredients/deep-linked-ads/create-ad-link.md !}

!!! info "Using Links in Gemini"
	During campaign setup, The App Store URL needs to be used in the app URL field. Then, when the ad is created, the tracking URL can be used. You will need to specify "Other" under the MMP, and can then enter the tracking URL.
	If you are still unable to locate a tracking URL field in the UI, you may have to upload them via bulk upload functionality. Please take a look at this documentation:  https://developer.verizonmedia.com/nativeandsearch/advertiser/guide/bulk/ . There are screenshots included and a short video. If you have further issues, please reach out to your VZM contact or support team.

{! ingredients/deep-linked-ads/add-agency-prefix-san-only.md !}

{! ingredients/deep-linked-ads/view-ad-link-data.md !}

!!! tip "Viewing Oath Attributions"
	When viewing attributions in your Oath reporting, you will notice attributions for both the Yahoo Gemini channel as well as their DSP Brightroll.  As Branch links can only be used for the Yahoo Gemini channel, Branch analytics can only show attributions specific to Yahoo Gemini.

{! ingredients/deep-linked-ads/view-through-attribution.md !}

{! ingredients/deep-linked-ads/granting-partner-access.md !}

## Advanced

{! ingredients/deep-linked-ads/add-more-postbacks-short.md !}

{! ingredients/deep-linked-ads/all-events-toggle.md !}

{! ingredients/deep-linked-ads/tracking-link-params.md !}

{! ingredients/deep-linked-ads/attribution-windows.md !}

{! ingredients/deep-linked-ads/reset-ad-settings.md !}

{! ingredients/deep-linked-ads/support.md !}
