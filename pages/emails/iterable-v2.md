## Overview

![Iterable](/_assets/img/pages/email/iterable/iterable.png)

This guide will walk you through how to setup your email campaigns with **[Iterable](https://iterable.com/){:target="\_blank"}** using Branch Universal Email to automatically convert your email links into **multi-platform deep links**

{! ingredients/email/overview-steps.md !}

## Setup

{! ingredients/email/prerequisites.md !}

## Configure your ESP

### Setup a custom click tracking domain

1. Add and verify a custom click tracking domain in the **[Mail Domains]** page of your Iterable account:

    ![image](/_assets/img/pages/email/iterable/create-domain.png)

For more information on how to set up your domain, please visit Iterable's [documentation](https://support.iterable.com/hc/en-us/articles/115002651226-Setting-Up-Mail-Domains#trackingdomains){:target="\_blank"}.

!!! tip "Adding a custom click-tracking domain"
    If you need help with setting up a custom click-tracking domain - please ask your account manager or request support at Iterable.

{! ingredients/email/cname.md !}

## Activate integration

### Choose your email service provider

Navigate to the [Universal Email](https://dashboard.branch.io/email){:target="\_blank"} section of the Branch dashboard. Select **Iterable** and click **Enable**.

{! ingredients/email/link-setup.md !}

### Tell us your click tracking domain

You can retrieve your click tracking domain from the **[Mail Domains]** page of your Iterable account.
If you have not added a custom click tracking domain yet, follow the instructions [here](#setup-a-custom-click-tracking-domain).

![image](/_assets/img/pages/email/iterable/setup-config.png)

{! ingredients/email/technical-setup.md !}

{! ingredients/email/validate-test.md !}

{! ingredients/email/usage-auto.md !}

## Configure your mobile app

{! ingredients/email/technical-setup-app.md !}

{! ingredients/email/associated-domains.md !}

### Configure Iterable account to support iOS Universal Links

1. Determine which links you want to redirect to your iOS application.

2. Once you have determined which URLs to link to, create an Apple-App-Site-Association (AASA) file that contains the redirect rules to the URLs you have identified. This file is a JSON object that determines which links to rewrite into Universal Links. Here's a sample that you can use.
```
{
    "applinks": {
        "apps": [],
        "details": [
            {
                "appID": "appID.bundleID",
                "paths": [
                    "/a/*"
                ]
            },
            {
                "appID": "iterable",
                "paths": [
                    "PATHS TO BE REDIRECTED GO HERE"
                ]
            }
        ]
    }
}
```

3. Iterable will use your AASA file to determine which links in your messages to rewrite into iOS Universal Links.

!!! info "Important Note"
	After the links have been rewritten by Iterable, they will appear in this format:

	- Normal track and redirect URLs: mydomain.com/u/samplepath

	- iOS Universal Links: mydomain.com/a/samplepath

4. Email your AASA file to [Iterable Support](mailto:support@iterable.com).

5. After Iterable processes the file, you can view it on the bottom of the project settings screen (**Settings > Project Settings**).

![image](/_assets/img/pages/email/iterable/iterable-aasa.png)

For more information, please see Iterable's documentation on [Setting up iOS Universal Links](https://support.iterable.com/hc/en-us/articles/115000440206-Setting-up-iOS-Universal-Links#what-should-an-apple-app-site-association-file-look-like-how-does-all-this-work).

## Support

{! ingredients/email/support.md !}
