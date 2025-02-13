## Cisco Umbrella Reporting

Use Cisco Umbrella's Reporting to monitor your Umbrella integration and gain a better understanding of your Umbrella usage. Gain insights into request activity and blocked activity, determining which of your identities are generating blocked requests. Reports help build actionable intelligence in addressing security threats including changes in usage trends over time.

The Umbrella Reporting v2 API provides visibility into your core network and security activities and Umbrella logs.
This integration was integrated and tested with version xx of 
Cisco-umbrella-reporting.

## Configure Cisco Umbrella Reporting on Cortex XSOAR

1. Navigate to **Settings** > **Integrations** > **Servers & Services**.
2. Search for Cisco Umbrella Reporting.
3. Click **Add instance** to create and configure a new integration instance.

    | **Parameter** | **Description**                        | **Required** |
    |----------------------------------------| --- | --- |
    | API URL | Cisco Umbrella Reporting api base url. | False |
    | Organization ID | Organization ID.                       | True |
    | Client ID | Client ID.                             | True |
    | Client Secret | Client Secret.                         | True |
    | Trust any certificate (not secure) |                                        | False |
    | Use system proxy settings |                                        | False |

4. Click **Test** to validate the URLs, token, and connection.
## Commands
You can execute these commands from the Cortex XSOAR CLI, as part of an automation, or in a playbook.
After you successfully execute a command, a DBot message appears in the War Room with the command details.
### umbrella-reporting-destination-list
***
List of destinations ordered by the number of requests made in descending order.


#### Base Command

`umbrella-reporting-destination-list`
#### Input

| **Argument Name** | **Description** | **Required** |
| --- | --- | --- |
| traffic_type | Specify the type of traffic. Valid values: dns, proxy, firewall, or ip. By default value will be all i.e. dns, proxy, firewall and ip. Possible values are: dns, proxy, firewall, ip. | Optional | 
| domains | A domain name or comma-delimited list of domain name. | Optional | 
| ip | An IP address. | Optional | 
| urls | A URL or comma-delimited list of URL. | Optional | 
| ports | A port number or comma-delimited list of port number. | Optional | 
| sha256 | A SHA-256 hash. | Optional | 
| threats | A threat name or comma-delimited list of threat name. | Optional | 
| threat_types | A threat type or comma-delimited list of threat type. | Optional | 
| amp_disposition | An AMP disposition string. Possible values are: clean, malicious, unknown. | Optional | 
| from | A timestamp (milliseconds) or relative time string (for example:-1days' or '1639146300000'). Filter for data that appears after this time. By default value is -7days. | Optional | 
| to | A timestamp (milliseconds) or relative time string (for example:'now' or 1661510185000). Filter for data that appears before this time. By default value is 'now'. | Optional | 
| limit | The maximum number of records to return from the collection. Default value of limit is 50. | Optional | 
| identity_types | An identity type or comma-delimited list of identity type. | Optional | 
| verdict | A verdict string. Possible values are: allowed, blocked, proxied. | Optional | 
| page | The page number. Default Page number is 1. | Optional | 
| page_size | The number of requested results per page. | Optional | 


#### Context Output

| **Path** | **Type** | **Description** |
| --- | --- | --- |
| UmbrellaReporting.Destination.count | Number | Total number of requests made for this destination | 
| UmbrellaReporting.Destination.domain | String | Destination | 
| UmbrellaReporting.Destination.bandwidth | Number | Bandwidth | 
| UmbrellaReporting.Destination.rank | Number | The rank of the result based on the number of requests | 
| UmbrellaReporting.Destination.policycategories.id | Number | ID of category. | 
| UmbrellaReporting.Destination.policycategories.label | String | The human readable label of the category. | 
| UmbrellaReporting.Destination.policycategories.type | String | the type of category. | 
| UmbrellaReporting.Destination.policycategories.deprecated | Boolean | If the category is a legacy category. | 
| UmbrellaReporting.Destination.policycategories.integration | Boolean | If the category is an integration. | 
| UmbrellaReporting.Destination.categories.id | Number | ID of category. | 
| UmbrellaReporting.Destination.categories.label | String | The human readable label of the category. | 
| UmbrellaReporting.Destination.categories.type | String | The type of category. | 
| UmbrellaReporting.Destination.categories.deprecated | Boolean | if the category is a legacy category. | 
| UmbrellaReporting.Destination.categories.integration | Boolean | If the category is an integration. | 
| UmbrellaReporting.Destination.counts.allowedrequests | Number | Number of requests that were allowed | 
| UmbrellaReporting.Destination.counts.blockedrequests | Number | Number of requests that were blocked | 
| UmbrellaReporting.Destination.counts.requests | Number | Total number of requests | 

#### Command example
```!umbrella-reporting-destination-list limit=2```
#### Context Example
```json
{
    "UmbrellaReporting": {
        "Destination": [
            {
                "bandwidth": null,
                "categories": [
                    {
                        "deprecated": false,
                        "id": 113,
                        "integration": false,
                        "label": "Computer Security",
                        "type": "content"
                    }
                ],
                "count": 456,
                "counts": {
                    "allowedrequests": 456,
                    "blockedrequests": 0,
                    "requests": 456
                },
                "domain": "rp.cloud.threatseeker.com",
                "policycategories": [],
                "rank": 1
            },
            {
                "bandwidth": null,
                "categories": [
                    {
                        "deprecated": false,
                        "id": 163,
                        "integration": false,
                        "label": "Business and Industry",
                        "type": "content"
                    },
                    {
                        "deprecated": false,
                        "id": 167,
                        "integration": false,
                        "label": "Computers and Internet",
                        "type": "content"
                    },
                    {
                        "deprecated": false,
                        "id": 142,
                        "integration": false,
                        "label": "Online Meetings",
                        "type": "content"
                    },
                    {
                        "deprecated": false,
                        "id": 148,
                        "integration": false,
                        "label": "Application",
                        "type": "application"
                    },
                    {
                        "deprecated": true,
                        "id": 25,
                        "integration": false,
                        "label": "Software/Technology",
                        "type": "content"
                    },
                    {
                        "deprecated": true,
                        "id": 32,
                        "integration": false,
                        "label": "Business Services",
                        "type": "content"
                    }
                ],
                "count": 442,
                "counts": {
                    "allowedrequests": 442,
                    "blockedrequests": 0,
                    "requests": 442
                },
                "domain": "presence.teams.microsoft.com",
                "policycategories": [],
                "rank": 2
            }
        ]
    }
}
```

#### Human Readable Output

>### Destination List
>|Destination|Category|Allowed|Blocked|Requests|
>|---|---|---|---|---|
>| rp.cloud.threatseeker.com | Computer Security | 456 | 0 | 456 |
>| presence.teams.microsoft.com | Business and Industry,Computers and Internet,Online Meetings,Application,Software/Technology,Business Services | 442 | 0 | 442 |


### umbrella-reporting-category-list
***
List of categories ordered by the number of requests made matching the categories in descending order.


#### Base Command

`umbrella-reporting-category-list`
#### Input

| **Argument Name** | **Description** | **Required** |
| --- | --- | --- |
| traffic_type | Specify the type of traffic. Valid values: dns, proxy, or ip. By default value will be all i.e dns, proxy and ip. Possible values are: dns, proxy, ip. | Optional | 
| from | A timestamp (milliseconds) or relative time string (for example:-1days' or '1639146300000'). Filter for data that appears after this time. By default value is -7days. | Optional | 
| to | A timestamp (milliseconds) or relative time string (for example:'now' or 1661510185000). Filter for data that appears before this time. By default value is 'now'. | Optional | 
| limit | The maximum number of records to return from the collection. Default value of limit is 50. | Optional | 
| domains | A domain name or comma-delimited list of domain name. | Optional | 
| urls | A URL or comma-delimited list of URL. | Optional | 
| ip | An IP address. | Optional | 
| sha256 | A SHA-256 hash. | Optional | 
| threats | A threat name or comma-delimited list of threat name. | Optional | 
| threat_types | A threat type or comma-delimited list of threat type. | Optional | 
| amp_disposition | An AMP disposition string. Possible values are: clean, malicious, unknown. | Optional | 
| identity_types | An identity type or comma-delimited list of identity type. | Optional | 
| verdict | A verdict string. Possible values are: allowed, blocked, proxied. | Optional | 
| page | The page number. Default Page number is 1. | Optional | 
| page_size | The number of requested results per page. | Optional | 


#### Context Output

| **Path** | **Type** | **Description** |
| --- | --- | --- |
| UmbrellaReporting.Category.count | Number | Count | 
| UmbrellaReporting.Category.bandwidth | String | Bandwidth | 
| UmbrellaReporting.Category.category.id | Number | Category ID | 
| UmbrellaReporting.Category.category.type | String | Category Type | 
| UmbrellaReporting.Category.category.label | String | Category Label | 
| UmbrellaReporting.Category.category.integration | Boolean | Category integration | 
| UmbrellaReporting.Category.category.deprecated | String | Category deprecated | 
| UmbrellaReporting.Category.rank | Number | Rank | 

#### Command example
```!umbrella-reporting-category-list limit=2```
#### Context Example
```json
{
    "UmbrellaReporting": {
        "Category": [
            {
                "bandwidth": null,
                "category": {
                    "deprecated": false,
                    "id": 148,
                    "integration": false,
                    "label": "Application",
                    "type": "application"
                },
                "count": 14082,
                "rank": 1
            },
            {
                "bandwidth": 1236884238,
                "category": {
                    "deprecated": true,
                    "id": 32,
                    "integration": false,
                    "label": "Business Services",
                    "type": "content"
                },
                "count": 8930,
                "rank": 2
            },
            {
                "bandwidth": 1236885730,
                "category": {
                    "deprecated": true,
                    "id": 25,
                    "integration": false,
                    "label": "Software/Technology",
                    "type": "content"
                },
                "count": 8618,
                "rank": 3
            },
            {
                "bandwidth": 0,
                "category": {
                    "deprecated": false,
                    "id": 123,
                    "integration": false,
                    "label": "Infrastructure and Content Delivery Networks",
                    "type": "content"
                },
                "count": 7297,
                "rank": 4
            },
            {
                "bandwidth": null,
                "category": {
                    "deprecated": false,
                    "id": 163,
                    "integration": false,
                    "label": "Business and Industry",
                    "type": "content"
                },
                "count": 5736,
                "rank": 5
            },
            {
                "bandwidth": 1236884238,
                "category": {
                    "deprecated": false,
                    "id": 167,
                    "integration": false,
                    "label": "Computers and Internet",
                    "type": "content"
                },
                "count": 5686,
                "rank": 6
            },
            {
                "bandwidth": null,
                "category": {
                    "deprecated": true,
                    "id": 23,
                    "integration": false,
                    "label": "Search Engines",
                    "type": "content"
                },
                "count": 4015,
                "rank": 7
            },
            {
                "bandwidth": null,
                "category": {
                    "deprecated": false,
                    "id": 190,
                    "integration": false,
                    "label": "Search Engines and Portals",
                    "type": "content"
                },
                "count": 2763,
                "rank": 8
            },
            {
                "bandwidth": null,
                "category": {
                    "deprecated": false,
                    "id": 27,
                    "integration": false,
                    "label": "Advertisements",
                    "type": "content"
                },
                "count": 2255,
                "rank": 9
            },
            {
                "bandwidth": null,
                "category": {
                    "deprecated": false,
                    "id": 142,
                    "integration": false,
                    "label": "Online Meetings",
                    "type": "content"
                },
                "count": 1314,
                "rank": 10
            },
            {
                "bandwidth": null,
                "category": {
                    "deprecated": true,
                    "id": 4,
                    "integration": false,
                    "label": "Chat",
                    "type": "content"
                },
                "count": 1302,
                "rank": 11
            },
            {
                "bandwidth": null,
                "category": {
                    "deprecated": true,
                    "id": 15,
                    "integration": false,
                    "label": "Instant Messaging",
                    "type": "content"
                },
                "count": 1276,
                "rank": 12
            },
            {
                "bandwidth": null,
                "category": {
                    "deprecated": false,
                    "id": 205,
                    "integration": false,
                    "label": "Online Document Sharing and Collaboration",
                    "type": "content"
                },
                "count": 1089,
                "rank": 13
            },
            {
                "bandwidth": 1492,
                "category": {
                    "deprecated": false,
                    "id": 113,
                    "integration": false,
                    "label": "Computer Security",
                    "type": "content"
                },
                "count": 1059,
                "rank": 14
            },
            {
                "bandwidth": null,
                "category": {
                    "deprecated": true,
                    "id": 28,
                    "integration": false,
                    "label": "Video Sharing",
                    "type": "content"
                },
                "count": 1053,
                "rank": 15
            },
            {
                "bandwidth": null,
                "category": {
                    "deprecated": false,
                    "id": 194,
                    "integration": false,
                    "label": "Streaming Video",
                    "type": "content"
                },
                "count": 984,
                "rank": 16
            },
            {
                "bandwidth": null,
                "category": {
                    "deprecated": true,
                    "id": 31,
                    "integration": false,
                    "label": "Webmail",
                    "type": "content"
                },
                "count": 878,
                "rank": 17
            },
            {
                "bandwidth": null,
                "category": {
                    "deprecated": false,
                    "id": 164,
                    "integration": false,
                    "label": "Chat and Instant Messaging",
                    "type": "content"
                },
                "count": 868,
                "rank": 18
            },
            {
                "bandwidth": null,
                "category": {
                    "deprecated": false,
                    "id": 162,
                    "integration": false,
                    "label": "Web-based Email",
                    "type": "content"
                },
                "count": 864,
                "rank": 19
            },
            {
                "bandwidth": null,
                "category": {
                    "deprecated": false,
                    "id": 141,
                    "integration": false,
                    "label": "Organizational Email",
                    "type": "content"
                },
                "count": 858,
                "rank": 20
            },
            {
                "bandwidth": null,
                "category": {
                    "deprecated": false,
                    "id": 198,
                    "integration": false,
                    "label": "Cloud and Data Centers",
                    "type": "content"
                },
                "count": 683,
                "rank": 21
            },
            {
                "bandwidth": null,
                "category": {
                    "deprecated": false,
                    "id": 24,
                    "integration": false,
                    "label": "Social Networking",
                    "type": "content"
                },
                "count": 630,
                "rank": 22
            },
            {
                "bandwidth": null,
                "category": {
                    "deprecated": false,
                    "id": 132,
                    "integration": false,
                    "label": "SaaS and B2B",
                    "type": "content"
                },
                "count": 525,
                "rank": 23
            },
            {
                "bandwidth": null,
                "category": {
                    "deprecated": true,
                    "id": 8,
                    "integration": false,
                    "label": "Ecommerce/Shopping",
                    "type": "content"
                },
                "count": 498,
                "rank": 24
            },
            {
                "bandwidth": null,
                "category": {
                    "deprecated": true,
                    "id": 17,
                    "integration": false,
                    "label": "Movies",
                    "type": "content"
                },
                "count": 355,
                "rank": 25
            },
            {
                "bandwidth": null,
                "category": {
                    "deprecated": true,
                    "id": 18,
                    "integration": false,
                    "label": "News/Media",
                    "type": "content"
                },
                "count": 353,
                "rank": 26
            },
            {
                "bandwidth": null,
                "category": {
                    "deprecated": false,
                    "id": 124,
                    "integration": false,
                    "label": "Internet Telephony",
                    "type": "content"
                },
                "count": 340,
                "rank": 27
            },
            {
                "bandwidth": null,
                "category": {
                    "deprecated": true,
                    "id": 54,
                    "integration": false,
                    "label": "Research/Reference",
                    "type": "content"
                },
                "count": 256,
                "rank": 28
            },
            {
                "bandwidth": null,
                "category": {
                    "deprecated": true,
                    "id": 21,
                    "integration": false,
                    "label": "Portals",
                    "type": "content"
                },
                "count": 252,
                "rank": 29
            },
            {
                "bandwidth": null,
                "category": {
                    "deprecated": false,
                    "id": 138,
                    "integration": false,
                    "label": "Software Updates",
                    "type": "content"
                },
                "count": 249,
                "rank": 30
            },
            {
                "bandwidth": null,
                "category": {
                    "deprecated": true,
                    "id": 9,
                    "integration": false,
                    "label": "File Storage",
                    "type": "content"
                },
                "count": 196,
                "rank": 31
            },
            {
                "bandwidth": null,
                "category": {
                    "deprecated": true,
                    "id": 3,
                    "integration": false,
                    "label": "Blogs",
                    "type": "content"
                },
                "count": 184,
                "rank": 32
            },
            {
                "bandwidth": null,
                "category": {
                    "deprecated": false,
                    "id": 188,
                    "integration": false,
                    "label": "Reference",
                    "type": "content"
                },
                "count": 184,
                "rank": 33
            },
            {
                "bandwidth": null,
                "category": {
                    "deprecated": false,
                    "id": 131,
                    "integration": false,
                    "label": "Real Estate",
                    "type": "content"
                },
                "count": 161,
                "rank": 34
            },
            {
                "bandwidth": null,
                "category": {
                    "deprecated": true,
                    "id": 50,
                    "integration": false,
                    "label": "Non-Profits",
                    "type": "content"
                },
                "count": 138,
                "rank": 35
            },
            {
                "bandwidth": null,
                "category": {
                    "deprecated": false,
                    "id": 191,
                    "integration": false,
                    "label": "Shopping",
                    "type": "content"
                },
                "count": 133,
                "rank": 36
            },
            {
                "bandwidth": null,
                "category": {
                    "deprecated": false,
                    "id": 107,
                    "integration": false,
                    "label": "URL Shorteners",
                    "type": "content"
                },
                "count": 116,
                "rank": 37
            },
            {
                "bandwidth": null,
                "category": {
                    "deprecated": false,
                    "id": 179,
                    "integration": false,
                    "label": "News",
                    "type": "content"
                },
                "count": 101,
                "rank": 38
            },
            {
                "bandwidth": null,
                "category": {
                    "deprecated": false,
                    "id": 130,
                    "integration": false,
                    "label": "Professional Networking",
                    "type": "content"
                },
                "count": 74,
                "rank": 39
            },
            {
                "bandwidth": null,
                "category": {
                    "deprecated": true,
                    "id": 20,
                    "integration": false,
                    "label": "Photo Sharing",
                    "type": "content"
                },
                "count": 63,
                "rank": 40
            },
            {
                "bandwidth": null,
                "category": {
                    "deprecated": true,
                    "id": 16,
                    "integration": false,
                    "label": "Jobs/Employment",
                    "type": "content"
                },
                "count": 44,
                "rank": 41
            },
            {
                "bandwidth": null,
                "category": {
                    "deprecated": false,
                    "id": 169,
                    "integration": false,
                    "label": "Entertainment",
                    "type": "content"
                },
                "count": 36,
                "rank": 42
            },
            {
                "bandwidth": null,
                "category": {
                    "deprecated": false,
                    "id": 173,
                    "integration": false,
                    "label": "Government and Law",
                    "type": "content"
                },
                "count": 35,
                "rank": 43
            },
            {
                "bandwidth": null,
                "category": {
                    "deprecated": true,
                    "id": 35,
                    "integration": false,
                    "label": "Government",
                    "type": "content"
                },
                "count": 35,
                "rank": 44
            },
            {
                "bandwidth": null,
                "category": {
                    "deprecated": false,
                    "id": 55,
                    "integration": false,
                    "label": "Travel",
                    "type": "content"
                },
                "count": 31,
                "rank": 45
            },
            {
                "bandwidth": null,
                "category": {
                    "deprecated": true,
                    "id": 49,
                    "integration": false,
                    "label": "Forums/Message boards",
                    "type": "content"
                },
                "count": 29,
                "rank": 46
            },
            {
                "bandwidth": null,
                "category": {
                    "deprecated": false,
                    "id": 183,
                    "integration": false,
                    "label": "Online Communities",
                    "type": "content"
                },
                "count": 27,
                "rank": 47
            },
            {
                "bandwidth": null,
                "category": {
                    "deprecated": false,
                    "id": 122,
                    "integration": false,
                    "label": "Illegal Downloads",
                    "type": "content"
                },
                "count": 21,
                "rank": 48
            },
            {
                "bandwidth": null,
                "category": {
                    "deprecated": false,
                    "id": 128,
                    "integration": false,
                    "label": "Online Trading",
                    "type": "content"
                },
                "count": 21,
                "rank": 49
            },
            {
                "bandwidth": null,
                "category": {
                    "deprecated": false,
                    "id": 177,
                    "integration": false,
                    "label": "Job Search",
                    "type": "content"
                },
                "count": 20,
                "rank": 50
            },
            {
                "bandwidth": null,
                "category": {
                    "deprecated": true,
                    "id": 34,
                    "integration": false,
                    "label": "Financial Institutions",
                    "type": "content"
                },
                "count": 20,
                "rank": 51
            },
            {
                "bandwidth": null,
                "category": {
                    "deprecated": false,
                    "id": 71,
                    "integration": false,
                    "label": "Block List",
                    "type": "customer"
                },
                "count": 19,
                "rank": 52
            },
            {
                "bandwidth": null,
                "category": {
                    "deprecated": false,
                    "id": 134,
                    "integration": false,
                    "label": "Science and Technology",
                    "type": "content"
                },
                "count": 18,
                "rank": 53
            },
            {
                "bandwidth": null,
                "category": {
                    "deprecated": false,
                    "id": 184,
                    "integration": false,
                    "label": "Online Storage and Backup",
                    "type": "content"
                },
                "count": 18,
                "rank": 54
            },
            {
                "bandwidth": null,
                "category": {
                    "deprecated": false,
                    "id": 168,
                    "integration": false,
                    "label": "Education",
                    "type": "content"
                },
                "count": 16,
                "rank": 55
            },
            {
                "bandwidth": null,
                "category": {
                    "deprecated": true,
                    "id": 33,
                    "integration": false,
                    "label": "Educational Institutions",
                    "type": "content"
                },
                "count": 16,
                "rank": 56
            },
            {
                "bandwidth": null,
                "category": {
                    "deprecated": true,
                    "id": 26,
                    "integration": false,
                    "label": "Television",
                    "type": "content"
                },
                "count": 15,
                "rank": 57
            },
            {
                "bandwidth": null,
                "category": {
                    "deprecated": false,
                    "id": 193,
                    "integration": false,
                    "label": "Streaming Audio",
                    "type": "content"
                },
                "count": 14,
                "rank": 58
            },
            {
                "bandwidth": null,
                "category": {
                    "deprecated": false,
                    "id": 172,
                    "integration": false,
                    "label": "Finance",
                    "type": "content"
                },
                "count": 10,
                "rank": 59
            },
            {
                "bandwidth": null,
                "category": {
                    "deprecated": true,
                    "id": 5,
                    "integration": false,
                    "label": "Classifieds",
                    "type": "content"
                },
                "count": 9,
                "rank": 60
            },
            {
                "bandwidth": null,
                "category": {
                    "deprecated": false,
                    "id": 126,
                    "integration": false,
                    "label": "Mobile Phones",
                    "type": "content"
                },
                "count": 8,
                "rank": 61
            },
            {
                "bandwidth": null,
                "category": {
                    "deprecated": false,
                    "id": 182,
                    "integration": false,
                    "label": "Not Actionable",
                    "type": "content"
                },
                "count": 8,
                "rank": 62
            },
            {
                "bandwidth": null,
                "category": {
                    "deprecated": false,
                    "id": 175,
                    "integration": false,
                    "label": "Health and Medicine",
                    "type": "content"
                },
                "count": 7,
                "rank": 63
            },
            {
                "bandwidth": null,
                "category": {
                    "deprecated": false,
                    "id": 11,
                    "integration": false,
                    "label": "Games",
                    "type": "content"
                },
                "count": 5,
                "rank": 64
            },
            {
                "bandwidth": null,
                "category": {
                    "deprecated": false,
                    "id": 202,
                    "integration": false,
                    "label": "Internet of Things",
                    "type": "content"
                },
                "count": 5,
                "rank": 65
            },
            {
                "bandwidth": null,
                "category": {
                    "deprecated": false,
                    "id": 192,
                    "integration": false,
                    "label": "Sports and Recreation",
                    "type": "content"
                },
                "count": 5,
                "rank": 66
            },
            {
                "bandwidth": null,
                "category": {
                    "deprecated": true,
                    "id": 39,
                    "integration": false,
                    "label": "Sports",
                    "type": "content"
                },
                "count": 5,
                "rank": 67
            },
            {
                "bandwidth": null,
                "category": {
                    "deprecated": true,
                    "id": 36,
                    "integration": false,
                    "label": "Music",
                    "type": "content"
                },
                "count": 4,
                "rank": 68
            },
            {
                "bandwidth": null,
                "category": {
                    "deprecated": true,
                    "id": 22,
                    "integration": false,
                    "label": "Radio",
                    "type": "content"
                },
                "count": 4,
                "rank": 69
            },
            {
                "bandwidth": null,
                "category": {
                    "deprecated": false,
                    "id": 10,
                    "integration": false,
                    "label": "Gambling",
                    "type": "content"
                },
                "count": 3,
                "rank": 70
            },
            {
                "bandwidth": null,
                "category": {
                    "deprecated": false,
                    "id": 140,
                    "integration": false,
                    "label": "Web Page Translation",
                    "type": "content"
                },
                "count": 3,
                "rank": 71
            },
            {
                "bandwidth": null,
                "category": {
                    "deprecated": false,
                    "id": 115,
                    "integration": false,
                    "label": "Dining and Drinking",
                    "type": "content"
                },
                "count": 2,
                "rank": 72
            },
            {
                "bandwidth": null,
                "category": {
                    "deprecated": false,
                    "id": 180,
                    "integration": false,
                    "label": "Non-governmental Organizations",
                    "type": "content"
                },
                "count": 2,
                "rank": 73
            },
            {
                "bandwidth": null,
                "category": {
                    "deprecated": false,
                    "id": 201,
                    "integration": false,
                    "label": "DoH and DoT",
                    "type": "content"
                },
                "count": 2,
                "rank": 74
            },
            {
                "bandwidth": null,
                "category": {
                    "deprecated": true,
                    "id": 29,
                    "integration": false,
                    "label": "Visual Search Engines",
                    "type": "content"
                },
                "count": 2,
                "rank": 75
            },
            {
                "bandwidth": null,
                "category": {
                    "deprecated": true,
                    "id": 43,
                    "integration": false,
                    "label": "Proxy/Anonymizer",
                    "type": "content"
                },
                "count": 2,
                "rank": 76
            },
            {
                "bandwidth": null,
                "category": {
                    "deprecated": false,
                    "id": 117,
                    "integration": false,
                    "label": "Fashion",
                    "type": "content"
                },
                "count": 2,
                "rank": 77
            },
            {
                "bandwidth": null,
                "category": {
                    "deprecated": false,
                    "id": 139,
                    "integration": false,
                    "label": "Web Hosting",
                    "type": "content"
                },
                "count": 2,
                "rank": 78
            },
            {
                "bandwidth": null,
                "category": {
                    "deprecated": false,
                    "id": 137,
                    "integration": false,
                    "label": "Society and Culture",
                    "type": "content"
                },
                "count": 2,
                "rank": 79
            },
            {
                "bandwidth": null,
                "category": {
                    "deprecated": false,
                    "id": 200,
                    "integration": false,
                    "label": "Cryptocurrency",
                    "type": "content"
                },
                "count": 1,
                "rank": 80
            },
            {
                "bandwidth": null,
                "category": {
                    "deprecated": false,
                    "id": 195,
                    "integration": false,
                    "label": "Transportation",
                    "type": "content"
                },
                "count": 1,
                "rank": 81
            },
            {
                "bandwidth": null,
                "category": {
                    "deprecated": false,
                    "id": 187,
                    "integration": false,
                    "label": "Photo Search and Images",
                    "type": "content"
                },
                "count": 1,
                "rank": 82
            },
            {
                "bandwidth": null,
                "category": {
                    "deprecated": true,
                    "id": 48,
                    "integration": false,
                    "label": "Automotive",
                    "type": "content"
                },
                "count": 1,
                "rank": 83
            }
        ]
    }
}
```

#### Human Readable Output

>### Category List
>|Category|Type|Activity|
>|---|---|---|
>| Application | application | 14082 |
>| Business Services | content | 8930 |
>| Software/Technology | content | 8618 |
>| Infrastructure and Content Delivery Networks | content | 7297 |
>| Business and Industry | content | 5736 |
>| Computers and Internet | content | 5686 |
>| Search Engines | content | 4015 |
>| Search Engines and Portals | content | 2763 |
>| Advertisements | content | 2255 |
>| Online Meetings | content | 1314 |
>| Chat | content | 1302 |
>| Instant Messaging | content | 1276 |
>| Online Document Sharing and Collaboration | content | 1089 |
>| Computer Security | content | 1059 |
>| Video Sharing | content | 1053 |
>| Streaming Video | content | 984 |
>| Webmail | content | 878 |
>| Chat and Instant Messaging | content | 868 |
>| Web-based Email | content | 864 |
>| Organizational Email | content | 858 |
>| Cloud and Data Centers | content | 683 |
>| Social Networking | content | 630 |
>| SaaS and B2B | content | 525 |
>| Ecommerce/Shopping | content | 498 |
>| Movies | content | 355 |
>| News/Media | content | 353 |
>| Internet Telephony | content | 340 |
>| Research/Reference | content | 256 |
>| Portals | content | 252 |
>| Software Updates | content | 249 |
>| File Storage | content | 196 |
>| Blogs | content | 184 |
>| Reference | content | 184 |
>| Real Estate | content | 161 |
>| Non-Profits | content | 138 |
>| Shopping | content | 133 |
>| URL Shorteners | content | 116 |
>| News | content | 101 |
>| Professional Networking | content | 74 |
>| Photo Sharing | content | 63 |
>| Jobs/Employment | content | 44 |
>| Entertainment | content | 36 |
>| Government and Law | content | 35 |
>| Government | content | 35 |
>| Travel | content | 31 |
>| Forums/Message boards | content | 29 |
>| Online Communities | content | 27 |
>| Illegal Downloads | content | 21 |
>| Online Trading | content | 21 |
>| Job Search | content | 20 |
>| Financial Institutions | content | 20 |
>| Block List | customer | 19 |
>| Science and Technology | content | 18 |
>| Online Storage and Backup | content | 18 |
>| Education | content | 16 |
>| Educational Institutions | content | 16 |
>| Television | content | 15 |
>| Streaming Audio | content | 14 |
>| Finance | content | 10 |
>| Classifieds | content | 9 |
>| Mobile Phones | content | 8 |
>| Not Actionable | content | 8 |
>| Health and Medicine | content | 7 |
>| Games | content | 5 |
>| Internet of Things | content | 5 |
>| Sports and Recreation | content | 5 |
>| Sports | content | 5 |
>| Music | content | 4 |
>| Radio | content | 4 |
>| Gambling | content | 3 |
>| Web Page Translation | content | 3 |
>| Dining and Drinking | content | 2 |
>| Non-governmental Organizations | content | 2 |
>| DoH and DoT | content | 2 |
>| Visual Search Engines | content | 2 |
>| Proxy/Anonymizer | content | 2 |
>| Fashion | content | 2 |
>| Web Hosting | content | 2 |
>| Society and Culture | content | 2 |
>| Cryptocurrency | content | 1 |
>| Transportation | content | 1 |
>| Photo Search and Images | content | 1 |
>| Automotive | content | 1 |


### umbrella-reporting-identity-list
***
List of identities ordered by the number of requests made matching the categories in descending order.


#### Base Command

`umbrella-reporting-identity-list`
#### Input

| **Argument Name** | **Description** | **Required** |
| --- | --- | --- |
| traffic_type | Specify the type of traffic. Valid values: dns, proxy, firewall or ip. By default value will be all i.e. dns, proxy, firewall and ip. Possible values are: dns, proxy, firewall, ip. | Optional | 
| from | A timestamp (milliseconds) or relative time string (for example:-1days' or '1639146300000'). Filter for data that appears after this time. By default value is -7days. | Optional | 
| to | A timestamp (milliseconds) or relative time string (for example:'now' or 1661510185000). Filter for data that appears before this time. By default value is 'now'. | Optional | 
| limit | The maximum number of records to return from the collection. Default value of limit is 50. | Optional | 
| domains | A domain name or comma-delimited list of domain name. | Optional | 
| urls | A URL or comma-delimited list of URL. | Optional | 
| ip | An IP address. | Optional | 
| ports | A port number or comma-delimited list of port number. | Optional | 
| verdict | A verdict string. Possible values are: allowed, blocked, proxied. | Optional | 
| sha256 | A SHA-256 hash. | Optional | 
| threats | A threat name or comma-delimited list of threat name. | Optional | 
| threat_types | A threat type or comma-delimited list of threat type. | Optional | 
| amp_disposition | An AMP disposition string. Possible values are: clean, malicious, unknown. | Optional | 
| identity_types | An identity type or comma-delimited list of identity type. | Optional | 
| page | The page number. Default Page number is 1. | Optional | 
| page_size | The number of requested results per page. | Optional | 


#### Context Output

| **Path** | **Type** | **Description** |
| --- | --- | --- |
| UmbrellaReporting.Identity.requests | Number | Total number of requests made by this identity | 
| UmbrellaReporting.Identity.bandwidth | Number | Bandwidth | 
| UmbrellaReporting.Identity.rank | Number | The rank of the result based on the number of requests | 
| UmbrellaReporting.Identity.counts.allowedrequests | Number | Number of requests that were allowed | 
| UmbrellaReporting.Identity.counts.blockedrequests | Number | Number of requests that were blocked | 
| UmbrellaReporting.Identity.counts.requests | Number | Total number of requests | 
| UmbrellaReporting.Identity.identity.id | Number | ID of identity. | 
| UmbrellaReporting.Identity.identity.type.id | Number | Origin type for identity | 
| UmbrellaReporting.Identity.identity.type.type | String | Origin type name for identity | 
| UmbrellaReporting.Identity.identity.type.label | String | Origin type label for identity | 
| UmbrellaReporting.Identity.identity.label | String | Label for identity | 
| UmbrellaReporting.Identity.identity.deleted | Boolean | Indicates whether the identity was deleted or not | 

#### Command example
```!umbrella-reporting-identity-list limit=2```
#### Context Example
```json
{
    "UmbrellaReporting": {
        "Identity": [
            {
                "bandwidth": 1236885730,
                "counts": {
                    "allowedrequests": 21329,
                    "blockedrequests": 19,
                    "requests": 21432
                },
                "identity": {
                    "deleted": false,
                    "id": 589064228,
                    "label": "DESKTOP-IIQVPJ7",
                    "type": {
                        "id": 9,
                        "label": "Roaming Computers",
                        "type": "roaming"
                    }
                },
                "rank": 1,
                "requests": 21432
            }
        ]
    }
}
```

#### Human Readable Output

>### Identities List
>|Identity|Requests|
>|---|---|
>| DESKTOP-IIQVPJ7 | 21432 |


### umbrella-reporting-event-type-list
***
List of event types ordered by the number of requests made for each type of event in descending order. The event types are: domain_security, domain_integration, url_security, url_integration, cisco_amp and antivirus.


#### Base Command

`umbrella-reporting-event-type-list`
#### Input

| **Argument Name** | **Description** | **Required** |
| --- | --- | --- |
| from | A timestamp (milliseconds) or relative time string (for example:-1days' or '1639146300000'). Filter for data that appears after this time. By default value is -7days. | Optional | 
| to | A timestamp (milliseconds) or relative time string (for example:'now' or 1661510185000). Filter for data that appears before this time. By default value is 'now'. | Optional | 
| domains | A domain name or comma-delimited list of domain name. | Optional | 
| urls | A URL or comma-delimited list of URL. | Optional | 
| ip | An IP address. | Optional | 
| identity_types | An identity type or comma-delimited list of identity type. | Optional | 
| verdict | A verdict string. Possible values are: allowed, blocked, proxied. | Optional | 
| threats | A threat name or comma-delimited list of threat name. | Optional | 
| threat_types | A threat type or comma-delimited list of threat type. | Optional | 
| amp_disposition | An AMP disposition string. Possible values are: clean, malicious, unknown. | Optional | 
| page | The page number. Default Page number is 1. | Optional | 
| page_size | The number of requested results per page. | Optional | 


#### Context Output

| **Path** | **Type** | **Description** |
| --- | --- | --- |
| UmbrellaReporting.Eventtype.eventtype | String | The eventtype. One of "domain_security", "domain_integration", "url_security", "url_integration", "cisco_amp" and "antivirus". | 
| UmbrellaReporting.Eventtype.count | Number | Number of requests made that match this eventtype. | 

#### Command example
```!umbrella-reporting-event-type-list```
#### Context Example
```json
{
    "UmbrellaReporting": {
        "TopEventType": [
            {
                "count": 0,
                "eventtype": "url_integration"
            },
            {
                "count": 0,
                "eventtype": "url_security"
            },
            {
                "count": 0,
                "eventtype": "antivirus"
            },
            {
                "count": 0,
                "eventtype": "application"
            },
            {
                "count": 0,
                "eventtype": "cisco_amp"
            },
            {
                "count": 0,
                "eventtype": "domain_integration"
            },
            {
                "count": 0,
                "eventtype": "domain_security"
            }
        ]
    }
}
```

#### Human Readable Output

>### Event Type List
>|Event Type|Count|
>|---|---|
>| url_integration | 0 |
>| url_security | 0 |
>| antivirus | 0 |
>| application | 0 |
>| cisco_amp | 0 |
>| domain_integration | 0 |
>| domain_security | 0 |


### umbrella-reporting-file-list
***
List of files within a timeframe. Only returns proxy data.


#### Base Command

`umbrella-reporting-file-list`
#### Input

| **Argument Name** | **Description** | **Required** |
| --- | --- | --- |
| from | A timestamp (milliseconds) or relative time string (for example:-1days' or '1639146300000'). Filter for data that appears after this time. By default value is -7days. | Optional | 
| to | A timestamp (milliseconds) or relative time string (for example:'now' or 1661510185000). Filter for data that appears before this time. By default value is 'now'. | Optional | 
| limit | The maximum number of records to return from the collection. Default value of limit is 50. | Optional | 
| domains | A domain name or comma-delimited list of domain name. | Optional | 
| urls | A URL or comma-delimited list of URL. | Optional | 
| ip | An IP address. | Optional | 
| verdict | A verdict string. Possible values are: allowed, blocked, proxied. | Optional | 
| sha256 | A SHA-256 hash. | Optional | 
| amp_disposition | An AMP disposition string. Possible values are: clean, malicious, unknown. | Optional | 
| identity_types | An identity type or comma-delimited list of identity type. | Optional | 
| page | The page number. Default Page number is 1. | Optional | 
| page_size | The number of requested results per page. | Optional | 


#### Context Output

| **Path** | **Type** | **Description** |
| --- | --- | --- |
| UmbrellaReporting.File.requests | Number | Number of requests. | 
| UmbrellaReporting.File.identitycount | Number | count of identities for entry | 
| UmbrellaReporting.File.sha256 | String | Sha256 for entry | 
| UmbrellaReporting.File.filenames | Unknown | array of filenames for entry | 
| UmbrellaReporting.File.filetypes | Unknown | array of filetypes for entry | 
| UmbrellaReporting.File.categories.id | Number | id of category | 
| UmbrellaReporting.File.categories.label | String | The human readable label of the category | 
| UmbrellaReporting.File.categories.type | String | The type of category | 
| UmbrellaReporting.File.categories.deprecated | Boolean | If the category is a legacy category | 
| UmbrellaReporting.File.categories.integration | Boolean | If the category is an integration | 

#### Command example
```!umbrella-reporting-file-list limit=2```
#### Context Example
```json
{
    "UmbrellaReporting": {
        "File": [
            {
                "categories": [
                    {
                        "deprecated": false,
                        "id": 167,
                        "integration": false,
                        "label": "Computers and Internet",
                        "type": "content"
                    },
                    {
                        "deprecated": true,
                        "id": 25,
                        "integration": false,
                        "label": "Software/Technology",
                        "type": "content"
                    },
                    {
                        "deprecated": true,
                        "id": 32,
                        "integration": false,
                        "label": "Business Services",
                        "type": "content"
                    }
                ],
                "filenames": [
                    "Nested_ESXi6.5d_Appliance_Template_v1.0.ova"
                ],
                "filetypes": [],
                "identitycount": 1,
                "requests": 2,
                "sha256": "4c5f650943b0ae6ae2c9864f3bf682578a86859be921ddbc1a596b3404c0b678"
            },
            {
                "categories": [
                    {
                        "deprecated": false,
                        "id": 113,
                        "integration": false,
                        "label": "Computer Security",
                        "type": "content"
                    },
                    {
                        "deprecated": true,
                        "id": 25,
                        "integration": false,
                        "label": "Software/Technology",
                        "type": "content"
                    }
                ],
                "filenames": [
                    "MFEwTzBNMEswSTAJBgUrDgMCGgUABBTIyCPRUzvKHRw7iRE1lF%2BfcLu%2FjgQUypJnUmHervy6Iit%2FHIdMJftvmVgCEANCxxGUAknZpbqre7qsi5Q%3D"
                ],
                "filetypes": [],
                "identitycount": 1,
                "requests": 1,
                "sha256": "8dd46f416f5d1ebfc56ca9a32db3354c895acb5c1be275143d716316f1ff540a"
            }
        ]
    }
}
```

#### Human Readable Output

>### File List
>|Requests|Identity Count|SHA256|Category|Category Type|File Name|
>|---|---|---|---|---|---|
>| 2 | 1 | 4c5f650943b0ae6ae2c9864f3bf682578a86859be921ddbc1a596b3404c0b678 | Computers and Internet,Software/Technology,Business Services | content,content,content | Nested_ESXi6.5d_Appliance_Template_v1.0.ova |
>| 1 | 1 | 8dd46f416f5d1ebfc56ca9a32db3354c895acb5c1be275143d716316f1ff540a | Computer Security,Software/Technology | content,content | MFEwTzBNMEswSTAJBgUrDgMCGgUABBTIyCPRUzvKHRw7iRE1lF%2BfcLu%2FjgQUypJnUmHervy6Iit%2FHIdMJftvmVgCEANCxxGUAknZpbqre7qsi5Q%3D |


### umbrella-reporting-threat-list
***
List of top threats within a timeframe. Returns both DNS and Proxy data.


#### Base Command

`umbrella-reporting-threat-list`
#### Input

| **Argument Name** | **Description** | **Required** |
| --- | --- | --- |
| traffic_type | Specify the type of traffic. Valid values: dns or proxy. By default value will be all i.e. dns and proxy. Possible values are: dns, proxy. | Optional | 
| from | A timestamp (milliseconds) or relative time string (for example:-1days' or '1639146300000'). Filter for data that appears after this time. By default value is -7days. | Optional | 
| to | A timestamp (milliseconds) or relative time string (for example:'now' or 1661510185000). Filter for data that appears before this time. By default value is 'now'. | Optional | 
| limit | The maximum number of records to return from the collection. Default value of limit is 50. | Optional | 
| domains | A domain name or comma-delimited list of domain name. | Optional | 
| ip | An IP address. | Optional | 
| identity_types | An identity type or comma-delimited list of identity type. | Optional | 
| verdict | A verdict string. Possible values are: allowed, blocked, proxied. | Optional | 
| threats | A threat name or comma-delimited list of threat name. | Optional | 
| threat_types | A threat type or comma-delimited list of threat type. | Optional | 
| page | The page number. Default Page number is 1. | Optional | 
| page_size | The number of requested results per page. | Optional | 


#### Context Output

| **Path** | **Type** | **Description** |
| --- | --- | --- |
| UmbrellaReporting.Threats.threat | String | The threat name | 
| UmbrellaReporting.Threats.threattype | String | The threat type | 
| UmbrellaReporting.Threats.count | Number | The number of requests for that threat name | 

#### Command example
```!umbrella-reporting-threat-list limit=2```
#### Human Readable Output

>### Threat List
>**No entries.**


### umbrella-reporting-activity-list
***
List all activity entries (dns/proxy/firewall/ip/intrusion/amp) within timeframe.


#### Base Command

`umbrella-reporting-activity-list`
#### Input

| **Argument Name** | **Description** | **Required** |
| --- | --- | --- |
| from | A timestamp (milliseconds) or relative time string (for example:-1days' or '1639146300000'). Filter for data that appears after this time. By default value is -7days. | Optional | 
| to | A timestamp (milliseconds) or relative time string (for example:'now' or 1661510185000). Filter for data that appears before this time. By default value is 'now'. | Optional | 
| limit | The maximum number of records to return from the collection. Default value of limit is 50. | Optional | 
| domains | A domain name or comma-delimited list of domain name. | Optional | 
| urls | A URL or comma-delimited list of URL. | Optional | 
| ip | An IP address. | Optional | 
| ports | A port number or comma-delimited list of port number. | Optional | 
| identity_types | An identity type or comma-delimited list of identity type. | Optional | 
| verdict | A verdict string. Possible values are: allowed, blocked, proxied. | Optional | 
| file_name | A string that identifies a filename. Filter request by the filename. Supports globbing or use of the wildcard character (''). The asterisk (*) matches zero or more occurrences of any character. | Optional | 
| threats | A threat name or comma-delimited list of threat name. | Optional | 
| threat_types | A threat type or comma-delimited list of threat type. | Optional | 
| amp_disposition | An AMP disposition string. Possible values are: clean, malicious, unknown. | Optional | 
| page | The page number. Default Page number is 1. | Optional | 
| page_size | The number of requested results per page. | Optional | 


#### Context Output

| **Path** | **Type** | **Description** |
| --- | --- | --- |
| UmbrellaReporting.Activity.type | String | External IP for entry. | 
| UmbrellaReporting.Activity.externalip | String | External IP for entry. | 
| UmbrellaReporting.Activity.internalip | String | Internal IP for entry. | 
| UmbrellaReporting.Activity.policycategories.id | Number | ID of category. | 
| UmbrellaReporting.Activity.policycategories.label | String | The human readable label of the category. | 
| UmbrellaReporting.Activity.policycategories.type | String | Type of the request. a dns request always has type dns. | 
| UmbrellaReporting.Activity.policycategories.deprecated | Boolean | If the category is a legacy category. | 
| UmbrellaReporting.Activity.policycategories.integration | Boolean | If the category is an integration. | 
| UmbrellaReporting.Activity.categories.id | Number | id of category | 
| UmbrellaReporting.Activity.categories.label | String | The human readable label of the category | 
| UmbrellaReporting.Activity.categories.type | String | The type of category | 
| UmbrellaReporting.Activity.categories.deprecated | Boolean | If the category is a legacy category | 
| UmbrellaReporting.Activity.categories.integration | Boolean | If the category is an integration | 
| UmbrellaReporting.Activity.verdict | String | Verdict for entry. | 
| UmbrellaReporting.Activity.domain | String | Domain for entry. | 
| UmbrellaReporting.Activity.timestamp | String | Timestamp in ms. | 
| UmbrellaReporting.Activity.time | String | The time in 24 hour format based on the timezone parameter. | 
| UmbrellaReporting.Activity.date | String | The date from the timestamp based on the timezone parameter. | 
| UmbrellaReporting.Activity.identities.id | Number | ID of identity. | 
| UmbrellaReporting.Activity.identities.type.id | Number | Origin type for identity | 
| UmbrellaReporting.Activity.identities.type.type | String | Origin type name for identity | 
| UmbrellaReporting.Activity.identities.type.label | String | Origin type label for identity | 
| UmbrellaReporting.Activity.identities.label | String | Label for identity | 
| UmbrellaReporting.Activity.identities.deleted | Boolean | Indicates whether the identity was deleted or not | 
| UmbrellaReporting.Activity.threats.label | Boolean | The threat name or label. | 
| UmbrellaReporting.Activity.threats.type | String | The type of threat. | 
| UmbrellaReporting.Activity.allapplications.id | Number | ID of the application. | 
| UmbrellaReporting.Activity.allapplications.type | String | Type of the application, NBAR or AVC. | 
| UmbrellaReporting.Activity.allapplications.label | String | Label of the application. | 
| UmbrellaReporting.Activity.allapplications.category.label | String | Label of the application category. | 
| UmbrellaReporting.Activity.allapplications.category.id | Number | ID of the application category. | 
| UmbrellaReporting.Activity.allowedapplications.id | Number | ID of the application. | 
| UmbrellaReporting.Activity.allowedapplications.label | String | Label of the application. | 
| UmbrellaReporting.Activity.allowedapplications.type | String | Type of the application, NBAR or AVC. | 
| UmbrellaReporting.Activity.allowedapplications.category.label | String | Label of the application category. | 
| UmbrellaReporting.Activity.allowedapplications.category.id | String | ID of the application category. | 
| UmbrellaReporting.Activity.querytype | String | The type of DNS request that was made. For more information, see Common DNS Request Types. | 
| UmbrellaReporting.Activity.returncode | Number | The DNS return code for this request. For more information, see Common DNS return codes for any DNS service \(and Umbrella\). | 
| UmbrellaReporting.Activity.blockedapplications.id | Number | ID of the application. | 
| UmbrellaReporting.Activity.blockedapplications.label | String | Label of the application. | 
| UmbrellaReporting.Activity.blockedapplications.type | String | Type of the application, NBAR or AVC. | 
| UmbrellaReporting.Activity.blockedapplications.category.label | String | Label of the application category. | 
| UmbrellaReporting.Activity.blockedapplications.category.id | Number | ID of the application category. | 

#### Command example
```!umbrella-reporting-activity-list limit=2```
#### Context Example
```json
{
    "UmbrellaReporting": {
        "Activity": [
            {
                "allapplications": [
                    {
                        "category": {
                            "id": 7,
                            "label": "Collaboration"
                        },
                        "id": 986340,
                        "label": "Google Hangouts"
                    }
                ],
                "allowedapplications": [],
                "blockedapplications": [],
                "categories": [
                    {
                        "deprecated": true,
                        "id": 4,
                        "integration": false,
                        "label": "Chat",
                        "type": "content"
                    },
                    {
                        "deprecated": true,
                        "id": 15,
                        "integration": false,
                        "label": "Instant Messaging",
                        "type": "content"
                    },
                    {
                        "deprecated": true,
                        "id": 23,
                        "integration": false,
                        "label": "Search Engines",
                        "type": "content"
                    },
                    {
                        "deprecated": false,
                        "id": 123,
                        "integration": false,
                        "label": "Infrastructure and Content Delivery Networks",
                        "type": "content"
                    },
                    {
                        "deprecated": false,
                        "id": 148,
                        "integration": false,
                        "label": "Application",
                        "type": "application"
                    },
                    {
                        "deprecated": false,
                        "id": 190,
                        "integration": false,
                        "label": "Search Engines and Portals",
                        "type": "content"
                    }
                ],
                "date": "2022-09-16",
                "domain": "mtalk.google.com",
                "externalip": "117.195.206.238",
                "identities": [
                    {
                        "deleted": false,
                        "id": 589064228,
                        "label": "DESKTOP-IIQVPJ7",
                        "type": {
                            "id": 9,
                            "label": "Roaming Computers",
                            "type": "roaming"
                        }
                    }
                ],
                "internalip": "192.168.10.7",
                "policycategories": [],
                "querytype": "A",
                "returncode": 0,
                "threats": [],
                "time": "05:52:51",
                "timestamp": 1663307571000,
                "type": "dns",
                "verdict": "allowed"
            },
            {
                "allapplications": [],
                "allowedapplications": [],
                "blockedapplications": [],
                "categories": [
                    {
                        "deprecated": true,
                        "id": 25,
                        "integration": false,
                        "label": "Software/Technology",
                        "type": "content"
                    },
                    {
                        "deprecated": true,
                        "id": 32,
                        "integration": false,
                        "label": "Business Services",
                        "type": "content"
                    },
                    {
                        "deprecated": false,
                        "id": 113,
                        "integration": false,
                        "label": "Computer Security",
                        "type": "content"
                    },
                    {
                        "deprecated": false,
                        "id": 198,
                        "integration": false,
                        "label": "Cloud and Data Centers",
                        "type": "content"
                    }
                ],
                "date": "2022-09-16",
                "domain": "loginsoft.cmdm.comodo.com",
                "externalip": "117.195.206.238",
                "identities": [
                    {
                        "deleted": false,
                        "id": 589064228,
                        "label": "DESKTOP-IIQVPJ7",
                        "type": {
                            "id": 9,
                            "label": "Roaming Computers",
                            "type": "roaming"
                        }
                    }
                ],
                "internalip": "192.168.10.7",
                "policycategories": [],
                "querytype": "A",
                "returncode": 0,
                "threats": [],
                "time": "05:51:39",
                "timestamp": 1663307499000,
                "type": "dns",
                "verdict": "allowed"
            }
        ]
    }
}
```

#### Human Readable Output

>### Activity List
>|Request|Identity|Policy or Ruleset Identity|Destination|Internal IP|External IP|DNS Type|Action|Categories|Public Application|Application Category|Date & Time|
>|---|---|---|---|---|---|---|---|---|---|---|---|
>| dns | DESKTOP-IIQVPJ7 | DESKTOP-IIQVPJ7 | mtalk.google.com | 192.168.10.7 | 117.195.206.238 | A | allowed | Chat,Instant Messaging,Search Engines,Infrastructure and Content Delivery Networks,Application,Search Engines and Portals | Google Hangouts | Collaboration | Sep 16, 2022 05:52 AM |
>| dns | DESKTOP-IIQVPJ7 | DESKTOP-IIQVPJ7 | loginsoft.cmdm.comodo.com | 192.168.10.7 | 117.195.206.238 | A | allowed | Software/Technology,Business Services,Computer Security,Cloud and Data Centers |  |  | Sep 16, 2022 05:51 AM |


### umbrella-reporting-activity-get
***
List all entries within a timeframe based on the traffic type selected. Valid activity types are dns, proxy, firewall, intrusion, ip, amp.
Only one activity type can be selected at a time.


#### Base Command

`umbrella-reporting-activity-get`
#### Input

| **Argument Name** | **Description** | **Required** |
| --- | --- | --- |
| traffic_type | Specify the type of traffic. Valid values are: dns, proxy, firewall, intrusion, ip, amp.<br/><br/>Supported optional parameter for DNS traffic type are limit, from,  to, offset, domains, ip, verdict, threats, threat_types.<br/> Supported optional parameter for Proxy traffic type are limit, from, to, offset, domains, ip, verdict, threats, threat_types, urls, ports, identity_types, file_name, amp_disposition.<br/> Supported optional parameter for Firewall traffic type are limit, from, to, offset, ip, ports, verdict.<br/> Supported optional parameter for Intrusion traffic type are limit, from, to, offset, ip, ports, signatures, intrusion_action.<br/> Supported optional parameter for IP traffic type are limit, from, to, offset, ip, ports, identity_types, verdict.<br/> Supported optional parameter for AMP traffic type are limit, from, to, offset, amp_disposition, sha256. Possible values are: dns, proxy, firewall, intrusion, ip, amp. | Required | 
| from | A timestamp (milliseconds) or relative time string (for example:-1days' or '1639146300000'). Filter for data that appears after this time. By default value is -7days. | Optional | 
| to | A timestamp (milliseconds) or relative time string (for example:'now' or 1661510185000). Filter for data that appears before this time. By default value is 'now'. | Optional | 
| limit | The maximum number of records to return from the collection. Default value of limit is 50. | Optional | 
| domains | A domain name or comma-delimited list of domain name. | Optional | 
| urls | A URL or comma-delimited list of URL. | Optional | 
| ip | An IP address. | Optional | 
| ports | A port number or comma-delimited list of port number. | Optional | 
| identity_types | An identity type or comma-delimited list of identity type. | Optional | 
| verdict | A verdict string. Possible values are: allowed, blocked, proxied. | Optional | 
| file_name | A string that identifies a filename. Filter request by the filename. Supports globbing or use of the wildcard character (''). The asterisk (*) matches zero or more occurrences of any character. | Optional | 
| threats | A threat name or comma-delimited list of threat name. | Optional | 
| threat_types | A threat type or comma-delimited list of threat type. | Optional | 
| amp_disposition | An AMP disposition string. Possible values are: clean, malicious, unknown. | Optional | 
| page | The page number. Default Page number is 1. | Optional | 
| page_size | The number of requested results per page. | Optional | 
| signatures | List of -, comma delimited. | Optional | 
| intrusion_action | List of intrusion actions, comma delimited. possible values: would_block, blocked, detected. | Optional | 


#### Context Output of DNS

| **Path** | **Type** | **Description** |
| --- | --- | --- |
| UmbrellaReporting.ActivityDns.type | String | External IP for entry. | 
| UmbrellaReporting.ActivityDns.externalip | String | External IP for entry. | 
| UmbrellaReporting.ActivityDns.internalip | String | Internal IP for entry. | 
| UmbrellaReporting.ActivityDns.policycategories.id | Number | ID of category. | 
| UmbrellaReporting.ActivityDns.policycategories.label | String | The human readable label of the category. | 
| UmbrellaReporting.ActivityDns.policycategories.type | String | Type of the request. a dns request always has type dns. | 
| UmbrellaReporting.ActivityDns.policycategories.deprecated | Boolean | If the category is a legacy category. | 
| UmbrellaReporting.ActivityDns.policycategories.integration | Boolean | If the category is an integration. | 
| UmbrellaReporting.ActivityDns.categories.id | Number | id of category | 
| UmbrellaReporting.ActivityDns.categories.label | String | The human readable label of the category | 
| UmbrellaReporting.ActivityDns.categories.type | String | The type of category | 
| UmbrellaReporting.ActivityDns.categories.deprecated | Boolean | If the category is a legacy category | 
| UmbrellaReporting.ActivityDns.categories.integration | Boolean | If the category is an integration | 
| UmbrellaReporting.ActivityDns.verdict | String | Verdict for entry. | 
| UmbrellaReporting.ActivityDns.domain | String | Domain for entry. | 
| UmbrellaReporting.ActivityDns.timestamp | String | Timestamp in ms. | 
| UmbrellaReporting.ActivityDns.time | String | The time in 24 hour format based on the timezone parameter. | 
| UmbrellaReporting.ActivityDns.date | String | The date from the timestamp based on the timezone parameter. | 
| UmbrellaReporting.ActivityDns.identities.id | Number | ID of identity. | 
| UmbrellaReporting.ActivityDns.identities.type.id | Number | Origin type for identity | 
| UmbrellaReporting.ActivityDns.identities.type.type | String | Origin type name for identity | 
| UmbrellaReporting.ActivityDns.identities.type.label | String | Origin type label for identity | 
| UmbrellaReporting.ActivityDns.identities.label | String | Label for identity | 
| UmbrellaReporting.ActivityDns.identities.deleted | Boolean | Indicates whether the identity was deleted or not | 
| UmbrellaReporting.ActivityDns.threats.label | Boolean | The threat name or label. | 
| UmbrellaReporting.ActivityDns.threats.type | String | The type of threat. | 
| UmbrellaReporting.ActivityDns.allapplications.id | Number | ID of the application. | 
| UmbrellaReporting.ActivityDns.allapplications.type | String | Type of the application, NBAR or AVC. | 
| UmbrellaReporting.ActivityDns.allapplications.label | String | Label of the application. | 
| UmbrellaReporting.ActivityDns.allapplications.category.label | String | Label of the application category. | 
| UmbrellaReporting.ActivityDns.allapplications.category.id | Number | ID of the application category. | 
| UmbrellaReporting.ActivityDns.allowedapplications.id | Number | ID of the application. | 
| UmbrellaReporting.ActivityDns.allowedapplications.label | String | Label of the application. | 
| UmbrellaReporting.ActivityDns.allowedapplications.type | String | Type of the application, NBAR or AVC. | 
| UmbrellaReporting.ActivityDns.allowedapplications.category.label | String | Label of the application category. | 
| UmbrellaReporting.ActivityDns.allowedapplications.category.id | String | ID of the application category. | 
| UmbrellaReporting.ActivityDns.querytype | String | The type of DNS request that was made. For more information, see Common DNS Request Types. | 
| UmbrellaReporting.ActivityDns.returncode | Number | The DNS return code for this request. For more information, see Common DNS return codes for any DNS service \(and Umbrella\). | 
| UmbrellaReporting.ActivityDns.blockedapplications.id | Number | ID of the application. | 
| UmbrellaReporting.ActivityDns.blockedapplications.label | String | Label of the application. | 
| UmbrellaReporting.ActivityDns.blockedapplications.type | String | Type of the application, NBAR or AVC. | 
| UmbrellaReporting.ActivityDns.blockedapplications.category.label | String | Label of the application category. | 
| UmbrellaReporting.ActivityDns.blockedapplications.category.id | Unknown | ID of the application category. | 

#### Command example of dns
```!umbrella-reporting-activity-get traffic_type=dns limit=2```
#### Context Example of dns
```json
{
    "UmbrellaReporting": {
        "ActivityDns": [
            {
                "allapplications": [
                    {
                        "category": {
                            "id": 7,
                            "label": "Collaboration"
                        },
                        "id": 986340,
                        "label": "Google Hangouts"
                    }
                ],
                "allowedapplications": [],
                "blockedapplications": [],
                "categories": [
                    {
                        "deprecated": true,
                        "id": 4,
                        "integration": false,
                        "label": "Chat",
                        "type": "content"
                    },
                    {
                        "deprecated": true,
                        "id": 15,
                        "integration": false,
                        "label": "Instant Messaging",
                        "type": "content"
                    },
                    {
                        "deprecated": true,
                        "id": 23,
                        "integration": false,
                        "label": "Search Engines",
                        "type": "content"
                    },
                    {
                        "deprecated": false,
                        "id": 123,
                        "integration": false,
                        "label": "Infrastructure and Content Delivery Networks",
                        "type": "content"
                    },
                    {
                        "deprecated": false,
                        "id": 148,
                        "integration": false,
                        "label": "Application",
                        "type": "application"
                    },
                    {
                        "deprecated": false,
                        "id": 190,
                        "integration": false,
                        "label": "Search Engines and Portals",
                        "type": "content"
                    }
                ],
                "date": "2022-09-16",
                "domain": "mtalk.google.com",
                "externalip": "117.195.206.238",
                "identities": [
                    {
                        "deleted": false,
                        "id": 589064228,
                        "label": "DESKTOP-IIQVPJ7",
                        "type": {
                            "id": 9,
                            "label": "Roaming Computers",
                            "type": "roaming"
                        }
                    }
                ],
                "internalip": "192.168.10.7",
                "policycategories": [],
                "querytype": "A",
                "returncode": 0,
                "threats": [],
                "time": "05:52:51",
                "timestamp": 1663307571000,
                "type": "dns",
                "verdict": "allowed"
            },
            {
                "allapplications": [],
                "allowedapplications": [],
                "blockedapplications": [],
                "categories": [
                    {
                        "deprecated": true,
                        "id": 25,
                        "integration": false,
                        "label": "Software/Technology",
                        "type": "content"
                    },
                    {
                        "deprecated": true,
                        "id": 32,
                        "integration": false,
                        "label": "Business Services",
                        "type": "content"
                    },
                    {
                        "deprecated": false,
                        "id": 113,
                        "integration": false,
                        "label": "Computer Security",
                        "type": "content"
                    },
                    {
                        "deprecated": false,
                        "id": 198,
                        "integration": false,
                        "label": "Cloud and Data Centers",
                        "type": "content"
                    }
                ],
                "date": "2022-09-16",
                "domain": "loginsoft.cmdm.comodo.com",
                "externalip": "117.195.206.238",
                "identities": [
                    {
                        "deleted": false,
                        "id": 589064228,
                        "label": "DESKTOP-IIQVPJ7",
                        "type": {
                            "id": 9,
                            "label": "Roaming Computers",
                            "type": "roaming"
                        }
                    }
                ],
                "internalip": "192.168.10.7",
                "policycategories": [],
                "querytype": "A",
                "returncode": 0,
                "threats": [],
                "time": "05:51:39",
                "timestamp": 1663307499000,
                "type": "dns",
                "verdict": "allowed"
            }
        ]
    }
}
```

#### Human Readable Output

>### Dns Activity List
>|Identity|Policy or Ruleset Identity|Destination|Internal IP|External IP|DNS Type|Action|Categories|Public Application|Application Category|Date & Time|
>|---|---|---|---|---|---|---|---|---|---|---|
>| DESKTOP-IIQVPJ7 | DESKTOP-IIQVPJ7 | mtalk.google.com | 192.168.10.7 | 117.195.206.238 | A | allowed | Chat,Instant Messaging,Search Engines,Infrastructure and Content Delivery Networks,Application,Search Engines and Portals | Google Hangouts | Collaboration | Sep 16, 2022 05:52 AM |
>| DESKTOP-IIQVPJ7 | DESKTOP-IIQVPJ7 | loginsoft.cmdm.comodo.com | 192.168.10.7 | 117.195.206.238 | A | allowed | Software/Technology,Business Services,Computer Security,Cloud and Data Centers |  |  | Sep 16, 2022 05:51 AM |


#### Context Output of Proxy

| **Path**                                                         | **Type** | **Description** |
|------------------------------------------------------------------| --- | --- |
| UmbrellaReporting.ActivityProxy.type                             | String <br/>| External IP for entry. | 
| UmbrellaReporting.ActivityProxy.externalip                         | String | External IP for entry. | 
| UmbrellaReporting.ActivityProxy.blockedfiletype                         | String | locked file type for entry. | 
| UmbrellaReporting.ActivityProxy.contenttype                         | String | The type of web content, typically text/html. |
| UmbrellaReporting.ActivityProxy.forwardingmethod                         | String | The request method (GET, POST, HEAD, etc.) |
| UmbrellaReporting.ActivityProxy.internalip                         | String | Internal IP for entry. |
| UmbrellaReporting.ActivityProxy.referer                         | String | The referring domain or URL. |
| UmbrellaReporting.ActivityProxy.requestmethod                         | String | The HTTP request method that was made. |
| UmbrellaReporting.ActivityProxy.responsefilename                         | String | Response filename for entry. |
| UmbrellaReporting.ActivityProxy.sha256                         | String | The hex digest of the response content. |
| UmbrellaReporting.ActivityProxy.url                         | String | The URL requested. |
| UmbrellaReporting.ActivityProxy.useragent                         | String | The browser agent that made the request. |
| UmbrellaReporting.ActivityProxy.warnstatus                         | Boolean | Warn Status. |
| UmbrellaReporting.ActivityProxy.securityoverridden                         | Boolean | Security Overridden. |
| UmbrellaReporting.ActivityProxy.tenantcontrols                         | Boolean | If the request was part of a tenant control policy. |
| UmbrellaReporting.ActivityProxy.bundleid                     | Number | Bundleid. |
| UmbrellaReporting.ActivityProxy.port                     | Number | Request Port. |
| UmbrellaReporting.ActivityProxy.requestsize                     | Number | Request size in bytes. |
| UmbrellaReporting.ActivityProxy.responsesize                     | Number | Response size in bytes. |
| UmbrellaReporting.ActivityProxy.statuscode                     | Number | The HTTP status code; should always be 200 or 201. |
| UmbrellaReporting.ActivityProxy.policycategories.id                | Number | ID of category. | 
| UmbrellaReporting.ActivityProxy.policycategories.label             | String | The human readable label of the category. | 
| UmbrellaReporting.ActivityProxy.policycategories.type              | String | Type of the request. a dns request always has type dns. | 
| UmbrellaReporting.ActivityProxy.policycategories.deprecated        | Boolean | If the category is a legacy category. | 
| UmbrellaReporting.ActivityProxy.policycategories.integration       | Boolean | If the category is an integration. | 
| UmbrellaReporting.ActivityProxy.categories.id                      | Number | id of category | 
| UmbrellaReporting.ActivityProxy.categories.label                   | String | The human readable label of the category | 
| UmbrellaReporting.ActivityProxy.categories.type                    | String | The type of category | 
| UmbrellaReporting.ActivityProxy.categories.deprecated              | Boolean | If the category is a legacy category | 
| UmbrellaReporting.ActivityProxy.categories.integration             | Boolean | If the category is an integration | 
| UmbrellaReporting.ActivityProxy.antivirusthreats.others                     | String | Other antivirus threats. | 
| UmbrellaReporting.ActivityProxy.antivirusthreats.puas                   | String | Potentially unwanted applications. | 
| UmbrellaReporting.ActivityProxy.antivirusthreats.viruses                    | String | Viruses. |  
| UmbrellaReporting.ActivityProxy.verdict                            | String | Verdict for entry. | 
| UmbrellaReporting.ActivityProxy.timestamp                          | String | Timestamp in ms. | 
| UmbrellaReporting.ActivityProxy.time                               | String | The time in 24 hour format based on the timezone parameter. | 
| UmbrellaReporting.ActivityProxy.date                               | String | The date from the timestamp based on the timezone parameter. | 
| UmbrellaReporting.ActivityProxy.identities.id                      | Number | ID of identity. | 
| UmbrellaReporting.ActivityProxy.identities.type.id                 | Number | Origin type for identity | 
| UmbrellaReporting.ActivityProxy.identities.type.type               | String | Origin type name for identity | 
| UmbrellaReporting.ActivityProxy.identities.type.label              | String | Origin type label for identity | 
| UmbrellaReporting.ActivityProxy.identities.label                   | String | Label for identity | 
| UmbrellaReporting.ActivityProxy.identities.deleted                 | Boolean | Indicates whether the identity was deleted or not | 
| UmbrellaReporting.ActivityProxy.threats.label                      | Boolean | The threat name or label. | 
| UmbrellaReporting.ActivityProxy.threats.type                       | String | The type of threat. | 
| UmbrellaReporting.ActivityProxy.datacenter.id             | String | Unique ID for the data center. | 
| UmbrellaReporting.ActivityProxy.datacenter.label          | String | Name of the data center. | 
| UmbrellaReporting.ActivityProxy.datalossprevention.state          | String | If the request was Blocked for DLP. Either 'blocked' or ''. |
| UmbrellaReporting.ActivityProxy.egress.ip             | String | Egress IP. | 
| UmbrellaReporting.ActivityProxy.egress.type          | String | Egress Type. |
| UmbrellaReporting.ActivityProxy.isolated.fileaction             | String | Isolated Fileaction | 
| UmbrellaReporting.ActivityProxy.isolated.state          | String | Isolated State. |
| UmbrellaReporting.ActivityProxy.allapplications.id                 | Number | ID of the application. | 
| UmbrellaReporting.ActivityProxy.allapplications.type               | String | Type of the application, NBAR or AVC. | 
| UmbrellaReporting.ActivityProxy.allapplications.label              | String | Label of the application. | 
| UmbrellaReporting.ActivityProxy.allapplications.category.label     | String | Label of the application category. | 
| UmbrellaReporting.ActivityProxy.allapplications.category.id        | Number | ID of the application category. | 
| UmbrellaReporting.ActivityProxy.allowedapplications.id             | Number | ID of the application. | 
| UmbrellaReporting.ActivityProxy.allowedapplications.label          | String | Label of the application. | 
| UmbrellaReporting.ActivityProxy.allowedapplications.type           | String | Type of the application, NBAR or AVC. | 
| UmbrellaReporting.ActivityProxy.allowedapplications.category.label | String | Label of the application category. | 
| UmbrellaReporting.ActivityProxy.allowedapplications.category.id    | String | ID of the application category. | 
| UmbrellaReporting.ActivityProxy.blockedapplications.id             | Number | ID of the application. | 
| UmbrellaReporting.ActivityProxy.blockedapplications.label          | String | Label of the application. | 
| UmbrellaReporting.ActivityProxy.blockedapplications.type           | String | Type of the application, NBAR or AVC. | 
| UmbrellaReporting.ActivityProxy.blockedapplications.category.label | String | Label of the application category. | 
| UmbrellaReporting.ActivityProxy.policy.timebasedrule                | Boolean | Whether the policy triggered a time-of-day rule. | 
| UmbrellaReporting.ActivityProxy.policy.ruleid               | Number | The rule ID for the policy. | 
| UmbrellaReporting.ActivityProxy.policy.rulesetid           | Number | The rule set ID for the policy. |  
| UmbrellaReporting.ActivityProxy.policy.destinationlistids                 | String | The destination lists that the policy triggered. | 
| UmbrellaReporting.ActivityProxy.httperrors.reason                | Boolean | The name of the error. | 
| UmbrellaReporting.ActivityProxy.httperrors.type               | Number | Type of the error CertificateError or TLSError. | 
| UmbrellaReporting.ActivityProxy.httperrors.attributes           | Number | Map of additional information about the error. |  
| UmbrellaReporting.ActivityProxy.httperrors.code                 | String | The http error code. |


#### Command example of proxy
```!umbrella-reporting-activity-get traffic_type=proxy limit=2```

#### Context Example of proxy
```json
{
   "UmbrellaReporting":{
      "ActivityProxy":[
         {
            "destinationip":"",
            "externalip":"32.4.91.7",
            "responsesize":3329530,
            "allapplications":[
               {
                  "id":1313,
                  "label":"Netflix",
                  "category":{
                     "id":47,
                     "label":"Media"
                  }
               }
            ],
            "date":"2022-02-18",
            "datalossprevention":{
               "state":""
            },
            "antivirusthreats":{
               "puas":[
                  
               ],
               "viruses":[
                  
               ],
               "others":[
                  
               ]
            },
            "internalip":"192.168.1.43",
            "referer":"",
            "contenttype":"",
            "tenantcontrols":false,
            "securityoverridden":false,
            "useragent":"",
            "time":"23:29:42",
            "amp":{
               "disposition":"",
               "score":0,
               "malware":""
            },
            "policycategories":[
               
            ],
            "type":"proxy",
            "requestsize":1996,
            "port":443,
            "policy":{
               "ruleid":0,
               "rulesetid":0,
               "destinationlistids":[
                  
               ],
               "timebasedrule":false
            },
            "forwardingmethod":"",
            "categories":[
               {
                  "id":17,
                  "type":"content",
                  "label":"Movies",
                  "integration":false,
                  "deprecated":true
               }
            ],
            "isolated":{
               "state":"not-isolated",
               "fileaction":""
            },
            "statuscode":200,
            "egress":{
               "ip":"155.190.3.8",
               "type":"shared"
            },
            "blockedfiletype":"",
            "url":"https://ipv4-lax2-ix.1.oca.anothervideo.net",
            "verdict":"allowed",
            "responsefilename":"",
            "warnstatus":"",
            "sha256":"",
            "timestamp":1645226982000,
            "blockedapplications":[
               
            ],
            "allowedapplications":[
               
            ],
            "identities":[
               {
                  "id":1,
                  "type":{
                     "id":34,
                     "type":"anyconnect",
                     "label":"Anyconnect Roaming Client"
                  },
                  "label":"Vincent's Macbook",
                  "deleted":false
               }
            ],
            "datacenter":{
               "label":"Los Angeles, US",
               "id":"LAX"
            },
            "threats":[
               
            ],
            "httperrors":[
               
            ],
            "bundleid":3
         }
      ]
   }
}
```
#### Human Readable Output

>### Proxy Activity List
>|Identity|Policy or Ruleset Identity|Internal IP|External IP|Action|Categories|Public Application| Application Category | URL |Date & Time|
>|---|---|---|---|---|---|----------------------|-----|---|---|
>| Vincent's Macbook | Vincent's Macbook |192.168.1.43 | 32.4.91.7 | allowed | Movies | Netflix | Media | https://ipv4-lax2-ix.1.oca.anothervideo.net    | Sep 16, 2022 05:52 AM |


#### Context Output of Firewall

| **Path**                                                         | **Type** | **Description** |
|------------------------------------------------------------------| --- |-----------|
| UmbrellaReporting.ActivityFirewall.type                             | String | External IP for entry. | 
| UmbrellaReporting.ActivityFirewall.destinationip                         | String | Destination IP for entry. |
| UmbrellaReporting.ActivityFirewall.direction                         | String | The direction of the packet. It is destined either towards the internet or to the customer's network. |
| UmbrellaReporting.ActivityFirewall.sourceip                         | String | Source IP |
| UmbrellaReporting.ActivityFirewall.destinationport                         | Number | Destination port for entry. |
| UmbrellaReporting.ActivityFirewall.sourceport                         | Number | Source port for entry. |
| UmbrellaReporting.ActivityFirewall.packetsize                         | Number | The size of the packet that Umbrella CDFW received. |
| UmbrellaReporting.ActivityFirewall.verdict                            | String | Verdict for entry. | 
| UmbrellaReporting.ActivityFirewall.timestamp                          | String | Timestamp in ms. | 
| UmbrellaReporting.ActivityFirewall.time                               | String | The time in 24 hour format based on the timezone parameter. | 
| UmbrellaReporting.ActivityFirewall.date                               | String | The date from the timestamp based on the timezone parameter. | 
| UmbrellaReporting.ActivityFirewall.identities.id                      | Number | ID of identity. | 
| UmbrellaReporting.ActivityFirewall.identities.type.id                 | Number | Origin type for identity | 
| UmbrellaReporting.ActivityFirewall.identities.type.type               | String | Origin type name for identity | 
| UmbrellaReporting.ActivityFirewall.identities.type.label              | String | Origin type label for identity | 
| UmbrellaReporting.ActivityFirewall.identities.label                   | String | Label for identity | 
| UmbrellaReporting.ActivityFirewall.identities.deleted                 | Boolean | Indicates whether the identity was deleted or not | 
| UmbrellaReporting.ActivityFirewall.protocol.label                      | String | Name of the protocol. | 
| UmbrellaReporting.ActivityFirewall.protocol.id                       | Number | ID of protocol. | 
| UmbrellaReporting.ActivityFirewall.allapplications.id                 | Number | ID of the application. | 
| UmbrellaReporting.ActivityFirewall.allapplications.app               | String | Type: "IT Service Management" (string) - application/protocol type. | 
| UmbrellaReporting.ActivityFirewall.allapplications.label              | String | Label of the application. | 
| UmbrellaReporting.ActivityFirewall.rule.label                 | String | Name of the rule | 
| UmbrellaReporting.ActivityFirewall.rule.id                      | String | ID of rule. | 
| UmbrellaReporting.ActivityFirewall.rule.privateapplicationgroup.label                       | String | Name of application group. | 
| UmbrellaReporting.ActivityFirewall.rule.privateapplicationgroup.id                 | Number | ID of application group | 
| UmbrellaReporting.ActivityFirewall.applicationprotocols.id                 | Number | ID of the application. | 
| UmbrellaReporting.ActivityFirewall.applicationprotocols.app               | String | Type: "IT Service Management" (string) - application/protocol type. | 
| UmbrellaReporting.ActivityFirewall.applicationprotocols.label              | String | Application/Protocol label. |


#### Command example of firewall
```!umbrella-reporting-activity-get traffic_type=firewall limit=1```

#### Context Example of firewall
```json
{
   "UmbrellaReporting":{
      "ActivityFirewall":[
        {
            "date": "2019",
            "destinationip": "52.8.160.247",
            "sourceip": "192.168.0.1",
            "sourceport": 0,
            "destinationport": 0,
            "verdict": "allowed",
            "time": "12:34",
            "timestamp": 1548311506,
            "identities": [
                {
                    "id": 1,
                    "label": "Catch Rate Testing System",
                    "type": {
                        "id": 21,
                        "label": "Sites",
                        "type": "site"
                    },
                    "deleted": false
                }
            ],
            "protocol": {
                "id": 17,
                "label": "UDP"
            },
            "rule": {
                "id": 1,
                "label": "Default Rule"
            },
            "type": "firewall",
            "allapplications": [
                {
                    "id": 72,
                    "label": "dns IT Service Management",
                    "app": ""
                }
            ],
            "applicationprotocols": [
                {
                    "id": 72,
                    "label": "dns IT Service Management",
                    "app": ""
                }
            ],
            "packetsize": 32,
            "direction": "towards"
        }
    ]
   }
}
```
#### Human Readable Output

>### Firewall Activity List
>|Identity|Policy or Ruleset Identity|Internal IP|Source IP|Source Port|Destination Port|Protocol|Rule|Type|Action|Public Application|Direction|Date & Time|
>|---|---|---|---|---|---|---|---|---|---|---|---|---|
>| Catch Rate Testing System | Catch Rate Testing System | 52.8.160.247 | 192.168.0.1 | 0 | 0 | UDP | Default Rule | firewall |allowed|dns IT Service Management|towards| Sep 16, 2022 05:52 AM |

#### Context Output of IP

| **Path**                                                         | **Type** | **Description** |
|------------------------------------------------------------------| --- |-----------|
| UmbrellaReporting.ActivityIP.type                             | String <br/>| External IP for entry. | 
| UmbrellaReporting.ActivityIP.destinationip                         | String | Destination IP for entry. |
| UmbrellaReporting.ActivityIP.sourceip                         | String | Source IP |
| UmbrellaReporting.ActivityIP.destinationport                         | Number | Destination port for entry. |
| UmbrellaReporting.ActivityIP.sourceport                         | Number | Source port for entry. |
| UmbrellaReporting.ActivityIP.verdict                            | String | Verdict for entry. | 
| UmbrellaReporting.ActivityIP.timestamp                          | String | Timestamp in ms. | 
| UmbrellaReporting.ActivityIP.time                               | String | The time in 24 hour format based on the timezone parameter. | 
| UmbrellaReporting.ActivityIP.date                               | String | The date from the timestamp based on the timezone parameter. | 
| UmbrellaReporting.ActivityIP.identities.id                      | Number | ID of identity. | 
| UmbrellaReporting.ActivityIP.identities.type.id                 | Number | Origin type for identity | 
| UmbrellaReporting.ActivityIP.identities.type.type               | String | Origin type name for identity | 
| UmbrellaReporting.ActivityIP.identities.type.label              | String | Origin type label for identity | 
| UmbrellaReporting.ActivityIP.identities.label                   | String | Label for identity | 
| UmbrellaReporting.ActivityIP.identities.deleted                 | Boolean | Indicates whether the identity was deleted or not | 
| UmbrellaReporting.ActivityIP.categories.id                      | Number | id of category | 
| UmbrellaReporting.ActivityIP.categories.label                   | String | The human readable label of the category | 
| UmbrellaReporting.ActivityIP.categories.type                    | String | The type of category | 
| UmbrellaReporting.ActivityIP.categories.deprecated              | Boolean | If the category is a legacy category | 
| UmbrellaReporting.ActivityIP.categories.integration             | Boolean | If the category is an integration |  


#### Command example IP
```!umbrella-reporting-activity-get traffic_type=ip limit=1```

#### Context Example of IP
```json
{
   "UmbrellaReporting":{
      "ActivityIP":[
        {
            "destinationip": "52.8.160.247",
            "sourceip": "192.168.0.1",
            "date": "03-15-22",
            "sourceport": 0,
            "destinationport": 0,
            "verdict": "allowed",
            "timestamp": 1548311506,
            "time": "10:15",
            "identities": [
                {
                    "id": 1,
                    "label": "Catch Rate Testing System",
                    "type": {
                        "id": 21,
                        "label": "Sites",
                        "type": "site"
                    },
                    "deleted": false
                }
            ],
            "categories": [
                {
                    "id": 66,
                    "label": "Malware",
                    "type": "security",
                    "integration": true
                }
            ],
            "type": "ip"
        }
    ]
   }
}
```
#### Human Readable Output

>### IP Activity List
>|Identity|Destination IP|Source IP|Source Port| Destination Port|Categories|Type|Action|Date & Time|
>|---|---|---|---|---|---|---|---|---|
>| Catch Rate Testing System |  10.10.10.10 | 10.10.10.10 |22|33|Malware|IP|allowed|Sep 16, 2022 05:52 AM|

#### Context Output of Intrusion

| **Path**                                                         | **Type** | **Description** |
|------------------------------------------------------------------| --- |-----------|
| UmbrellaReporting.ActivityIntrusion.type                             | String | External IP for entry. | 
| UmbrellaReporting.ActivityIntrusion.classification                         | String | The category of attack detected by a rule that is part of a more general type of attack class, such as trojan-activity, attempted-user, and unknown. |
| UmbrellaReporting.ActivityIntrusion.destinationip                         | String | Destination IP for entry. |
| UmbrellaReporting.ActivityIntrusion.severity                         | String | The severity level of the rule, such as High, Medium, Low, and Very Low. |
| UmbrellaReporting.ActivityIntrusion.sourceip                         | String | Source IP |
| UmbrellaReporting.ActivityIntrusion.destinationport                         | Number | Destination port for entry. |
| UmbrellaReporting.ActivityIntrusion.sessionid                         | Number | The unique identifier of a session, which is used to group the correlated events between various services. |
| UmbrellaReporting.ActivityIntrusion.sourceport                         | Number | Source port for entry. |
| UmbrellaReporting.ActivityIntrusion.verdict                            | String | Verdict for entry. | 
| UmbrellaReporting.ActivityIntrusion.timestamp                          | String | Timestamp in ms. | 
| UmbrellaReporting.ActivityIntrusion.time                               | String | The time in 24 hour format based on the timezone parameter. | 
| UmbrellaReporting.ActivityIntrusion.date                               | String | The date from the timestamp based on the timezone parameter. | 
| UmbrellaReporting.ActivityIntrusion.identities.id                      | Number | ID of identity. | 
| UmbrellaReporting.ActivityIntrusion.identities.type.id                 | Number | Origin type for identity | 
| UmbrellaReporting.ActivityIntrusion.identities.type.type               | String | Origin type name for identity | 
| UmbrellaReporting.ActivityIntrusion.identities.type.label              | String | Origin type label for identity | 
| UmbrellaReporting.ActivityIntrusion.identities.label                   | String | Label for identity | 
| UmbrellaReporting.ActivityIntrusion.identities.deleted                 | Boolean | Indicates whether the identity was deleted or not | 
| UmbrellaReporting.ActivityIntrusion.protocol.label                      | String | Name of the protocol. | 
| UmbrellaReporting.ActivityIntrusion.protocol.id                       | Number | ID of protocol. | 
| UmbrellaReporting.ActivityIntrusion.signature.id                 | Number | ID of the application. | 
| UmbrellaReporting.ActivityIntrusion.signature.generatorid               | Number | Unique id assigned to the part of the IPS which generated the event. | 
| UmbrellaReporting.ActivityIntrusion.signature.label              | String | A brief description of the signature. | 
| UmbrellaReporting.ActivityIntrusion.signature.cves              | String | An identifier for a known security vulnerability/exposure. |
| UmbrellaReporting.ActivityIntrusion.signaturelist.id                 | Number | Unique id assigned to a Default or Custom Signature List. | 


#### Command example of intrusion
```!umbrella-reporting-activity-get traffic_type=intrusion limit=2```

#### Context Example of intrusion
```json
{
   "UmbrellaReporting":{
      "ActivityIntrusion":[
        {
            "type": "intrusion",
            "date": "12-02-22",
            "destinationip": "10.10.10.10",
            "protocol": {
                "id": 17,
                "label": "UDP"
            },
            "sourceip": "10.10.10.10",
            "signaturelist": { "id": 1111 },
            "classification": "malicious",
            "sourceport": 22,
            "sessionid": 190898098,
            "verdict": "detected",
            "destinationport": 33,
            "timestamp": 1594557262000,
            "time": "09:30",
            "identities": [
                {
                    "id": 211034846,
                    "type": {
                        "id": 34,
                        "type": "anyconnect",
                        "label": "Anyconnect Roaming Client"
                    },
                    "label": "omerta",
                    "deleted": false
                }
            ],
            "severity": "HIGH",
            "signature": {
                "generatorid": 1,
                "id": 47829,
                "label": "SERVER-OTHER JBoss Richfaces expression language injection attempt",
                "cves": [
                    "cve-2015-0279",
                    "cve-2018-12532"
                ]
            }
        }
    ]
   }
}
```
#### Human Readable Output

>### Intrusion Activity List
>|Identity|Classification|Destination IP|Source IP|Source Port| Destination Port|Protocol|Severity|CVE|CVE|Signature|Type|Action|Date & Time|
>|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
>| Anyconnect Roaming Client | malicious | 10.10.10.10 | 10.10.10.10 |22|33|UDP|HIGH|HIGH|cve-2015-0279,cve-2018-12532|SERVER-OTHER JBoss Richfaces expression language injection attempt|intrusion|detected|Sep 16, 2022 05:52 AM|

#### Context Output of AMP

| **Path**                                            | **Type** | **Description** |
|-----------------------------------------------------| --- |-----------|
| UmbrellaReporting.ActivityAMPRetro.timestamp              | String | Timestamp in ms. | 
| UmbrellaReporting.ActivityAMPRetro.firstseenat              | Number | Timestamp. |
| UmbrellaReporting.ActivityAMPRetro.disposition              | String | Disposition for entry. |
| UmbrellaReporting.ActivityAMPRetro.hostname              | String | Hostname for entry. |
| UmbrellaReporting.ActivityAMPRetro.malwarename              | String | Malware name for entry. |
| UmbrellaReporting.ActivityAMPRetro.sha256              | String | SHA256 for entry. |
| UmbrellaReporting.ActivityAMPRetro.score              | Number | Score for entry. |


#### Command example of amp
```!umbrella-reporting-activity-get traffic_type=amp limit=1```

#### Context Example
```json
{
   "UmbrellaReporting":{
      "ActivityAMPRetro":[
        {
            "timestamp": 1548311506,
            "firstseenat": 1548311506,
            "disposition": "clean",
            "score": 10,
            "hostname": "google.com",
            "malwarename": "malware",
            "sha256": "9495b6c155044053953efe30ebaf804780c114e7b721b14f6a5b0a782769696e"
        }
    ]
   }
}
```
#### Human Readable Output

>### AMP Activity List
>|First Seen| Disposition | Score | Host Name | Malware | SHA256 | Date & Time |
>|---|---|---|---|--------|---|---|
>| 1548311506 | clean | 10 | google.com | malware | 9495b6c155044053953efe30ebaf804780c114e7b721b14f6a5b0a782769696e | Sep 16, 2022 05:52 AM |


### umbrella-reporting-summary-list
***
Get the summary.


#### Base Command

`umbrella-reporting-summary-list`
#### Input

| **Argument Name** | **Description** | **Required** |
| --- | --- | --- |
| summary_type | Get summary list of different summary types. Valid values for summary_type are category, destination, intrusion_rule.<br/>If summary type is not provided by the user, then all summary types i.e. category, destination, intrusion_rule will be considered.<br/>Supported optional parameters for category summary type are domain, urls, ip, identity_types, verdict, file_name, threats, threat_types, amp_disposition.<br/>Supported optional parameters for destination summary type are domain, urls, ip, identity_types, verdict, file_name, threats, threat_types, amp_disposition.<br/>Supported optional parameters for intrusion_rule summary type are signatures, ip, identity_types, intrusion_action, ports. Possible values are: category, destination, intrusion_rule. | Optional | 
| from | A timestamp (milliseconds) or relative time string (for example:-1days' or '1639146300000'). Filter for data that appears after this time. By default value is -7days. | Optional | 
| to | A timestamp (milliseconds) or relative time string (for example:'now' or 1661510185000). Filter for data that appears before this time. By default value is 'now'. | Optional | 
| limit | The maximum number of records to return from the collection. Default value of limit is 50. | Optional | 
| domains | A domain name or comma-delimited list of domain name. | Optional | 
| urls | A URL or comma-delimited list of URL. | Optional | 
| ip | An IP address. | Optional | 
| ports | A port number or comma-delimited list of port number. | Optional | 
| identity_types | An identity type or comma-delimited list of identity type. | Optional | 
| verdict | A verdict string. Possible values are: allowed, blocked, proxied. | Optional | 
| file_name | A string that identifies a filename. Filter request by the filename. Supports globbing or use of the wildcard character (''). The asterisk (*) matches zero or more occurrences of any character. | Optional | 
| threats | A threat name or comma-delimited list of threat name. | Optional | 
| threat_types | A threat type or comma-delimited list of threat type. | Optional | 
| amp_disposition | An AMP disposition string. Possible values are: clean, malicious, unknown. | Optional | 
| page | The page number. Default Page number is 1. | Optional | 
| page_size | The number of requested results per page. | Optional | 
| signatures | List of -, comma delimited. | Optional | 
| intrusion_action | List of intrusion actions, comma delimited. possible values: would_block, blocked, detected. | Optional | 


#### Context Output of summary list

| **Path** | **Type** | **Description** |
| --- | --- | --- |
| UmbrellaReporting.Summary.applications | Number | Total number of applications \(avc or total\). | 
| UmbrellaReporting.Summary.applicationsallowed | Number | Total number of allowed applications. | 
| UmbrellaReporting.Summary.applicationsblocked | Number | Total number of blocked applications. | 
| UmbrellaReporting.Summary.categories | Number | Total number of categories. | 
| UmbrellaReporting.Summary.domains | Number | Total number of domains. | 
| UmbrellaReporting.Summary.files | Number | Total number of files. | 
| UmbrellaReporting.Summary.filetypes | Number | Total number of file types. | 
| UmbrellaReporting.Summary.identities | Number | Total number of identities. | 
| UmbrellaReporting.Summary.identitytypes | Number | Total number of identity types. | 
| UmbrellaReporting.Summary.policycategories | Number | Total number of blocked categories. | 
| UmbrellaReporting.Summary.policyrequests | Number | Total number of policy requests. | 
| UmbrellaReporting.Summary.requests | Number | Total number of requests. | 
| UmbrellaReporting.Summary.requestsallowed | Number | Total number of allowed requests. | 
| UmbrellaReporting.Summary.requestsblocked | Number | Total number of blocked requests. | 

#### Command example
```!umbrella-reporting-summary-list domains=api.tunnels.cdfw.umbrella.com```
#### Context Example
```json
{
    "UmbrellaReporting": {
        "Summary": {
            "applications": 0,
            "applicationsallowed": 0,
            "applicationsblocked": 0,
            "categories": 0,
            "domains": 0,
            "files": 0,
            "filetypes": 0,
            "identities": 0,
            "identitytypes": 0,
            "policycategories": 0,
            "policyrequests": 0,
            "requests": 0,
            "requestsallowed": 0,
            "requestsblocked": 0
        }
    }
}
```

#### Human Readable Output

>### Summary List
>|Application|Allowed Application|Blocked Application|Category|Domain|File|File Type|Identity|Identity Type|Policy Category|Policy Request|Request|Allowed Request|Blocked Request|
>|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
>| 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 |



#### Context Output of summary with category 

| **Path** | **Type** | **Description** |
| --- | --- | --- |
| UmbrellaReporting.SummaryWithCategory.category.label | String | The human readable label of the category. | 
| UmbrellaReporting.SummaryWithCategory.category.type | String | The type of category. |
| UmbrellaReporting.SummaryWithCategory.category.deprecated | Boolean | If the category is a legacy category. |
| UmbrellaReporting.SummaryWithCategory.category.integration | boolean | If the category is an integration. |
| UmbrellaReporting.SummaryWithCategory.category.id | Number | ID of category. |
| UmbrellaReporting.SummaryWithCategory.summary.applications | Number | Total number of applications \(avc or total\). | 
| UmbrellaReporting.SummaryWithCategory.summary.applicationsallowed | Number | Total number of allowed applications. | 
| UmbrellaReporting.SummaryWithCategory.summary.applicationsblocked | Number | Total number of blocked applications. | 
| UmbrellaReporting.SummaryWithCategory.summary.categories | Number | Total number of categories. | 
| UmbrellaReporting.SummaryWithCategory.summary.domains | Number | Total number of domains. | 
| UmbrellaReporting.SummaryWithCategory.summary.files | Number | Total number of files. | 
| UmbrellaReporting.SummaryWithCategory.summary.filetypes | Number | Total number of file types. | 
| UmbrellaReporting.SummaryWithCategory.summary.identities | Number | Total number of identities. | 
| UmbrellaReporting.SummaryWithCategory.summary.identitytypes | Number | Total number of identity types. | 
| UmbrellaReporting.SummaryWithCategory.summary.policycategories | Number | Total number of blocked categories. | 
| UmbrellaReporting.SummaryWithCategory.summary.policyrequests | Number | Total number of policy requests. | 
| UmbrellaReporting.SummaryWithCategory.summary.requests | Number | Total number of requests. | 
| UmbrellaReporting.SummaryWithCategory.summary.requestsallowed | Number | Total number of allowed requests. | 
| UmbrellaReporting.SummaryWithCategory.summary.requestsblocked | Number | Total number of blocked requests. |


#### Command example of summary with category
```!umbrella-reporting-summary-list summary_type=category limit=1```

#### Context Example of summary with category
```json
{
   "UmbrellaReporting":{
      "SummaryWithCategory":[
        {
            "category": {
                "id": 66,
                "label": "Malware",
                "type": "security",
                "integration": true
            },
            "summary": {
                "applications": 0,
                "domains": 0,
                "requestsblocked": 0,
                "filetypes": 0,
                "policycategories": 0,
                "requests": 0,
                "requestsallowed": 0,
                "categories": 0,
                "identitytypes": 0,
                "applicationsblocked": 0,
                "files": 0,
                "identities": 0,
                "applicationsallowed": 0,
                "policyrequests": 0
            }
        }
    ]
   }
}
```
#### Human Readable Output

#### Human Readable Output

>### Summary with Category List 
>|Category Type| Category Name |Application|Allowed Application|Blocked Application|Category|Domain|File|File Type|Identity|Identity Type|Policy Category|Policy Request|Request|Allowed Request|Blocked Request|
>|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
>| security | Malware | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 |

#### Context Output of summary with destination

| **Path** | **Type** | **Description**                                |
| --- |----------|------------------------------------------------|
| UmbrellaReporting.SummaryWithDestination.domain | String   | Total number of applications (avc or total).   |
| UmbrellaReporting.SummaryWithDestination.summary.applications | Number   | Total number of applications \(avc or total\). | 
| UmbrellaReporting.SummaryWithDestination.summary.applicationsallowed | Number   | Total number of allowed applications.          | 
| UmbrellaReporting.SummaryWithDestination.summary.applicationsblocked | Number   | Total number of blocked applications.          | 
| UmbrellaReporting.SummaryWithDestination.summary.categories | Number   | Total number of categories.                    | 
| UmbrellaReporting.SummaryWithDestination.summary.domains | Number   | Total number of domains.                       | 
| UmbrellaReporting.SummaryWithDestination.summary.files | Number   | Total number of files.                         | 
| UmbrellaReporting.SummaryWithDestination.summary.filetypes | Number   | Total number of file types.                    | 
| UmbrellaReporting.SummaryWithDestination.summary.identities | Number   | Total number of identities.                    | 
| UmbrellaReporting.SummaryWithDestination.summary.identitytypes | Number   | Total number of identity types.                | 
| UmbrellaReporting.SummaryWithDestination.summary.policycategories | Number   | Total number of blocked categories.            | 
| UmbrellaReporting.SummaryWithDestination.summary.policyrequests | Number   | Total number of policy requests.               | 
| UmbrellaReporting.SummaryWithDestination.summary.requests | Number   | Total number of requests.                      | 
| UmbrellaReporting.SummaryWithDestination.summary.requestsallowed | Number   | Total number of allowed requests.              | 
| UmbrellaReporting.SummaryWithDestination.summary.requestsblocked | Number   | Total number of blocked requests.              |


#### Command example of summary with destination
```!umbrella-reporting-summary-list summary_type=destination limit=1```

#### Context Example of summary with destination
```json
{
   "UmbrellaReporting":{
      "SummaryWithDestination":[
        {
            "domain": "www.google.com",
            "summary": {
                "applications": 0,
                "domains": 0,
                "requestsblocked": 0,
                "filetypes": 0,
                "policycategories": 0,
                "policyrequests": 0,
                "requests": 0,
                "requestsallowed": 0,
                "categories": 0,
                "identitytypes": 0,
                "applicationsblocked": 0,
                "files": 0,
                "identities": 0,
                "applicationsallowed": 0
            }
        }
    ]
   }
}
```
#### Human Readable Output

>### Summary with Destination List 
>|Destination| Application|Allowed Application|Blocked Application|Category|Domain|File|File Type|Identity|Identity Type|Policy Category|Policy Request|Request|Allowed Request|Blocked Request|
>|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
>| www.google.com | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 |

#### Context Output of summary with intrusion

| **Path** | **Type** | **Description**                                |
| --- |----------|------------------------------------------------|
| UmbrellaReporting.SignatureListSummary.signaturelist.id | Number   | Unique id assigned to a Default or Custom Signature List.   |
| UmbrellaReporting.SignatureListSummary.signatures.generatorid | Number   | Generator id. | 
| UmbrellaReporting.SignatureListSummary.signatures.id | Number   | ID. | 
| UmbrellaReporting.SignatureListSummary.signatures.lasteventat | Number   | Last Eevent At. | 
| UmbrellaReporting.SignatureListSummary.signatures.lasteventat.counts.blocked | Number   | Blocked | 
| UmbrellaReporting.SignatureListSummary.signatures.lasteventat.counts.detected | Number   | Detected. |
| UmbrellaReporting.SignatureListSummary.signatures.lasteventat.counts.wouldblock | Number   | Would Block. |


#### Command example of summary with intrusion
```!umbrella-reporting-summary-list summary_type=intrusion_rule limit=1```

#### Context Example of summary with intrusion
```json
{
   "UmbrellaReporting":{
      "SignatureListSummary":[
        {
            "signaturelist": { "id": 1111 },
            "signatures": [
                {
                    "counts": {
                        "blocked": 0,
                        "detected": 1,
                        "wouldblock": 0
                    },
                    "generatorid": 1,
                    "lasteventat": 1594557262000,
                    "id": 47829
                }
            ]
        }
    ]
   }
}
```

#### Human Readable Output

>### Summary with Intrusion List 
>|Blocked| Detected | Would Block | Last Event |
>|---|---|---|---|
>| 0 | 1 | 0 | 1594557262000 |
