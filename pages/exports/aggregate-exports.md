## Overview

!!! info "For ex-TUNE Clients Only"
	This feature is currently only available for ex-TUNE clients and replicates the TUNE endpoints available via `https://api.mobileapptracking.com/v2/advertiser/stats/actuals/export`.

The Branch Aggregate Exports find and queue aggregate data that match your search criteria for export. Unlike the Custom Exports which contains individual logs for each attribution related to your mobile app, the Aggregate Exports include customizable visualizations of your data of interest.

Aggregate exports endpoints are limited to a maximum of 5k rows on the synchronous endpoint / 10k rows on the asynchronous endpoint and can query up to 180 days prior to the date of export. If more records are required, please make multiple requests with smaller time intervals to pull the necessary data in "batches".

## Authentication

Calls to the Aggregate Export API require an _api_key_ query string parameter to be passed with each request. API Keys are generated on a per-user basis and are permanent.

Learn how to [retrieve your API key (a.k.a. `Access Token`)](/dashboard/organization-view/#managing-your-user-profile)

!!! warning "Organization Level Access Required"
	In order to retrieve or reset your API Key/Access Token, you must have access to the Organization level of the account.  This functionality is not present at the app level.

##Rate Limits

Rate limits depend on the endpoint you are making a request to.

For creating exports, the rate limit is 2 requests per second and 10 requests per minute.

For checking the status of an export, the rate limit is 50 requests per minute and 1000 per hour.

## Export Access

In order to access Aggregate Exports, a user will need to have both **Aggregate Data** and **Export** access.

![image](/_assets/img/pages/dashboard/access-levels/aggregate-access.png)

For more details on how to give a user the required access, please follow [Granting a User Export Access](/dashboard/export-access/#granting-a-user-export-access).

### Third Party Access

Any user with access to an account’s API keys will be able to access Branch’s Custom Export API (and thus unfiltered, log-level data). As a result, we would recommend against providing third parties with the permissions required to view API keys during the invitation process.


### Providing Agencies/Partners API Access

If you work with an agency that runs your advertising campaigns and want to give them access to export the subsequent data, you can provide them with access to the Custom Export API.

To provide an agency team member with access to the Custom Export API:

1. In the left-hand navigation, under **Setup & Testing**, click on **Account Settings**.
2. On the **Account Settings** page, click on the **Agencies** tab.
3. Expand the agency in question, find the agency team member you want to give access to, hover on the button in the **Actions** column and click **Edit**.
4. In the **Edit Agency Team Member** modal:
    1. Under **Access Level**, check the **Export** box.
    2. Under **Permissions**, check the **Aggregate Data** box.
5. Optional: add data filters
    1. Under **Data Filters**, toggle any necessary data filters on/blue. Exported data will be filtered accordingly.
6. Click **Save**.

![image](/_assets/img/pages/dashboard/access-levels/agency-aggregate-export.png)

!!! warning "Agency-Tagged Data"
	If you do not enable the Only Show Agency-Tagged Data data filter, the Agency Team Member will be able to export aggregate data associated with all of your campaigns, regardless if they are associated with them or not.


## Available Topics to Export

The following log topics are available via the Aggregate Export API:

*   **Clicks**
*   **Events**
*   **Impressions**
*   **Installs**
*   **Opens**
*   **Revenue USD**

!!! info "Info"
	Branch does not support exports of the infrequently-used update and postbacks TUNE topics.


## Available Fields

| TUNE Field                    |TUNE Human Readable           |
|-------------------------------|------------------------------|
| ad_network_id                 | Ad Network ID                |
| ad_network.name               | Ad Network Name              |
| advertiser_id                 | Advertiser ID                |
| advertiser.name               | Advertiser Name              |
| advertiser_sub_ad.name        | My Ad Name                   |
| advertiser_sub_ad.ref         | My Ad Ref                    |
| advertiser_sub_adgroup.name   | My AdGroup Name              |
| advertiser_sub_adgroup.ref    | My AdGroup Ref               |
| advertiser_sub_campaign.name  | My Campaign Name             |
| advertiser_sub_campaign.ref   | My Campaign Ref              |
| advertiser_sub_keyword.name   | My Keyword Name              |
| advertiser_sub_keyword.ref    | My Keyword Ref               |
| advertiser_sub_placement.name | My Placement Name            |
| advertiser_sub_placement.ref  | My Placement Ref             |
| advertiser_sub_publisher.name | My Publisher Name            |
| advertiser_sub_publisher.ref  | My Publisher Ref             |
| advertiser_sub_site.name      | My Site Name                 |
| advertiser_sub_site.ref       | My Site Ref                  |
| country.code                  | Country Code                 |
| device_type                   | Device Type                  |
| publisher_sub_ad.name         | Publisher Sub Ad Name        |
| publisher_sub_ad.ref          | Publisher Sub Ad Ref         |
| publisher_sub_adgroup.name    | Publisher Sub AdGroup Name   |
| publisher_sub_adgroup.ref     | Publisher Sub AdGroup Ref    |
| publisher_sub_campaign.name   | Publisher Sub Campaign Name  |
| publisher_sub_campaign.ref    | Publisher Sub Campaign Ref   |
| publisher_sub_keyword.name    | Publisher Sub Keyword Name   |
| publisher_sub_placement.name  | Publisher Sub Placement Name |
| publisher_sub_publisher.name  | Publisher Sub Publisher Name |
| publisher_sub_site.name       | Publisher Sub Site Name      |
| site_id                       | Site ID                      |
| timestamp                     | Timestamp                    |
| wurfl_device_os               | Device OS                    |
| wurfl_model_name              | Model Name                   |


!!! warning "Discontinued Fields"
	Some fields have very limited value to our customers and as such have been discontinued. Discontinued fields will not be available via the Custom Export API. Please work with your CSM or our Support team if you have questions or concerns.

### Including Fields from Related Data Objects

Related objects no longer use periods ( . ) to access the properties on the object. Rather, field names use underscores ( _ ) only.

For example, `site_event.id` will now be exported as `site_event_id`.

## Building the Export Request

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
   <td>filter
   </td>
   <td>Filter
   </td>
   <td>Filter by fields and boolean operators against fields of the Actuals endpoint; must be URI encoded and JSON parsed. Example: <code>&filter=%5B%22and%22%2C%5B%22eq%22%2C%22mat_id%22%2C%223bc15517-92d5-4b7f-9837-e9a30d6fb9b8%22%5D%2C%5B%22eq%22%2C%22site_event_id%22%2C1844998705%5D%5D</code>
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
   <td>sort
   </td>
   <td>Sort
   </td>
   <td>Fields followed by the direction (asc or desc). Results can be sorted with multiple fields and directions.</a>
<p>
Optional parameter.
   </td>
  </tr>
	<tr>
   <td>group
   </td>
   <td>Array
   </td>
   <td>Group items returned by the field selected.</a>
<p>
Optional parameter.
   </td>
  </tr>
	<tr>
   <td>timestamp
   </td>
   <td>String
   </td>
   <td>Set to breakdown stats by timestamp. Choices include: hour, datehour, date, week, month.</a>
<p>
Optional parameter.
   </td>
  </tr>
  <tr>
   <td>format
   </td>
   <td><em>Nullable String</em>
   </td>
   <td>Format of the response; can be either JSON or CSV. If not selected, defaults to CSV.
   </td>
  </tr>
	<tr>
   <td>response_timezone
   </td>
   <td><em>Timezone</em>
   </td>
   <td>Timezone in which result dates are conveyed; defaults to the timezone set in your account.
   </td>
  </tr>
</table>

#### Sample Export Request


```
https://api.mobileapptracking.com/v2/advertiser/stats/actuals/export.json?api_key=4c5b6461026cb0caff3c66bef881b4af&start_date=2018-08-01+00%3A00%3A00&end_date=2018-08-18+00%3A00%3A00&fields[]=opens&fields[]=installs&fields[]=events&fields[]=publisher_sub_adgroup_id&fields[]=publisher_sub_campaign_id&timestamp=date&format=json
```

#### Sample Export Response

```
{
  "status_code": 200,
  "response_size": "334",
  "throttle": {
    "decision": "Permit",
    "decision_authority": "Endpoint",
    "decision_state": "Always Permit",
    "object_key": "/advertiser/stats/actuals/export",
    "virtual_record": false,
    "next_reset": "N/A",
    "count_remaining": 0,
    "limit": 0,
    "interval": 0
  },
  "data": {
    "job_id": "5a494d8b-e5f9-4561-b71d-5c5ee4ed087d"
  }
}
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


#### Sample Download Export Request

```
https://api.mobileapptracking.com/v2/export/download.json?api_key=REMOVED&job_id=5a494d8b-e5f9-4561-b71d-5c5ee4ed087d
```


#### Sample Download Export Response

```
{"status_code":200,"response_size":"437","data":{"status":"complete","percent_complete":100,"data":{"format":"json","url":"https:\\s3.amazonaws.com\hasdevfiles\9da89700-ee8e-42f1-932f-7b9459a614dd.json?response-content-disposition=attachment%3B%20filename%3D%229da89700-ee8e-42f1-932f-7b9459a614dd.json%22&AWSAccessKeyId=AKIAIHT2RGXNQAIUT7ZA&Expires=1547654522&Signature=mfXJ7fGZeZZ%2FYPnEHssGopvdpxk%3D"},"report_schedule_id":null}}
```
