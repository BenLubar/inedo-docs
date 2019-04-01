---
title: Connector Health API
subtitle: Connector Health API
sequence: 200
keywords: proget,feeds,api,connector,health
show-headings-in-nav: true
---

The Connector Health API Endpoint offer a simple mechanism for querying the health status of the connectors accross and instance of ProGet.

For security and simplicity, these endpoints require that a `[Feed Management API Key]` is created first. This key is passed into the API call within the body or the header of your request.
`{
   "API_key": "APIKEY"
 }`

### Feed Data Specification {#feed-data-specification}


This endpoint sends and receives entries as [JSON](http://json.org/) objects.

<tab-block>
<tab name="Feed">

Property               | Format
-----------------------|----------
`Id`                 | An *integer* that represents the unique identifier of the connector **optional**.
`Name`             | A *string* value of the connector name.
`Url`          | A *string* value of the Url of the connector.
`State`          | A *string* that displays the health status returned by the connector Url.
`LastChecked`               | A *datetime* representing the last time the connector health was checked.

</tab>
</tab-block>


### Endpoint Specifications {#endpoints}
You will have two options for accessing the connector health endpoints.

{.info}

**All Connectors**
```
_GET/POST_ ::/api/connector-health/?key=secure123 
```
**A Single Connector**
```
_GET/POST_ ::/api/connector-health/{Id}/?key=secure123 
```

- `Id` can be added optionally to access the status of a specific connector.


These endpoints return a status of 200 (on success), or 403 (api key not authorized), and a body containing only an *array* of entity objects. 

{.info}

<tab-block>
<tab name="List Connector Health">

```
[
    {
        "Id": 1,
        "Name": "npmConnector",
        "Url": "https://registry.npmjs.org",
        "State": "Healthy",
        "LastChecked": "2019-03-29T17:41:59.907+00:00"
    },
    {
        "Id": 2,
        "Name": "ChocolateyConnector",
        "Url": "https://www.chocolatey.org/api/v2",
        "State": "Healthy",
        "LastChecked": "2019-03-29T17:41:59.903+00:00"
    },
    {
        "Id": 3,
        "Name": "nugetConnector",
        "Url": "https://www.nuget.org/api/v2",
        "State": "Healthy",
        "LastChecked": "2019-03-29T17:41:55.05+00:00"
    },
    {....}

]
```
</tab>
</tab-block>