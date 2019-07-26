## Overview

!!! info "For ex-TUNE Clients Only"
	This feature is currently only available for ex-TUNE clients and replicates the TUNE endpoints available via `https://api.mobileapptracking.com/v3/logs/advertisers/exports/`.

The Branch Custom Exports find and queue log records that match your search criteria for export. You can do so either via the **Custom Exports** section in your Branch dashboard OR via API.

Custom exports endpoints are limited to a maximum of 2 million records each and can query up to 120 days prior to the date of export. If more records are required, please make multiple requests with smaller time intervals to pull the necessary data in "batches".

## Authentication

Calls to the Custom Export API require an _api_key_ query string parameter to be passed with each request. API Keys are generated on a per-user basis and are permanent.

##Rate Limits

Rate limits depend on the endpoint you are making a request to.

For creating exports, the rate limit is 10 requests per minute and 25 requests per hour.

For checking the status of an export, the rate limit is 50 requests per minute and 1000 per hour.

## Third Party Access

Any user with access to an account’s API keys will be able to access Branch’s Custom Export API (and thus unfiltered, log-level data). As a result, we would recommend against providing third parties with the permissions required to view API keys during the invitation process.


### Providing Agencies API Access

If you work with an agency that runs your advertising campaigns and want to give them access to export the subsequent data, you can provide them with access to the Custom Export API.

To provide an agency team member with access to the Custom Export API:

1. In the left-hand navigation, under **Setup & Testing**, click on **Account Settings**.
2. On the **Account Settings** page, click on the **Agencies** tab.
3. Expand the agency in question, find the agency team member you want to give access to, hover on the button in the **Actions** column and click **Edit**.
4. In the **Edit Agency Team Member** modal:
    1. Under **Access Level**, check the **Export** box.
    2. Under **Permissions**, check the **Sensitive Data** box.
5. Optional: add data filters
    1. Under **Data Filters**, toggle any necessary data filters on/blue. Exported data will be filtered accordingly.
6. Click **Save**.

![image](/_assets/img/pages/exports/agency-export-access.png)

!!! warning "Agency-Tagged Data"
	If you do not enable the Only Show Agency-Tagged Data data filter, the Agency Team Member will be able to export sensitive data associated with all of your campaigns, regardless if they are associated with them or not.


## Available Topics to Export

The following log topics are available via the Custom Export API:

*   **Clicks**
*   **Event Items**
*   **Events**
*   **Impressions**
*   **Installs**
*   **Opens**

!!! info ""
Branch does not support exports of the infrequently-used update and postbacks TUNE topics.


## Available Fields


<table>
  <tr>
   <td><strong>TUNE field</strong>
   </td>
   <td><strong>TUNE human readable</strong>
   </td>
  </tr>
  <tr>
   <td>ad_network_id
   </td>
   <td>Ad Network ID
   </td>
  </tr>
  <tr>
   <td>ad_network_name
   </td>
   <td>Ad Network Name
   </td>
  </tr>
  <tr>
   <td>advertiser_id
   </td>
   <td>Advertiser ID
   </td>
  </tr>
  <tr>
   <td>advertiser_name
   </td>
   <td>Advertiser Name
   </td>
  </tr>
  <tr>
   <td>advertiser_opt_out
   </td>
   <td>Advertiser Opt Out
   </td>
  </tr>
  <tr>
   <td>advertiser_ref_id
   </td>
   <td>Advertiser Ref ID
   </td>
  </tr>
  <tr>
   <td>advertiser_sub_ad_name
   </td>
   <td>My Ad Name
   </td>
  </tr>
  <tr>
   <td>advertiser_sub_ad_ref
   </td>
   <td>My Ad Ref
   </td>
  </tr>
  <tr>
   <td>advertiser_sub_adgroup_name
   </td>
   <td>My Adgroup Name
   </td>
  </tr>
  <tr>
   <td>advertiser_sub_adgroup_ref
   </td>
   <td>My Adgroup Ref
   </td>
  </tr>
  <tr>
   <td>advertiser_sub_campaign_name
   </td>
   <td>My Campaign Name
   </td>
  </tr>
  <tr>
   <td>advertiser_sub_campaign_ref
   </td>
   <td>My Campaign Ref
   </td>
  </tr>
  <tr>
   <td>advertiser_sub_keyword_name
   </td>
   <td>My Keyword Name
   </td>
  </tr>
  <tr>
   <td>advertiser_sub_keyword_ref
   </td>
   <td>My Keyword Ref
   </td>
  </tr>
  <tr>
   <td>advertiser_sub_placement_name
   </td>
   <td>My Placement Name
   </td>
  </tr>
  <tr>
   <td>advertiser_sub_placement_ref
   </td>
   <td>My Placement Ref
   </td>
  </tr>
  <tr>
   <td>advertiser_sub_publisher_name
   </td>
   <td>My Publisher Name
   </td>
  </tr>
  <tr>
   <td>advertiser_sub_publisher_ref
   </td>
   <td>My Publisher Ref
   </td>
  </tr>
  <tr>
   <td>advertiser_sub_site_name
   </td>
   <td>My Site Name
   </td>
  </tr>
  <tr>
   <td>advertiser_sub_site_ref
   </td>
   <td>My Site Ref
   </td>
  </tr>
  <tr>
   <td>agency_id
   </td>
   <td>Agency ID
   </td>
  </tr>
  <tr>
   <td>agency_name
   </td>
   <td>Agency Name
   </td>
  </tr>
  <tr>
   <td>app_version
   </td>
   <td>App Version
   </td>
  </tr>
  <tr>
   <td>attribute_sub1
   </td>
   <td>Attribute Sub1
   </td>
  </tr>
  <tr>
   <td>attribute_sub2
   </td>
   <td>Attribute Sub2
   </td>
  </tr>
  <tr>
   <td>attribute_sub3
   </td>
   <td>Attribute Sub3
   </td>
  </tr>
  <tr>
   <td>attribute_sub4
   </td>
   <td>Attribute Sub4
   </td>
  </tr>
  <tr>
   <td>attribute_sub5
   </td>
   <td>Attribute Sub5
   </td>
  </tr>
	<tr>
   <td>branch_app_id
   </td>
   <td>Branch App ID
   </td>
  </tr>
  <tr>
   <td>click_created
   </td>
   <td>Click Created
   </td>
  </tr>
  <tr>
   <td>country_code
   </td>
   <td>Country Code
   </td>
  </tr>
  <tr>
   <td>country_name
   </td>
   <td>Country Name
   </td>
  </tr>
  <tr>
   <td>created
   </td>
   <td>Created
   </td>
  </tr>
  <tr>
   <td>currency_code
   </td>
   <td>Currency Code
   </td>
  </tr>
  <tr>
   <td>device_brand
   </td>
   <td>Device Brand
   </td>
  </tr>
  <tr>
   <td>device_carrier
   </td>
   <td>Device Carrier
   </td>
  </tr>
  <tr>
   <td>device_ip
   </td>
   <td>Device IP
   </td>
  </tr>
  <tr>
   <td>device_model
   </td>
   <td>Device Model
   </td>
  </tr>
  <tr>
   <td>device_type
   </td>
   <td>Device Type
   </td>
  </tr>
  <tr>
   <td>download_date
   </td>
   <td>Download Date
   </td>
  </tr>
  <tr>
   <td>event_type
   </td>
   <td>Event Type
   </td>
  </tr>
  <tr>
   <td>existing_user
   </td>
   <td>Existing User
   </td>
  </tr>
  <tr>
   <td>google_ad_tracking
   </td>
   <td>Google Ad Tracking Enabled
   </td>
  </tr>
  <tr>
   <td>google_aid
   </td>
   <td>Google Advertising ID
   </td>
  </tr>
  <tr>
   <td>id
   </td>
   <td>ID
   </td>
  </tr>
  <tr>
   <td>impression_created
   </td>
   <td>Impression Created
   </td>
  </tr>
  <tr>
   <td>install_created
   </td>
   <td>Install Created
   </td>
  </tr>
  <tr>
   <td>install_date
   </td>
   <td>Install Date
   </td>
  </tr>
  <tr>
   <td>install_publisher_name
   </td>
   <td>Install Publisher Name
   </td>
  </tr>
  <tr>
   <td>ios_ad_tracking
   </td>
   <td>iOS Ad Tracking Enabled
   </td>
  </tr>
  <tr>
   <td>ios_ifa
   </td>
   <td>iOS IDFA
   </td>
  </tr>
  <tr>
   <td>ios_ifv
   </td>
   <td>iOS IDFV
   </td>
  </tr>
  <tr>
   <td>ip
   </td>
   <td>IP
   </td>
  </tr>
  <tr>
   <td>is_view_through
   </td>
   <td>Is View Through
   </td>
  </tr>
  <tr>
   <td>language
   </td>
   <td>Language
   </td>
  </tr>
  <tr>
   <td>latitude
   </td>
   <td>Latitude
   </td>
  </tr>
  <tr>
   <td>longitude
   </td>
   <td>Longitude
   </td>
  </tr>
  <tr>
   <td>mat_id
   </td>
   <td>Mat ID
   </td>
  </tr>
  <tr>
   <td>metro_code
   </td>
   <td>Metro Code
   </td>
  </tr>
  <tr>
   <td>os_id
   </td>
   <td>OS ID
   </td>
  </tr>
  <tr>
   <td>os_jailbroke
   </td>
   <td>Jailbroken
   </td>
  </tr>
  <tr>
   <td>os_version
   </td>
   <td>OS Version
   </td>
  </tr>
  <tr>
   <td>package_name
   </td>
   <td>Package Name
   </td>
  </tr>
  <tr>
   <td>platform_aid
   </td>
   <td>Platform AID
   </td>
  </tr>
  <tr>
   <td>postal_code
   </td>
   <td>Postal Code
   </td>
  </tr>
  <tr>
   <td>publisher_adgroup_id
   </td>
   <td>Publisher Adgroup ID
   </td>
  </tr>
  <tr>
   <td>publisher_click_id
   </td>
   <td>Publisher Click ID
   </td>
  </tr>
  <tr>
   <td>publisher_id
   </td>
   <td>Publisher ID
   </td>
  </tr>
  <tr>
   <td>publisher_name
   </td>
   <td>Publisher Name
   </td>
  </tr>
  <tr>
   <td>publisher_ref_id
   </td>
   <td>Publisher Ref ID
   </td>
  </tr>
  <tr>
   <td>publisher_sub_ad_id
   </td>
   <td>Publisher Sub Ad ID
   </td>
  </tr>
  <tr>
   <td>publisher_sub_ad_name
   </td>
   <td>Publisher Sub Ad Name
   </td>
  </tr>
  <tr>
   <td>publisher_sub_ad_ref
   </td>
   <td>Publisher Sub Ad Ref
   </td>
  </tr>
  <tr>
   <td>publisher_sub_adgroup_name
   </td>
   <td>Publisher Sub Adgroup Name
   </td>
  </tr>
  <tr>
   <td>publisher_sub_adgroup_ref
   </td>
   <td>Publisher Sub Adgroup Ref
   </td>
  </tr>
  <tr>
   <td>publisher_sub_campaign_id
   </td>
   <td>Publisher Sub Campaign ID
   </td>
  </tr>
  <tr>
   <td>publisher_sub_campaign_name
   </td>
   <td>Publisher Sub Campaign Name
   </td>
  </tr>
  <tr>
   <td>publisher_sub_campaign_ref
   </td>
   <td>Publisher Sub Campaign Ref
   </td>
  </tr>
	<tr>
   <td>publisher_sub_channel
   </td>
   <td>Publisher Sub Channel
   </td>
  </tr>
	<tr>
   <td>publisher_sub_feature
   </td>
   <td>Publisher Sub Feature
   </td>
  </tr>
  <tr>
   <td>publisher_sub_keyword_id
   </td>
   <td>Publisher Sub Keyword ID
   </td>
  </tr>
  <tr>
   <td>publisher_sub_keyword_name
   </td>
   <td>Publisher Sub Keyword Name
   </td>
  </tr>
  <tr>
   <td>publisher_sub_keyword_ref
   </td>
   <td>Publisher Sub Keyword Ref
   </td>
  </tr>
  <tr>
   <td>publisher_sub_placement_id
   </td>
   <td>Publisher Sub Placement ID
   </td>
  </tr>
  <tr>
   <td>publisher_sub_placement_name
   </td>
   <td>Publisher Sub Placement Name
   </td>
  </tr>
  <tr>
   <td>publisher_sub_placement_ref
   </td>
   <td>Publisher Sub Placement Ref
   </td>
  </tr>
  <tr>
   <td>publisher_sub_publisher_id
   </td>
   <td>Publisher Sub Publisher ID
   </td>
  </tr>
  <tr>
   <td>publisher_sub_publisher_name
   </td>
   <td>Publisher Sub Publisher Name
   </td>
  </tr>
  <tr>
   <td>publisher_sub_publisher_ref
   </td>
   <td>Publisher Sub Publisher Ref
   </td>
  </tr>
  <tr>
   <td>publisher_sub_site_name
   </td>
   <td>Publisher Sub Site Name
   </td>
  </tr>
  <tr>
   <td>publisher_sub1
   </td>
   <td>Publisher Sub1
   </td>
  </tr>
  <tr>
   <td>publisher_sub2
   </td>
   <td>Publisher Sub2
   </td>
  </tr>
  <tr>
   <td>publisher_sub3
   </td>
   <td>Publisher Sub3
   </td>
  </tr>
  <tr>
   <td>publisher_sub4
   </td>
   <td>Publisher Sub4
   </td>
  </tr>
  <tr>
   <td>publisher_sub5
   </td>
   <td>Publisher Sub5
   </td>
  </tr>
	<tr>
	 <td>publisher_sub_stage
	 </td>
	 <td>Publisher Sub Stage
	 </td>
	</tr>
	<tr>
   <td>publisher_sub_tags
   </td>
   <td>Publisher Sub Tags
   </td>
  </tr>
  <tr>
   <td>region_name
   </td>
   <td>Region Name
   </td>
  </tr>
  <tr>
   <td>revenue
   </td>
   <td>Revenue
   </td>
  </tr>
  <tr>
   <td>revenue_usd
   </td>
   <td>Revenue USD
   </td>
  </tr>
  <tr>
   <td>sdk
   </td>
   <td>SDK
   </td>
  </tr>
  <tr>
   <td>sdk_version
   </td>
   <td>SDK Version
   </td>
  </tr>
  <tr>
   <td>search_string
   </td>
   <td>Search String
   </td>
  </tr>
  <tr>
   <td>session_datetime
   </td>
   <td>Session Datetime
   </td>
  </tr>
  <tr>
   <td>site_event_id
   </td>
   <td>Site Event ID
   </td>
  </tr>
  <tr>
   <td>site_event_name
   </td>
   <td>Site Event Name
   </td>
  </tr>
  <tr>
   <td>site_event_type
   </td>
   <td>Site Event Type
   </td>
  </tr>
  <tr>
   <td>site_id
   </td>
   <td>Site ID
   </td>
  </tr>
  <tr>
   <td>site_name
   </td>
   <td>Site Name
   </td>
  </tr>
  <tr>
   <td>stat_click_id
   </td>
   <td>Click ID
   </td>
  </tr>
  <tr>
   <td>stat_impression_id
   </td>
   <td>Impression ID
   </td>
  </tr>
  <tr>
   <td>transaction_id
   </td>
   <td>Transaction ID
   </td>
  </tr>
  <tr>
   <td>user_agent
   </td>
   <td>User Agent
   </td>
  </tr>
  <tr>
   <td>user_id
   </td>
   <td>User ID
   </td>
  </tr>
  <tr>
   <td>windows_aid
   </td>
   <td>Windows Advertising ID
   </td>
  </tr>
  <tr>
   <td>wurfl_brand_name
   </td>
   <td>Brand Name
   </td>
  </tr>
  <tr>
   <td>wurfl_device_os
   </td>
   <td>Device OS
   </td>
  </tr>
  <tr>
   <td>wurfl_device_os_version
   </td>
   <td>Device OS Version
   </td>
  </tr>
  <tr>
   <td>wurfl_model_name
   </td>
   <td>Model Name
   </td>
  </tr>
  <tr>
   <td>branch_app_id
   </td>
   <td>Branch App ID
   </td>
  </tr>
</table>

!!! warning "Discontinued Fields"
	Some fields have very limited value to our customers and as such have been discontinued. Discontinued fields will not be available via the Custom Export API. Please work with your CSM or our Support team if you have questions or concerns.


### Field Value Changes

When exporting the following fields, you will notice a difference between the value TUNE provides vs the value Branch provides.

*   Country Name
    *   TUNE: Korea - South
    *   Branch: Republic of Korea
*   Region Name
    *   TUNE: seoul teugbyeoisi
    *   Branch: Seoul
*   City Code
    *   TUNE: 2261 (Seoul)
    *   Branch: 1835848 (Seoul)
*   Language
    *   TUNE: ko, ko-KR, en-KR
    *   Branch: KO


### Including Fields from Related Data Objects

Related objects no longer use periods ( . ) to access the properties on the object. Rather, field names use underscores ( _ ) only.

For example, `site_event.id` will now be exported as `site_event_id`.

## Accessing via Branch Dashboard

!!! warning "BETA - TUNE Clients Only"
	This feature is currently in BETA. If you do not see this feature in your dashboard, please contact your CSM or [Contact Support](mailto:support@branch.io) to request access.  

	This feature is currently only available to TUNE migrated clients, with plans to open this feature to all Branch clients in Q4.

Rather than accessing the Custom Export API directly, you can use the Custom Exports section in your Branch dashboard to request the appropriate data via CSVs.

To request an export:

1. In the left-hand navigation, under the **Setup & Testing** section, click **Data Import & Export**, then click on **Exports**.
2. On the **Custom Exports** page, provide the following:
	- The appropriate **Date Range**.
	- The **Topic** type the export should include.
	- The **Columns** of fields you want included.
	- Any additional **Filters** you want included.
	- The **Download Type** for the export.

![image](/_assets/img/pages/exports/custom-exports.gif)

Upon request, you will receive a confirmation email verifying the details of your request. Once we finish processing your export, you will receive another email that includes as CSV attachment. Please keep in mind larger exports require more processing time.

You can also view any requested export in the **Custom Exports Created** table which includes:

- Date Created
- Topic / Date Range
- Row Count
- Format
- Status

## Accessing via API

### Building the Export Request

Find and queue all records that match search criteria for export; returns a “handle” to be used in the download export request.


<table>
  <tr>
   <td><strong>Parameter Name</strong>
   </td>
   <td><strong>Type</strong>
   </td>
   <td><strong>Description</strong>
   </td>
  </tr>
  <tr>
   <td>advertiser_id
   </td>
   <td>String
   </td>
   <td>Your TUNE Advertiser ID; <strong>REQUIRED</strong>
   </td>
  </tr>
  <tr>
   <td>api_key
   </td>
   <td>String
   </td>
   <td>Your API Key; <strong>REQUIRED</strong>
   </td>
  </tr>
  <tr>
   <td>start_date
   </td>
   <td>Date
   </td>
   <td><a href="https://en.wikipedia.org/wiki/ISO_8601">The beginning datetime for the requested results, provided in ISO-8601 format. </a>; <strong>REQUIRED</strong>
<p>
Dates without offsets (i.e. a timezone) default to the value provided for the timezone parameter. If the timezone parameter is not specified, the dates timezone defaults to UTC. Date must be within the last 120 days. Example: 2016-01-01T00:00:00Z
   </td>
  </tr>
  <tr>
   <td>end_date
   </td>
   <td>Date
   </td>
   <td><a href="https://en.wikipedia.org/wiki/ISO_8601">The end datetime for the requested results, provided in ISO-8601 format. </a>; <strong>REQUIRED</strong>
<p>
Dates without offsets (i.e. a timezone) default to the value provided for the timezone parameter. If the timezone parameter is not specified, the dates timezone defaults to UTC. Example: 2016-01-01T23:59:59Z
   </td>
  </tr>
  <tr>
   <td>timezone
   </td>
   <td>Timezone
   </td>
   <td><a href="https://en.wikipedia.org/wiki/List_of_tz_database_time_zones">Timezone for results. Accepts tz database strings like ‘America/Los_Angeles’. </a>
<p>
Optional parameter; results are returned in UTC if not provided.
   </td>
  </tr>
  <tr>
   <td>filter_cthulhu
   </td>
   <td>Filter
   </td>
   <td>Filter by fields and boolean operators against fields of the LogInstalls model; must be URI encoded and JSON parsed. Example: <code>&filter_cthulhu=%5B%22and%22%2C%5B%22eq%22%2C%22mat_id%22%2C%223bc15517-92d5-4b7f-9837-e9a30d6fb9b8%22%5D%2C%5B%22eq%22%2C%22site_event_id%22%2C1844998705%5D%5D</code>
   </td>
  </tr>
  <tr>
   <td>fields
   </td>
   <td>Comma Separated List
   </td>
   <td>List of comma-separated fields from the LogInstalls model desired in results. Defaults to display all fields; <strong>REQUIRED</strong>
   </td>
  </tr>
  <tr>
   <td>limit
   </td>
   <td>Integer
   </td>
   <td>Limit the number of items returned per request. Maximum allowed value is 2 million. If more than 2 million records are required, please make multiple requests with smaller time intervals to pull the data needed in “batches”; <strong>REQUIRED</strong>
   </td>
  </tr>
  <tr>
   <td>response_format
   </td>
   <td><em>Nullable String</em>
   </td>
   <td>Format of the response; can be either JSON or CSV. If not selected, defaults to CSV.
   </td>
  </tr>
</table>



#### Sample Export Request


```
https://api.mobileapptracking.com/v3/logs/advertisers/ADVERTISER_ID/exports/installs?api_key=REMOVED&start_date=2019-01-14T00:00:00&end_date=2019-01-15T00:00:00&timezone=UTC&fields=site.name,site.id,device_ip&limit=100&response_format=csv
```



#### Sample Export Response


```
{"handle": "0818e641-cd5c-4498-8a17-77152689bb94", "export_job_status_url": "http://api.mobileapptracking.com/v3/logs/advertisers/ADVERTISER_ID/exports/0818e641-cd5c-4498-8a17-77152689bb94?api_key=REMOVED", "branch_url": "http://tlnk.branch.io/v3/logs/advertisers/ADVERTISER_ID/exports/installs?start_date=2019-01-14T00%3A00%3A00%2B00%3A00&end_date=2019-01-15T00%3A00%3A00%2B00%3A00&fields=site.name%2Csite.id%2Cdevice_ip&filter_cthulhu=%5B%22in%22%2C%20%22advertiser_id%22%2C%20ADVERTISER_ID%5D&response_format=csv&timezone=UTC&limit=100&api_key=REMOVED"}
```



### Building the Download Export Request

Finds and exports requested queue (by handle) and provides URL location for download.


<table>
  <tr>
   <td><strong>Parameter Name</strong>
   </td>
   <td><strong>Type</strong>
   </td>
   <td><strong>Description</strong>
   </td>
  </tr>
  <tr>
   <td>advertiser_id
   </td>
   <td>String
   </td>
   <td>Your TUNE Advertiser ID; <strong>REQUIRED</strong>
   </td>
  </tr>
  <tr>
   <td>api_key
   </td>
   <td>String
   </td>
   <td>Your API Key; <strong>REQUIRED</strong>
   </td>
  </tr>
  <tr>
   <td>handle
   </td>
   <td>String
   </td>
   <td>The ID returned by the log export queue. <strong>REQUIRED</strong>
   </td>
  </tr>
</table>


#### Sample Download Export Request` `

```
http://api.mobileapptracking.com/v3/logs/advertisers/ADVERTISER_ID/exports/0818e641-cd5c-4498-8a17-77152689bb94?api_key=REMOVED
```


#### Sample Download Export Response

```
{"report_schedule_id": null, "lines_exported": null, "context": "", "url": "https://branch-exports-web.s3.amazonaws.com/ADVERTISER_ID-installs-2019-01-14-2019-01-15-0818e641-cd5c-4498-8a17-77152689bb94-wxGQxyHo0Djw2ktt.csv?Signature=5XN9MRMftyQ1XafNSTW4STMpT9U%3D&AWSAccessKeyId=AKIAI7A6NRHGMRDK2LIQ&Expires=1548295211", "percent_complete": 100, "status": "complete", "branch_url": "http://tlnk.branch.io/v3/logs/advertisers/ADVERTISER_ID/exports/0818e641-cd5c-4498-8a17-77152689bb94?api_key=REMOVED"}
```
