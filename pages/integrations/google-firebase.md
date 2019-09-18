!!! warning "Google Analytics vs. Google Firebase"
	If you are a paying Google Analytics customer, please refer to our [Google Analytics](/integrations/google-analytics/) data integration. Otherwise, please follow the guide below to send Branch data to your free Google Firebase Analytics account.

## Overview

With a push of a button you can send your Branch data to your Google Analytics dashboard, helping you understand the power of Branch as an acquisition pathway. If you're interested in the segment of users coming into your apps through Branch and want to measure their events against your other cohorts, this guide can help.

## Prerequisites

- [Branch SDK](/resources/native-sdks-and-plugins/)
- [Firebase Analytics SDK](https://firebase.google.com/docs/guides)

## Events Sent to Google Firebase

Branch will send *referred* **installs** and **opens**, as well as any **custom events** you track with Branch. Non-referred events, clicks, web session starts, and pageviews will be excluded. Branch also sends over analytics data that is attached to the link, whether it's UTM tags or fields set on the Branch Dashboard (e.g. Campaign, Channel, Feature). This will allow you to analyze which campaigns, channels, etc. are helping you acquire and engage users.

Below is the full list of fields:

| Property Name | Value | Sourced from | Example | Req
| --- | --- | --- | --- | ---
| v | API version | [fixed] | 1 | Y
| tid | Tracking ID | Branch Dashboard | UA-XXXXXX-Y | Y
| ds | Source (mobile SDK) | [fixed] | app | Y
| an | Application Name | [fixed] | BRANCH-APP | Y
| t | Type | [fixed] | event | Y
| ec | Event Category | [fixed] | BranchEvent | Y
| cid | Client ID | (discussed above, includes $google_analytics_client_id) | AEBE52E7-03EE-455A-B3C4-E57283966239 | Y
| uid | User Id | $google_analytics_user_id | User A | N
| cn | Campaign Name | utm_campaign -or- Branch campaign  | "Beaches and breezes" | N
| cs | Campaign Source | utm_source -or- Branch channel | "Twitter" | N
| cm | Campaign Medium | utm_medium -or- Branch feature  | "480banner" | N
| ck | Campaign Keywords | utm_term -or- Branch $keywords | ["Keyword1", "keyword3"] | N
| cc | Campaign Content | utm_content -or- Branch tags | "Some content" | N
| ea | Event Action (Name) | event name | install | Y
| uip | User’s IP Address | collected by Branch SDK | 111.111.111.111 | N
| z | Cache buster | [unix time + random number] | 1461878903666 | N

## Setup

### Android

1. Ensure you've completed the Firebase SDK implementation as documented [here](https://firebase.google.com/docs/analytics/android/start)
2. Ensure you've completed the Branch SDK implementation as documented [here](/apps/android).
3. In the `LauncherActivity#onStart() method` of the Branch Android SDK, update the implementation as below:

```java
	@Override
	 public void onStart() {
		 super.onStart();

		 // Branch init  
		 Branch.getInstance().initSession(new Branch.BranchReferralInitListener() {
			 @Override
			 public void onInitFinished(JSONObject referringParams, BranchError error) {
				 if (error == null) {
					 if (referringParams != null) {
						 try {
							 // check if the session is from a Branch link  
							 if (referringParams.getBoolean("+clicked_branch_link")) {

								 // create FirebaseAnalytics instance  
								 FirebaseAnalytics firebaseAnalytics = FirebaseAnalytics
										 .getInstance(getApplicationContext());
								 Bundle bundle = new Bundle();

								 bundle.putBoolean("clicked_branch_link",
										 referringParams.getBoolean("+clicked_branch_link"));
								 // get the click timestamp  
								 bundle.putString("click_timestamp",
										 referringParams.getString("+click_timestamp"));
								 // get the link OG title  
								 bundle.putString("link_title",
										 referringParams.getString("$og_title"));
								 // get the link OG image  
								 bundle.putString("link_image",
										 referringParams.getString("$og_image_url"));
								 // get the link campaign  
								 bundle.putString("utm_campaign",
										 referringParams.getString("~campaign"));
								 // get the link channel  
								 bundle.putString("utm_medium", channel
										 referringParams.getString("~"));
								 // get the link feature  
								 bundle.putString("utm_source",
										 referringParams.getString("~feature"));

								 // you can use the local shared preference to detect if this is an install session or open session as below  
								 SharedPreferences sharedPreferences = getApplication()
										 .getSharedPreferences("local_sharefpref",
												 Context.MODE_PRIVATE);
								 SharedPreferences.Editor editor = sharedPreferences.edit();
								 boolean isFirstSession = sharedPreferences
										 .getBoolean("is_first_session", true);
								 if (isFirstSession) {
									 editor.putBoolean("is_first_session", false);
									 editor.apply();
								 }

								 // check if the session is install or open  
								 String eventName =
										 isFirstSession ? "branch_install" : "branch_open";

								 // log the event to the firebase  
								 firebaseAnalytics.logEvent(eventName, bundle);
							 }
						 } catch (JSONException ignore) {
						 }
					 }
				 }
			 }
		 }, this.getIntent().getData(), this);
	 }
```

### iOS

1. Ensure you've completed the Firebase SDK implementation as documented [here](https://firebase.google.com/docs/analytics/ios/start)
2. Ensure you've completed the Branch SDK implementation as documented [here](/apps/ios).
3. In the `AppDelegate` of the Branch iOS SDK, update the implementation as below:

```swift
	FirebaseApp.configure()
	Branch.getInstance().initSession(launchOptions: launchOptions) { (params, error) in
	// do stuff with deep link data (nav to page, display content, etc)
	if(error == nil && params != nil){
	  // create and add properties that you want to track in Firebase                
	  var firebase_params = [String: Any]()
	  firebase_params["clicked_branch_link"] =  params?["+clicked_branch_link"] ?? ""
	  // get the click timestamp
	  firebase_params["click_timestamp"] = params?["+click_timestamp"] ?? ""
	  // get the link OG title  
	  firebase_params["link_title"] = params?["$og_title"] ?? ""
	  // get the link OG image  
	  firebase_params["link_image"] =  params?["$og_image_url"] ?? ""
	  // get the link campaign  
	  firebase_params["utm_campaign"] = params?["~campaign"] ?? ""
	  // get the link channel  
	  firebase_params["utm_medium"] = params?["channel"] ?? ""
	  // get the link feature  
	  firebase_params["utm_source"] = params?["~feature"] ?? ""
	  // check if this is an open or and install event
	  if(UserDefaults.standard.object(forKey: "is_first_session") == nil){
	    UserDefaults.standard.set(true, forKey: "is_first_session")
	  }
	                else{
	    UserDefaults.standard.set(false, forKey: "is_first_session")
	  }
	  let event_name = UserDefaults.standard.bool(forKey: "is_first_session") == true ? "branch_install" : "branch_open"
	  // track the event to Firebase
	  Analytics.logEvent(event_name, parameters: firebase_params)
	}
	}
```

## Using Firebase DebugView

To debug the events and their metadata, you can enable the `DebugView` on Firebase to verify the setup. Please refer to Google's official instructions [here](https://firebase.google.com/docs/analytics/debugview).

![image](/_assets/img/pages/integrations/google-analytics/firebase-debugview.png)

## Common Discrepancies Between Firebase & Branch

- When the attribution of the custom events occurs in the following sessions after the click (i.e not the session after the immediate click). For example, Click -> app open -> app close -> app open -> Purchase -> Purchase sent to Firebase.

	The above purchase event on Branch might be attributed based on the attribution window, but on the Firebase this will always be organic as the SDK will not have the attribution data.

	!!! info "Feature in Development"
		Last attributed touch data explicitly within the SDK is currently in development. Once released, this discrepancy should not occur.

- SAN attribution support, for Google UAC (no deep linking) and Facebook App Install (not so reliable deferred deep links), the Firebase installs would miss the attribution data.

	!!! warning "NOTE"
		Please ensure you’ve reviewed your agreements with any ad network (for example Facebook, Snap and Twitter) to ensure your handling of attribution data and use of third party analytics tools is in compliance.

- As per your account settings, it may be the case where the Fingerprinting attribution is disabled. This means that the deep link will return the link data, but no attribution data will be recorded at Branch’s end. If this is the case(ensure to check with your Account Manager or support@branch.io).
