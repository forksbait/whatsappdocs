## Overview

We take our customers’ privacy very seriously and provide mechanisms for disabling certain data collection features, which are identified below. You can learn more about the types of data that we need to collect through our services here: https://branch.io/policies/#privacy.

We collect limited device information to power our deep linking technology and to provide attribution and analytics services, but we understand that some users would like to opt out of this data processing; and, in other cases, the law (or Branch policies) do not permit that certain types of personal data for certain end users be provided to Branch (for example, data relating to children under the age of 13). For that reason, we make available to our customers the SDK Privacy Controls feature.

Through the  Branch SDK Privacy Controls, a Branch app or website customer can request that Branch cease certain personal data processing for a particular end user . When the SDK Privacy Controls are enabled for a particular end-user, it will still be possible for that user to generate and share Branch links. Basic deep linking will also continue to work. However, since all further activities must occur without passing any identifiable user information on to Branch, these users will no longer benefit from the seamless customer journeys Branch helps you build with cross-platform data.

!!! info "End-User Opt Out"
	If you are an end user looking to opt out of the Branch Services, please visit [Branch’s Opt-Out](https://branch.app.link/optout) page for available methods.

## Enabling / Disabling SDK Privacy Controls

If you would like to enable the SDK Privacy Controls for a particular user (for example, pursuant to a data subject request, or to comply with certain privacy laws), utilize this field to prevent Branch from sending network requests.

By default, tracking is enabled (opt-in).

### Android SDK

```
Branch.getInstance().disableTracking(true);
```
### iOS SDK

```
Branch.setTrackingDisabled(true)
```
### Web SDK

**NOTE**: This state is persistent, meaning that it’s saved for the user across browser sessions for the web site.

```
branch.init( 'BRANCH_KEY',
    {
        ‘tracking_disabled’ : true
    }
);
```
