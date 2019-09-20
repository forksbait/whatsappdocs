## Postman

  - Use `Postman` to test Branch API for requests, responses, and code examples

  - Change the `branch_key` to match your [Branch Dashboard](https://dashboard.branch.io/account-settings/app)

  - [![Run in Postman](https://run.pstmn.io/button.svg)](https://app.getpostman.com/run-collection/3dadd3558239b25f385d)

## Link

- ### Link create

    - *Request*

        ```bash
        curl -XPOST https://api2.branch.io/v1/url \
          -d '{
          "branch_key": "key_live_kaFuWw8WvY7yn1d9yYiP8gokwqjV0Swt",
          "channel": "facebook",
          "feature": "onboarding",
          "campaign": "new product",
          "stage": "new user",
          "tags": ["one", "two", "three"],
          "data": {
            "$canonical_identifier": "content/123",
            "$og_title": "Title from Deep Link",
            "$og_description": "Description from Deep Link",
            "$og_image_url": "http://www.lorempixel.com/400/400/",
            "$desktop_url": "http://www.example.com",
            "custom_boolean": true,
            "custom_integer": 1243,
            "custom_string": "everything",
            "custom_array": [1,2,3,4,5,6],
            "custom_object": { "random": "dictionary" }
          }
        }'
        ```

    - *Response*

        ```js
        {
          "url": "https://example.app.link/WgiqvsepqF"
        }
        ```

    - Parameters

        | Key | Value | Usage | Required
        | --- | :-: | --- | :-:
        | branch_key | `string` | From your [Branch Settings Dashboard](https://dashboard.branch.io/account-settings/app) | √
        | ... | ... | Parameters from [Configuring Links](/links/integrate/) |

- ### Link create bulk

    - *Request*

        ```bash
        curl -XPOST https://api2.branch.io/v1/url/bulk/key_live_kaFuWw8WvY7yn1d9yYiP8gokwqjV0Swt \
          -d '[
            {
              "channel": "facebook",
              "feature": "onboarding",
              "campaign": "new product",
              "stage": "new user",
              "tags": ["one", "two", "three"],
              "data": {
                "$canonical_identifier": "content/123",
                "$og_title": "Title from Deep Link",
                "$og_description": "Description from Deep Link",
                "$og_image_url": "http://www.lorempixel.com/400/400/",
                "$desktop_url": "http://www.example.com",
                "custom_boolean": true,
                "custom_integer": 1243,
                "custom_string": "everything",
                "custom_array": [1,2,3,4,5,6],
                "custom_object": { "random": "dictionary" }
              }
            },
            {
              "channel": "facebook",
              "feature": "onboarding",
              "campaign": "new product",
              "stage": "new user",
              "tags": ["one", "two", "three"],
              "data": {
                "$canonical_identifier": "content/123",
                "$og_title": "Title from Deep Link",
                "$og_description": "Description from Deep Link",
                "$og_image_url": "http://www.lorempixel.com/400/400/",
                "$desktop_url": "http://www.example.com"
              }
            }
          ]'
        ```

    - *Response*

        ```js
        [
          {
            "url": "https://example.app.link/0AjuiLcpqF"
          },
          {
            "url": "https://example.app.link/5IULiLcpqF"
          }
        ]
        ```

    - Parameters

        | Key | Value | Usage | Required
        | --- | :-: | --- | :-:
        | branch_key | `string` | From your [Branch Settings Dashboard](https://dashboard.branch.io/settings) | √
        | ... | ... | Parameters from [Configuring Links](/links/integrate/) |

    - Bulk link creator is limited to a JSON payload size of 250KB at a time.

- ### Link read

    - Returns [deep link properties](/links/integrate/#read-deep-links)

    - *Request*

        ```bash
        curl -XGET 'https://api2.branch.io/v1/url?url=https://example.app.link/WgiqvsepqF&branch_key=key_live_kaFuWw8WvY7yn1d9yYiP8gokwqjV0Swt'
        ```

    - *Response*

        ```js
        {
          "campaign": "new product",
          "channel": "facebook",
          "feature": "onboarding",
          "stage": "new user",
          "tags": [
            "one",
            "two",
            "three"
          ],
          "data": {
            "$canonical_identifier": "content/123",
            "$desktop_url": "http://www.example.com",
            "$og_description": "Description from Deep Link",
            "$og_image_url": "http://www.lorempixel.com/400/400/",
            "$og_title": "Title from Deep Link",
            "$one_time_use": false,
            "custom_array": [
              1,
              2,
              3,
              4,
              5,
              6
            ],
            "custom_boolean": true,
            "custom_integer": 1243,
            "custom_object": {
              "random": "dictionary"
            },
            "custom_string": "everything",
            "~campaign": "new product",
            "~channel": "facebook",
            "~creation_source": 0,
            "~feature": "onboarding",
            "~id": "423196192848102356",
            "~stage": "new user",
            "~tags": [
              "one",
              "two",
              "three"
            ],
            "url": "https://example.app.link/WgiqvsepqF"
          },
          "type": 0,
          "alias": null
        }
        ```

    - Parameters

        | Key | Value | Usage | Required
        | --- | :-: | --- | :-:
        | branch_key | `string` | From your [Branch Settings Dashboard](https://dashboard.branch.io/settings) | √
        | url | `string` | The deep link url | √

- ### Link update

    - *Request*

          ```bash
          curl -XPUT 'https://api2.branch.io/v1/url?url=https%3A%2F%2Fexample.app.link%2F5IULiLcpqF' \
            -d '{
            "branch_key": "key_live_kaFuWw8WvY7yn1d9yYiP8gokwqjV0Swt",
            "branch_secret": "secret_live_RrrsLqpzVcoVWf5t4ncQVpzlg2pRpGH9",
            "channel": "twitter",
            "data":{
              "name":"alex",
              "user_id":"12346"
            }
          }'
          ```

    - *Response*

          ```js
          {
            "campaign": "new product",
            "channel": "twitter",
            "feature": "onboarding",
            "stage": "new user",
            "tags": [
              "one",
              "two",
              "three"
            ],
            "data": {
              "$one_time_use": false,
              "name": "alex",
              "user_id": "12346",
              "~campaign": "new product",
              "~channel": "twitter",
              "~creation_source": 0,
              "~feature": "onboarding",
              "~id": "423196096467215333",
              "~stage": "new user",
              "~tags": [
                "one",
                "two",
                "three"
              ],
              "url": "https://example.app.link/5IULiLcpqF"
            },
            "type": 0,
            "alias": null
          }
          ```

    - Parameters

        | Key | Value | Usage | Required
        | --- | :-: | --- | :-:
        | branch_key | `string` | From your [Branch Settings Dashboard](https://dashboard.branch.io/settings) | √
        | branch_secret | `string` | From your [Branch Settings Dashboard](https://dashboard.branch.io/settings) | √
        | url | `string` | The deep link url | √

- ### Link update tips

    - A link's `data` object is overwritten entirely by the [Link update](#link-update) API, so make sure to include all of the link's data when updating it (not just the data you're changing)
    - To update links in bulk, combine the [Link update](#link-update) and [Link read](#link-read) APIs when creating a script.  The sample Python script below reads a 2-column CSV file, and updates a key specified in the script for all links listed in column A, with the values in column B:

          ```python
          import requests
          import csv
          import sys
          import urllib
          import json

          #Insert API key & App Secret from the Branch dashboard, and the Link data key you want to change in each link **
          branch_key = "[API_KEY]"
          branch_secret = "[APP_SECRET]"
          key_to_update = "[DATA_KEY_TO_UPDATE]"

          #Insert filename for CSV containing links to update in first column, and values to add in second column **
          ifile = open('[INSERT_FILENAME].csv', "rb")

          #Constants
          branchendpoint = "https://api2.branch.io/v1/url?url="
          reader = csv.reader(ifile, delimiter=',')

          #Uncomment the next line if you want the script to skip the first line of the CSV
          #next(reader)

          #Loop through CSV
          for row in reader:

            #Retrieve link data for link being updated
            url = urllib.quote_plus(row[0])
            getrequest = branchendpoint + url + "&branch_key=" + branch_key
            linkdata = requests.get(getrequest)
            jsonData = json.loads(linkdata.text)

            #Set credentials for update API
            jsonData["branch_key"] = branch_key
            jsonData["branch_secret"] = branch_secret

            #Update specified data key
            newValue = row[1]
            if key_to_update in jsonData:
              jsonData[key_to_update] = newValue
            if key_to_update in jsonData["data"]:
              jsonData["data"][key_to_update] = newValue

            #PUT request to update link
            payload = json.dumps(jsonData)
            putrequest = branchendpoint + url
            r = requests.put(putrequest, json=jsonData)
            print(r.url)
            print(r)
            print
          ifile.close()
          ```


## Event

- Please refer to the detailed docs on event tracking located in the [V2 Event section](/apps/v2event).

## User

- ### User read

    - *Request*

        ```bash
        # identity
        curl -XGET 'https://api2.branch.io/v1/profile?branch_key=key_live_kaFuWw8WvY7yn1d9yYiP8gokwqjV0Swt&identity=steve'

        # identity id
        curl -XGET 'https://api2.branch.io/v1/profile?branch_key=key_live_kaFuWw8WvY7yn1d9yYiP8gokwqjV0Swt&identity_id=444'
        ```

    - *Response*

        ```js
        {
          "identity_id": 444,
          "identity": "steve",
          "link": "https://example.app.link/?%24identity_id=444"
        }
        ```

    - Parameters

        | Key | Value | Usage | Required
        | --- | :-: | --- | :-:
        | branch_key | `string` | From your [Branch Settings Dashboard](https://dashboard.branch.io/settings) | √
        | identity | `string` | Unique user id, also known as the `Developer Id` on your [Branch Identity Dashboard](https://dashboard.branch.io/liveview/identities) | √*
        | identity_id | `string` | Unique user id for Branch, also known as the `Branch Identity Id` on your [Branch Identity Dashboard](https://dashboard.branch.io/liveview/identities) | √*

        - `*` =  `identity` *OR* `identity_id` is required

## Referral

- ### Referral link

    - *Request*

        ```bash
        curl -XPOST https://api2.branch.io/v1/url \
          -d '{
          "branch_key": "key_live_kaFuWw8WvY7yn1d9yYiP8gokwqjV0Swt",
          "channel": "facebook",
          "feature": "referrals",
          "campaign": "referral-campaign",
          "identity": "BranchMonster" // specify identity name
        }'
        ```

    - *Response*

        ```bash
        {"url":"https://example.app.link/gvS4qgD8HP"}
        ```

- ### Referral reward

    - *Request*

        ```bash
        curl -XPOST https://api2.branch.io/v1/credits \
          -d '{
          "branch_key": "key_live_kaFuWw8WvY7yn1d9yYiP8gokwqjV0Swt",
          "branch_secret": "secret_live_RrrsLqpzVcoVWf5t4ncQVpzlg2pRpGH9",
          "identity": "steve",
          "amount": "10",
          "bucket": "default"
        }'
        ```

    - *Response*

        ```js
        {
          "success": true
        }
        ```

    - Parameters

        | Key | Value | Usage | Required
        | --- | :-: | --- | :-:
        | branch_key | `string` | From your [Branch Settings Dashboard](https://dashboard.branch.io/settings) | √
        | branch_secret | `string` | From your [Branch Settings Dashboard](https://dashboard.branch.io/settings) | √
        | identity | `string` | Unique user id, also known as the `Developer Id` on your [Branch Identity Dashboard](https://dashboard.branch.io/liveview/identities) | √
        | amount | `string` | Number of credits | √
        | bucket | `string` | The category where the credits are save to (defaults to `default`) |

- ### Referral redeem

    - *Request*

        ```bash
        curl -XPOST https://api2.branch.io/v1/redeem \
          -d '{
          "branch_key": "key_live_kaFuWw8WvY7yn1d9yYiP8gokwqjV0Swt",
          "branch_secret": "secret_live_RrrsLqpzVcoVWf5t4ncQVpzlg2pRpGH9",
          "identity": "steve",
          "amount": "5",
          "bucket": "default"
        }'
        ```

    - *Response*

        ```js
        // success
        {}

        // failure
        {
          "error": {
            "code": 402,
            "message": "Not enough credits to redeem."
          }
        }
        ```

- ### Referral read

    - *Request*

        ```bash
        curl -XGET 'https://api2.branch.io/v1/credits?branch_key=key_live_kaFuWw8WvY7yn1d9yYiP8gokwqjV0Swt&identity=steve'
        ```

    - *Response*

        ```js
        {
          "default": 40
        }
        ```

- ### Referral history

    - *Request*

        ```bash
        curl -XGET 'https://api2.branch.io/v1/credithistory?branch_key=key_live_kaFuWw8WvY7yn1d9yYiP8gokwqjV0Swt&identity=steve'
        ```

    - *Response*

        ```js
        [
          {
            "transaction": {
              "date": "2017-08-07T22:15:10.503Z",
              "id": "423229952507361694",
              "bucket": "default",
              "type": 2,
              "amount": -5
            },
            "event": {
              "name": null,
              "metadata": null
            },
            "referrer": null,
            "referree": null
          },
          {
            "transaction": {
              "date": "2017-08-07T22:15:01.818Z",
              "id": "423229916080032437",
              "bucket": "default",
              "type": 2,
              "amount": -5
            },
            "event": {
              "name": null,
              "metadata": null
            },
            "referrer": null,
            "referree": null
          },
          {
            "transaction": {
              "date": "2017-08-07T22:10:57.224Z",
              "id": "423228890178439487",
              "bucket": "default",
              "type": 1,
              "amount": 10
            },
            "event": {
              "name": null,
              "metadata": null
            },
            "referrer": null,
            "referree": null
          },
          {
            "transaction": {
              "date": "2017-08-07T22:10:56.416Z",
              "id": "423228886789240847",
              "bucket": "default",
              "type": 1,
              "amount": 10
            },
            "event": {
              "name": null,
              "metadata": null
            },
            "referrer": null,
            "referree": null
          }
        ]
        ```

- ### Referral reconcile

    - *Request*

        ```bash
        curl -X POST https://api2.branch.io/v1/reconcile \
          -d '{
          "branch_key": "key_live_kaFuWw8WvY7yn1d9yYiP8gokwqjV0Swt",
          "branch_secret": "secret_live_RrrsLqpzVcoVWf5t4ncQVpzlg2pRpGH9",
          "identity": "steve",
          "amount": "20",
          "bucket": "default"
        }'
        ```

    - *Response*

        ```js
        {
          "id": "423232788708309278",
          "app_id": "423194549918126821",
          "identity_id": 444,
          "type": 4,
          "bucket": "default",
          "amount": -20,
          "date": "2017-08-07T22:26:26.706Z"
        }
        ```

- ### Referral create rule

    - *Request*

        ```bash
        curl -XPOST https://api2.branch.io/v1/eventresponse \
          -d '{
          "branch_key": "key_live_kaFuWw8WvY7yn1d9yYiP8gokwqjV0Swt",
          "branch_secret": "secret_live_RrrsLqpzVcoVWf5t4ncQVpzlg2pRpGH9",
          "calculation_type": 2,
          "location": 4,
          "type": "credit",
          "event": "signup",
          "metadata": {
            "web_hook_url": "http://www.example.com",
            "amount": "20",
            "bucket": "default"
          },
          "filter": {
          "viewed_tutorial": true,
          "geo": "over_here"
          }
        }
        '
        ```

    - *Response*

        ```js
        {}
        ```

    - Parameters

        | Key | Value | Usage | Required
        | --- | :-: | --- | :-:
        | branch_key | `string` | From your [Branch Settings Dashboard](https://dashboard.branch.io/settings) | √
        | branch_secret | `string` | From your [Branch Settings Dashboard](https://dashboard.branch.io/settings) | √
        | calculation_type | `int` | `0` reward for each use, `1` reward for first use only | √
        | location | `int` | `0` all acting users, `1` referring users, `4`, referred acting users | √
        | type | `string` | `credit` reward points | √
        | web_hook | `string` | The url to call when an event occurs |  `type` = `web_hook`
        | amount | `string` | Number of credits |  `type` = `credit`
        | bucket | `string` | The category where the credits are save to | `type` = `credit`
        | filter | `json` | This is the set of keys and values that must be contained in the event metadata for this reward to be issued |

    !!! note "Please take note of the `type` parameter"
        `type` = `credit` will create a reward rule on your dashboard, but `type` = `web_hook` will create a webhook each time the reward rule is triggered. To see the structure of the webhook callback, please test this with [RequestBin](https://requestbin.com/) or a similar service.

- ### Referral troubleshooting

    - Referral `credits` cannot go below zero

## Webhook

- ### Webhook create

    - See [Referral create rule](#referral-create-rule)

## API troubleshooting

- Use your `branch_key` and `branch_secret` from your [Branch Settings Dashboard](https://dashboard.branch.io/settings)

- Use your `user_id` from your [Branch Account Dashboard](https://dashboard.branch.io/settings/account)

- Values have a `255` character max
