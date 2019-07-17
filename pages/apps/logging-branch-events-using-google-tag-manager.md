## Overview

**Use case**: Log Branch Events using Google Tag Manager (GTM), Firebase and Branch libraries. This is done using GTM custom functions.

**Pre-requisite**: Branch SDK must be in iOS and Android App.

**Warning**: This has not been tested intensively (with different use cases)!

## Setting up Custom Tags on Android

!!! warning "Pre-requisite"
	Please ensure that you have the Branch SDK installed on Android.

1. Import your GTM container
1. Implement a class that extends `com.google.android.gms.tagmanager.CustomTagProvider`. 	
	Please see an example below :
	```
	import android.support.annotation.Keep;
	import java.util.Map;
	import branch
	@Keep
	public class HighScoreProvider implements com.google.android.gms.tagmanager.CustomTagProvider {
	  @Override
	  ...
	}
	```
1. If using [ProGuard](https://developer.android.com/tools/help/proguard.html), make sure that the class names and methods are not obfuscated. Use the Keep annotation to specify this.
1. Within this custom class, use the following function below
	`public abstract void execute (Map<String, Object> parameters)`
1. Within this function, read the parameters passed by GTM within the "execute" function and log a Branch standard /custom event. Please ensure you import the Branch library.
	```
	@Keep
	public class TagProviderImpl implements CustomTagProvider {
	...

		@Keep
		public void execute(Map<String, Object> variables) {
			BranchEvent event = new BranchEvent("View Event");
			for (String key: variables.keySet()) {
				event.addCustomDataProperty(key, variables.get(key).toString());
			}
			event.logEvent(context);
		}
	}
	```

## Setting up custom tags on iOS

!!! warning "Pre-requisite"
	Please ensure that you have the Branch SDK installed on iOS.

1. Import your GTM container
1. Ensure that you have a bridging header included (especially for codebase using both Swift and Objective-C)
	1. Open Xcode.
	1. Click File > New > File.
	1. Under iOS > Source, select Header File.
	1. Click Next.
	1. Enter the header file name `BridgingHeader.h`.
	![image](/_assets/img/pages/apps/gtm/gtm1.png)
	1. Click Create
1. Add Objective-C bridging header on build settings
	1. In Xcode, click your project.
	![image](/_assets/img/pages/apps/gtm/gtm2.png)
	1. Click Build Settings in the editor area.
	1. Select All and Combined and search for bridging.
	1. In the right column of the row containing Objective-C Bridging Header, enter `BridgingHeader.h`.
	![image](/_assets/img/pages/apps/gtm/gtm3.png)
1. Implement a custom class e.g CustomEventTagFunction
	```
	import Foundation
	import GoogleTagManager

	@objc(CustomEventTagFunction)
	final class CustomEventTagFunction : NSObject, TAGCustomFunction {
	 ...
	}
	```
1. Within this custom class, use the following function below:
	`@objc func execute(withParameters parameters: [AnyHashable : Any]!) -> NSObject! { ...}`
1. Within this function, read the parameters passed by GTM within the "execute" function and log a Branch standard or custom event. Please ensure you import the Branch library. This is an example:
	```
	import Foundation
	import GoogleTagManager
	import Branch

	@objc(CustomEventTagFunction)
	final class CustomEventTagFunction : NSObject, TAGCustomFunction {
	    @objc func execute(withParameters parameters: [AnyHashable : Any]!) -> NSObject! {
	        print("********************* parameters: \(String(describing: parameters))")

	        let event_Name = parameters["event_name"] as! String
	        let event = BranchEvent.customEvent(withName: event_Name)

	        parameters.keys.forEach { key in
	            let a = parameters[key] as! String
	            event.customData[key] = a
	            print("*", a)
	        }
	        event.logEvent()
	        return nil
	    }
	}
	```

## Trigger events via Firebase Events

1. Ensure that you have events triggered via GTM.
	Here is an example:
	`dataLayer.push(["event": "branch_event", "screenName": "Home Screen"])`

## Setting up GTM configurations

1. Set up triggers for your event.
	1. Add in filters for when this trigger is fired.
	![image](/_assets/img/pages/apps/gtm/gtm4.png)
1. Add in relevant event variables of what to add in.
	1. Create a new variable
	1. Select ‘Event Parameter’
	1. Work with your Branch Sales engineer or Solutions engineer to determine what variable to create.
	![image](/_assets/img/pages/apps/gtm/gtm5.png)
1. Create a new Tag under Tags section and provide a name.
	1. Click on Tag Configuration and under Tag type select Function Call.
	1. Provide the created classpath under the Class path section
		1. iOS: Look at this section
		1. Android: Look at this section
	1. Expand the “Add Argument” section and provide the key as "event_name" with event name macro. Add in other keys which you need.
1. Click on Triggering section and choose your appropriate trigger on which this Tag should fire.
![image](/_assets/img/pages/apps/gtm/gtm6.png)
1. Please ensure that you update the container on both iOS and Android respectively.
