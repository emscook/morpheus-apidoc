# Price Sets

Provides API interfaces for managing price sets within Morpheus

## Get All Price Sets

```shell
curl "$MORPHEUS_API_URL/api/price-sets" \
  -H "Authorization: BEARER $MORPHEUS_API_TOKEN"
```

> The above command returns JSON structured like this:

```json
{
  "priceSets": [
    {
      "id": 25,
      "name": "Amazon - c1.medium - US West (N. California)",
      "code": "amazon.c1.medium.ec2.us-west-1.amazonaws.com",
      "active": true, 
      "priceUnit": "hour",
      "type": "compute_plus_storage",
      "regionCode": "ec2.us-west-1.amazonaws.com",
      "systemCreated": false,
      "zone": null,
      "zonePool": null,
      "account": null,
      "prices": [
        {
          "id": 3,
          "name": "Amazon - EBS (gp2) - US West (N. California)",
          "code": "amazon.storage.ebs.ec2.us-west-1.amazonaws.com",
          "priceType": "storage",
          "priceUnit": "month",
          "additionalPriceUnit": "GB",
          "price": 0.12,
          "customPrice": 0.0,
          "markupType": null,
          "markup": 0.0,
          "markupPercent": 0.0,
          "cost": 0.12,
          "currency": "usd",
          "incurCharges": "always",
          "platform": null,
          "software": null,
          "volumeType": {
            "id": 10,
            "code": "amazon-gp2",
            "name": "gp2"
          },
          "datastore": null,
          "crossCloudApply": null,
          "account": null
        }
      ]
    }
  ],
  "meta": {
    "size": 1,
    "total": 169,
    "offset": 0,
    "max": 1
  }
}
```

This endpoint retrieves all price sets.

### HTTP Request

`GET https://api.gomorpheus.com/api/price-sets`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
max | 25 | Max number of results to return
offset | 0 | Offset of records you want to load
sort | name | Sort order
direction | asc | Sort direction, use 'desc' to reverse sort
phrase |  | Restricts query to only load price sets with name or code containing the phrase specified
includeInactive | false | If true, include inactive prices in the results


## Get a Specific Price Set

```shell
curl "$MORPHEUS_API_URL/api/price-sets/1" \
  -H "Authorization: BEARER $MORPHEUS_API_TOKEN"
```

> The above command returns JSON structured like this:

```json
{
  "priceSet": {
    "id": 25,
    "name": "Amazon - c1.medium - US West (N. California)",
    "code": "amazon.c1.medium.ec2.us-west-1.amazonaws.com",
    "active": true, 
    "priceUnit": "hour",
    "type": "compute_plus_storage",
    "regionCode": "ec2.us-west-1.amazonaws.com",
    "systemCreated": false,
    "zone": null,
    "zonePool": null,
    "account": null,
    "prices": [
      {
        "id": 3,
        "name": "Amazon - EBS (gp2) - US West (N. California)",
        "code": "amazon.storage.ebs.ec2.us-west-1.amazonaws.com",
        "priceType": "storage",
        "priceUnit": "month",
        "additionalPriceUnit": "GB",
        "price": 0.12,
        "customPrice": 0.0,
        "markupType": null,
        "markup": 0.0,
        "markupPercent": 0.0,
        "cost": 0.12,
        "currency": "usd",
        "incurCharges": "always",
        "platform": null,
        "software": null,
        "volumeType": {
          "id": 10,
          "code": "amazon-gp2",
          "name": "gp2"
        },
        "datastore": null,
        "crossCloudApply": null,
        "account": null
      }
    ]
  }
}
```

This endpoint retrieves a specific price set.

### HTTP Request

`GET https://api.gomorpheus.com/api/price-sets/:id`

### URL Parameters

Parameter | Description
--------- | -----------
id | ID of the price set


## Create a Price Set

Use this command to create a price set.

```shell
curl -XPOST "$MORPHEUS_API_URL/api/price-sets" \
  -H "Authorization: BEARER $MORPHEUS_API_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"priceSet": {
        "name": "price set 1",
        "code": "price.set.1",
        "regionCode": "region.code.1",
        "zone": {
          "id": 3
        },
        "zonePool": {
          "id": 7
        },
        "priceUnit": "hour",
        "type": "compute_plus_storage",
        "prices": [
          {
            "id": 409
          },
          {
            "id": 124
          }
        ]
     }}'
```

> The above command returns JSON Structured like this:

```json
{
  "success": true,
  "id": 1
}
```

### HTTP Request

`POST https://api.gomorpheus.com/api/price-sets`

### JSON Parameters

Parameter | Required | Description
--------- | -------- | -----------
name | Y | Price set name
code | Y | Price set code, must be unique
regionCode | N | Price set region code
zone.id | N | Cloud ID
zonePool.id | N | Resource pool ID
priceUnit | Y | Price unit: minute, hour, day, month, year, two year, three year, four year, five year
type | Y | Price set type: fixed, compute_plus_storage, component
prices | N | List of price IDs to associate with price set


## Update a Price Set

```shell
curl -XPUT "$MORPHEUS_API_URL/api/price-sets/1" \
  -H "Authorization: BEARER $MORPHEUS_API_TOKEN"
  -H "Content-Type: application/json" \
  -d '{"priceSet": {
          "name": "new price set name",
          "restartUsage": true,
          "prices": [
            {
              "id": 409
            },
            {
              "id": 124
            }
          ]
        }
      }
```

> The above command returns JSON structured like this:

```json
{
  "success": true
}
```

### HTTP Request

`PUT https://api.gomorpheus.com/api/price-sets/:id`

### URL Parameters

Parameter | Description
--------- | -----------
id | The ID of the price set

### JSON Parameters

Parameter | Required | Description
--------- | -------- | -----------
name | N | Price set new name
restartUsage | N | Can be used to apply price changes to usage: true, false
prices | N | List of price IDs to associate with price set
 

## Deactivate a Price Set

```shell
curl -XPUT "$MORPHEUS_API_URL/api/price-sets/1/deactivate" \
  -H "Authorization: BEARER $MORPHEUS_API_TOKEN"
```

> The above command returns JSON structure like this:

```json
{
  "success": true
}
```

Will deactivate a price set 

### HTTP Request

`PUT https://api.gomorpheus.com/api/price-sets/:id/deactivate`

### URL Parameters

Parameter | Description
--------- | -----------
id | The ID of the price set