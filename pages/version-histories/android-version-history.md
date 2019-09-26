### v4.1.0 Changes

**( 26 Sep 2019 )**

- Added support for Cross-Platform ID (CPID) & Last attributed touch data (LATD).

### v4.0.1

**( 18 Sept 2019 )**

- Added new `customer_event_alias` setter method; removed standard event type: customer_event_alias
- Added IMEI collection code option

### v4.0.0

**( 09 Aug 2019 )**

- Switched to using Android X from the Android Support Library
- Added new standard event type: customer_event_alias
- Implemented support for pre-install analytics
- Added the option to set a custom base URL

### v3.2.0

**(2019-May-06)**

- Allow short link creation while privacy is enabled

### v3.1.2

**(2019-April-24)**

- Hardware ID is now included in every request
- Cleaned up compiler warnings, and updated tools to the latest versions

### v3.1.1

**(2019-March-27)**

- Added support for push notifications while the application is in the foreground

### v3.1.0

**(2019-March-22)**

- Ensure that Google Aid is present in all requests
- Refactored how Debug works, including making sure all Debug messages can be turned off if not in debug mode.
- Added new standard events for parity with Tune
- Fixed a synchronization issue around the event queue saving preferences while in a synchronized block.

### v3.0.4

**(2019-January-11)**

- Fixed a TLS1.2 issue with HttpsURLConnection on API Level 16~19 devices
- Added SDK version tag to the Android SDK to aid Google Scanning APIs
- The SDK now supports deep linking with enableForcedSession() for apps which choose to finish the Launcher Activity within onStart() method
