## Overview

A product feed or catalog is essentially an inventory of all your products and contain information like images, prices, descriptions and more. These attributes are used to define each one of your products in a unique way. Your product feed or catalog should reflect your business type, consisting of different attributes that are specific to your products.

Your Branch link ensures your users are taken to the correct product feed or catalog content and when used as part of your dynamic and responsive marketing efforts, they allow you to effectively engage with users who have expressed interest in a wide range of your products across both web and app.  

## Prerequisites for Product Feeds
*   Deep Link Routing set up in your Branch dashboard
*   Universal Links and/or App Links enabled in your iOS or Android app
*   Facebook and/or Google Ads integrations enabled in your Branch Dashboard
*   Branch link per product feed item

### Prerequisites for the Branch Product Feed Script
*   Feeds formatted as a CSV file
*   Github
*   Python 3.5+

## Creating Branch Links

As each product in your product feed is unique, each requires its own Branch link to ensure the user is not only taken to the correct content, but for Branch to correctly attribute the event.

The best way to create Branch deep links for your product feed is to create a ["long link"](https://docs.branch.io/links/integrate/#long-links) for each product feed item.

To create a Branch link:

1. Start with your base domain.
    1.  e.g. `https://example.app.link`
2. Add your deep link data as query parameters. NOTE: Be sure to URI encode each query parameter.
    2. e.g. `https://example.app.link?product_id=123&category=shoes`
3. Add any [fallback URLs](https://docs.branch.io/links/integrate/#fallback-to-a-specific-url) to ensure proper routing if the app isn't installed.
    3. e.g. `https://example.app.link?product_id=123&category=shoes&$fallback_url=https%3A%2F%2Fbranch.io%2Funiversal-ads%2F`
4. Finally, add the following analytics parameters needed to categorize your data accurately.
    1. [Generic Branch Analytics Parameters](https://docs.branch.io/links/integrate/#analytical-labels)
    2. [Facebook Analytics Parameters](#script-template-for-facebook)
    3. [Google Ads Analytics Parameters](#script-template-for-google-ads)

Your final link for Facebook looks like this:
```
https://example.app.link?product_id=123&category=shoes&$fallback_url=https%3A%2F%2Fbranch.io%2Funiversal-ads%2F&%243p=a_facebook&~advertising_partner_name=Facebook&%24one_time_use=false&branch_ad_format=App%20Only&~channel=Facebook&~feature=paid%20advertising&~campaign=%7B%7Bcampaign.name%7D%7D&~ad_id=%7B%7Bad.id%7D%7D&~ad_set_id=%7B%7Bad.set.id%7D%7D&~campaign_id=%7B%7Bcampaign.id%7D%7D
```

Your final link for Google Ads looks like this:
```
https://example.app.link?product_id=123&category=shoes&$fallback_url=https%3A%2F%2Fbranch.io%2Funiversal-ads%2F&%243p=a_google_adwords&~advertising_partner_name=Google%20Adwords&%24one_time_use=false&branch_ad_format=Cross-Platform%20Search&~channel=Google%20Adwords&~feature=paid%20advertising&~ad_set_id=%7Badgroupid%7D&~campaign_id=%7Bcampaignid%7D&~keyword=%7Bkeyword%7D&~placement=%7Bplacement%7D&~gclid=%7Bgclid%7D&~lpurl=%7Blpurl%7D&%24always_deeplink=false&%24android_deepview=false&%24ios_deepview=false&%24desktop_deepview=false&%24android_passive_deepview=false&%24ios_passive_deepview=false&%24
```

## Creating a Product Feed

When you create a feed, you're creating a database of products or services that can be used in your responsive/dynamic ads. Depending on your inventory type, data feeds need to have different information columns.

### Facebook Data Feeds

There are several different methods to add items to your catalog. One method is to use a data feed, which allows you to add many items to your catalog at once. A data feed is a spreadsheet file where you enter information about your inventory.

Please refer to Facebook’s Ads documentation for the following:

*   [Add Catalog Items with a Data Feed](https://www.facebook.com/business/help/125074381480892)
*   [Use a Data Feed Template](https://www.facebook.com/business/help/1898524300466211)
*   [Data Feed Columns](https://developers.facebook.com/docs/marketing-api/catalog-feed-setup#da-commerce)
*   [Troubleshoot Data Feeds](https://www.facebook.com/business/help/2041876302542944)

### Google Feeds

The type of feed you create should match the business type you selected when creating your Dynamic remarketing campaign. Use the "Custom" feed only if the other business types don't apply to your products or services.

Please refer to Google’s [Create a feed for your responsive ads](https://support.google.com/google-ads/answer/6053288?hl=en&ref_topic=3180758) for the following:

*   About feeds
*   Get feed templates and specs for your business type
*   Create and upload a new feed
*   Fix problems with your feed

## Placing your Branch Link in the Product Feed

Once you’ve created a Branch link for each item in your product feed, you need to include these links in your product feed file before uploading it to Facebook or Google Ads.

When creating your product feed, one of the required parameters is the `link` parameter.  The `link` parameter is typically a URL link to merchant's site (website landing page) where you can purchase or learn more about the item.

When using Branch links - that already contain all of the proper routing given multiple scenarios - you must substitute your website landing page URL with your Branch link.

## Uploading Your Feed

### To Facebook

We recommend using [Facebook’s Product Feed Debug Tool](https://business.facebook.com/ads/product_feed/debug) to test and debug your Product Feed format. The largest file size accepted by the tool is 50MB.

To upload your product feed to Facebook, please follow Facebook’s help document on [Add Catalog Items with a Data Feed](https://www.facebook.com/business/help/125074381480892).

### To Google Ads

There are limits to the number of feeds and feed items per account. Learn more [About Google Ads account limits. ](https://support.google.com/google-ads/answer/6372658)

To upload your product feed to Google Ads, please follow Google’s help document on [Create a feed for your responsive ads](https://support.google.com/google-ads/answer/6053288?hl=en&ref_topic=3180758).

If you're a retail business, use the [Google Merchant Center to upload your product feed](https://support.google.com/merchants/answer/188477).

## Branch Product Feed Link Script

To expedite the link creation process, we recommend using a script to programmatically bulk build your Branch links and insert them into your pre-existing feed CSV file.

The Branch Product Feed Link script parses your pre-existing product feed CSV file and (1) creates correctly formatted Branch links for each item in your feed, and (2) updates the `link` column with the newly created Branch link.  

The script includes the templates necessary to append your Branch links with the necessary information required for proper routing and attribution for Facebook and Google campaigns.

**NOTE**: The website URLs in the `link` column of your CSV will be appended to the Branch link as the URL to fallback to using the `fallback_url` parameter if (1) the user does not have the app installed, or (2) Branch cannot deep link the user into the app.

### Script Template for Facebook

The following parameters and corresponding values will be appended to your Branch link base domain - <code>[https://example.app.link](https://example.app.link) -</code> for Facebook Ad campaigns.

<table>
  <tr>
   <td><strong>Parameter</strong>
   </td>
   <td><strong>Value</strong>
   </td>
  </tr>
  <tr>
   <td>$3p
   </td>
   <td>a_facebook
   </td>
  </tr>
  <tr>
   <td>~advertising_partner_name
   </td>
   <td>Facebook
   </td>
  </tr>
  <tr>
   <td>$one_time_use
   </td>
   <td>false
   </td>
  </tr>
  <tr>
   <td>~branch_ad_format
   </td>
   <td>Cross-Platform Display OR App Only
   </td>
  </tr>
  <tr>
   <td>~channel
   </td>
   <td>Facebook
   </td>
  </tr>
  <tr>
   <td>~feature
   </td>
   <td>paid advertising
   </td>
  </tr>
  <tr>
   <td>~campaign
   </td>
   <td>{{campaign.name}}
   </td>
  </tr>
  <tr>
   <td>~ad_id
   </td>
   <td>{{ad.id}}
   </td>
  </tr>
  <tr>
   <td>~ad_set_id
   </td>
   <td>{{adset.id}}
   </td>
  </tr>
  <tr>
   <td>~campaign_id
   </td>
   <td>{{campaign.id}}
   </td>
  </tr>
</table>

### Script Template for Google Ads

The following parameters and corresponding values will be appended to your Branch link base domain - <code>[https://example.app.link](https://example.app.link) -</code> for Google Ads campaigns.

<table>
  <tr>
   <td><strong>Parameter</strong>
   </td>
   <td><strong>Value</strong>
   </td>
  </tr>
  <tr>
   <td>$3p
   </td>
   <td>a_google_adwords
   </td>
  </tr>
  <tr>
   <td>~advertising_partner_name
   </td>
   <td>Google Adwords
   </td>
  </tr>
  <tr>
   <td>$one_time_use
   </td>
   <td>false
   </td>
  </tr>
  <tr>
   <td>~branch_ad_format
   </td>
   <td>Cross-Platform Search
   </td>
  </tr>
  <tr>
   <td>~channel
   </td>
   <td>Google Adwords
   </td>
  </tr>
  <tr>
   <td>~feature
   </td>
   <td>paid advertising
   </td>
  </tr>
  <tr>
   <td>~ad_set_id
   </td>
   <td>{adgroupid}
   </td>
  </tr>
  <tr>
   <td>~campaign_id
   </td>
   <td>{campaignid}
   </td>
  </tr>
  <tr>
   <td>~keyword
   </td>
   <td>{keyword}
   </td>
  </tr>
  <tr>
   <td>~placement
   </td>
   <td>{placement}
   </td>
  </tr>
  <tr>
   <td>gclid
   </td>
   <td>{gclid}
   </td>
  </tr>
  <tr>
   <td>lpurl
   </td>
   <td>{lpurl}
   </td>
  </tr>
  <tr>
   <td>$always_deeplink
   </td>
   <td>false
   </td>
  </tr>
  <tr>
   <td>$android_deepview
   </td>
   <td>false
   </td>
  </tr>
  <tr>
   <td>$ios_deepview
   </td>
   <td>false
   </td>
  </tr>
  <tr>
   <td>$desktop_deepview
   </td>
   <td>false
   </td>
  </tr>
  <tr>
   <td>$android_passive_deepview
   </td>
   <td>false
   </td>
  </tr>
  <tr>
   <td>$ios_passive_deepview
   </td>
   <td>false
   </td>
  </tr>
</table>

## Running the Branch Product Feed Script

In order to run the product feed script, you will need (1) Your product feed CSV, (2) Github account, (3) Python 3.5+.

1. Clone or download the [Branch Product Feed v1](https://github.com/jmandarino-branch/product-feedv1) Github repo.
2. Upload your pre-existing product feed CSV to the **Input** folder.
3. Open the **settings.json** file and edit the following parameter’s values:
    1. "**input_file**": "File name of your uploaded CSV",
    2. "**base_url**": "Your default link domain, e.g. https://example.app.link",
    3. "**active_template**": “Name of the template to apply from the template folder”
4. Execute script `python main.py` | `./main.py` etc.
5. Retrieve updated product feed CSV from the **Output** folder.
