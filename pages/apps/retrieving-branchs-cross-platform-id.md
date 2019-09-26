## Overview

Branch includes SDK methods to allow retrieval of our Cross Platform ID (CPID) from the client. This results in an asynchronous call being made to Branch’s servers, with CPID data returned when possible.

!!! warning "Paid Feature"
	The use of the CPID SDK querying is a paid feature. Without CPID SDK querying, you can still export the CPID fields in [Daily Exports via the Branch dashboard or API](https://docs.branch.io/exports/daily-exports/).

By using the CPID SDK querying, the following fields will be returned to the client:

- **user_data_cross_platform_id**: string, Branch’s internal Persona ID hashed by app_id
- **user_data_past_cross_platform_ids**: array of strings, which are past Cross-Platform IDs
- **user_data_prob_cross_platform_ids**: array of dicts. Each dict represents a probabilistically linked Cross-Platform ID, along with a score/probability representing how confident Branch is that this ID is associated with the main Cross-Platform ID for this event.

## Android

```java
Branch.getInstance().getCrossPlatformIds(new BranchCrossPlatformIdListener() {

	@Override
	public void onDataFetched(BranchCPID branchCPID, BranchError error) {
    	branchCPID.getCrossPlatformID();
    	branchCPID.getPastCrossPlatformIds();
    	branchCPID.getDeveloperIdentity();
    	branchCPID.getProbabilisticCrossPlatformIds();
	}
});
```

## iOS

```objective-c
[[Branch getInstance] crossPlatformIdDataWithCompletion:^(BranchCrossPlatformID *cpid) {
   // NSString *
   cpid.crossPlatformID;
   // NSArray<NSString *> *
   cpid.pastCrossPlatformIDs;
   // NSArray<BranchProbabilisticCrossPlatformID *> *
   cpid.probabiliticCrossPlatformIDs;

   for (BranchProbabilisticCrossPlatformID *probID in cpid.probabiliticCrossPlatformIDs) {
       // NSString *
       probID.crossPlatformID;
       // NSNumber *
       probID.score;
   }
}];
```

## Web

```html
branch.crossPlatformIds(
      callback (err, data)
);
/*
`data` will be of the form:
{
      "cross_platform_id":"",
      "past_cross_platform_ids":[],
      "prob_cross_platform_ids":[],
      "developer_identity":""
}
*/
```
