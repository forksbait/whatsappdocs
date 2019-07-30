## Overview

Branch's Universal Email allows you to automatically convert your email links into multi-platform deep links that take users directly to content in the app on mobile devices, while still maintaining the same web experience for desktop and mobile users without the app.

In conjunction with Universal Email, you can use third party - like [MovableInk](https://movableink.com/) and [Liveclicker](https://www.liveclicker.com/) - services to create personalized visual experiences that are based on relevant data and are unique for each and every one of your customers.

## Required Redirect Parameter

As these highly-personalized experiences require an additional redirect through the third party service, Branch requires an additional parameter appended to the URL you use in your Universal Email template. This parameter ensures Branch deep links your users to the personalized content you've created through the third party service.

For any Universal Email link that originates from a third party service such as MovableInk and Liveclicker, you must append the following parameter:

`$follow_redirect=true`

**Example URL + Redirect Parameter**

```https://cbsn.ws/2KW0dnE?$follow_redirect=true```
