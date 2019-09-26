## Overview

![Flashtalking](https://cdn.branch.io/branch-assets/ad-partner-manager/adnetwork_logos/flashtalking.png)

This guide will walk you through how to setup your campaigns with **[![Flashtalking](http://www.flashtalking.com/)
](https://www.1plusads.com/)** using Branch Universal Ads and track ad conversions across **every device, platform, and channel**.

{! ingredients/deep-linked-ads/overview-steps.md !}

## Setup

{! ingredients/deep-linked-ads/integrate-branch-sdk.md !}

{! ingredients/deep-linked-ads/conversion-events-tracking.md !}

{! ingredients/deep-linked-ads/enable-partner.md !}

![image](/_assets/img/pages/deep-linked-ads/flashtalking/flashtalking-enable.png)

{! ingredients/deep-linked-ads/add-credentials.md !}

{! ingredients/deep-linked-ads/enable-partner-tip.md !}

![image](/_assets/img/pages/deep-linked-ads/flashtalking/flashtalking-postbacks.png)

### Create an ad link

Once you've enabled an integration it's time to create a tracking link.

1. First, select an ad format. For App Install or App Engagement campaigns you'll want to select the **App Only** format. For Search or Display campaigns where the user should go to web if they don't have the app, then you should select **Cross-Platform Search** or **Cross-Platform Display**. **Product Links** are for shopping or dynamic remarketing campaigns and will take you to create a Deep Linked Product Feed.

    ![image](/_assets/img/pages/deep-linked-ads/branch-universal-ads/create-link.png)

1. At this point you need to name your link. Select something that will make it easy to find if you need it later. Your Ad Format and Ad Partner should be selected already, but feel free to choose one if they aren't. It's important that you select the right Ad Partner for analytics later on. Click **Configure Options** to continue.

    ![image](/_assets/img/pages/deep-linked-ads/branch-universal-ads/create-link-name.png)

1. Add the following required keys to the **Deep Linking** sub tab during link configuration:
		- spotGroupId
		- spotId
		- reportingBucket
		- advertiserId

		![image](/_assets/img/pages/deep-linked-ads/flashtalking/flashtalking-deep-linking.png)

		!!! warning "Deep Linking Keys Required"
			If you do not already possess the values for the above-mentioned 4 keys, please reach out to your Flashtalking CSM.

1. This is also your chance to add analytics tags. Analytics tags are important for later segmentation, so click the **Analytics** sub tab to add a Channel and Campaign value.

    ![image](/_assets/img/pages/deep-linked-ads/branch-universal-ads/create-link-tags.png)

    !!! tip "Set Analytics tags"

        It's easier to slice your data in our analytics platform if you properly assign analytics parameters to your link. _Channels_ generally correspond to ad networks, and _Campaigns_ correspond to marketing initiatives that you're launching. For example: _Channel_: "YouTube", _Campaign_: "Summer 2017 Shoe Discounts."

    !!! info "Links Created by Agency Users"
        When an Agency users saves an ad link/Journey/Quick Link, that ad link/Journey/Quick Link is associated with that Agency via a unique agency_id that is included as a key-value in deep linking setup.

1. Click **Create Link Now**, and you have your tracking link! Take this link and give it to your Ad Partner's Account Manager or paste it into the tracking section of your campaign yourself.

    ![image](/_assets/img/pages/deep-linked-ads/branch-universal-ads/create-link-completed.png)

	!!! tip "Server to server tracking links"
		If you just need a server to server tracking link just add `%24s2s=true` at the end of your link, so we know it's a server to server link.

{! ingredients/deep-linked-ads/view-ad-link-data.md !}

{! ingredients/deep-linked-ads/people-based-attribution.md !}

{! ingredients/deep-linked-ads/view-through-attribution.md !}

{! ingredients/deep-linked-ads/granting-partner-access.md !}

## Advanced

{! ingredients/deep-linked-ads/add-more-postbacks-short.md !}

{! ingredients/deep-linked-ads/all-events-toggle.md !}

{! ingredients/deep-linked-ads/whitelist-ip.md !}

{! ingredients/deep-linked-ads/edit-postbacks.md !}

{! ingredients/deep-linked-ads/tracking-link-params.md !}

{! ingredients/deep-linked-ads/attribution-windows.md !}

{! ingredients/deep-linked-ads/reset-ad-settings.md !}

{! ingredients/deep-linked-ads/support.md !}
