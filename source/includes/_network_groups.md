## Network Groups

Provides API for managing Network Groups.

<!--## Get All Network Groups-->

```shell
curl "$MORPHEUS_API_URL/api/networks/groups"
  -H "Authorization: BEARER $MORPHEUS_API_TOKEN"
```

> The above command returns JSON structured like this:

```json
{
  "networkGroups": [
    {
      "id": 1,
      "name": "test network group",
      "description": "a test network group",
      "visibility": "private",
      "active": true,
      "networks": [
        1
      ],
      "subnets": [

      ],
      "tenants": [
        {
          "id": 1,
          "name": "root"
        }
      ]
    }
  ],
  "meta": {
    "size": 1,
    "total": 1,
    "offset": 0,
    "max": 25
  }
}
```

This endpoint retrieves all Network Groups associated with the account.

### HTTP Request

`GET https://api.gomorpheus.com/api/networks/groups`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
name |  | If specified will return an exact match on name
phrase |  | If specified will return a partial match on name

## Get a Specific Network Group


```shell
curl "$MORPHEUS_API_URL/api/networks/groups/1" \
  -H "Authorization: BEARER $MORPHEUS_API_TOKEN"
```

> The above command returns JSON structured like this:

```json
{
  "networkGroup": {
    "id": 1,
    "name": "test network group",
    "description": "a test network group",
    "visibility": "private",
    "active": true,
    "networks": [
      1
    ],
    "subnets": [

    ],
    "tenants": [
      {
        "id": 1,
        "name": "root"
      }
    ],
    "resourcePermission": {
      "all": true,
      "sites": [
        {
          "id": 284,
          "name": "anothergroup",
          "default": true
        },
        {
          "id": 317,
          "name": "another group",
          "default": false
        }
      ],
      "allPlans": null,
      "plans": [

      ]
    }
  },
  "networks": [
    {
      "id": 1,
      "name": "VM Network",
      "zone": {
        "id": 29,
        "name": "den-vcenter"
      },
      "type": {
        "id": 6,
        "name": "VMWare Network",
        "code": "vmwareNetwork"
      },
      "owner": {
        "id": 1,
        "name": "root"
      },
      "code": "vmware.network.29.network-51",
      "category": "vmware.network.29",
      "interfaceName": null,
      "bridgeName": null,
      "bridgeInterface": null,
      "description": "VM Network",
      "externalId": "network-51",
      "internalId": null,
      "uniqueId": "network-51",
      "externalType": "Network",
      "refUrl": null,
      "refType": "ComputeZone",
      "refId": 29,
      "vlanId": null,
      "vswitchName": null,
      "dhcpServer": true,
      "dhcpIp": null,
      "gateway": null,
      "netmask": null,
      "broadcast": null,
      "subnetAddress": null,
      "dnsPrimary": null,
      "dnsSecondary": null,
      "cidr": null,
      "tftpServer": null,
      "bootFile": null,
      "switchId": null,
      "fabricId": null,
      "networkRole": null,
      "status": null,
      "availabilityZone": null,
      "pool": null,
      "networkProxy": null,
      "networkDomain": null,
      "prefixLength": null,
      "visibility": "private",
      "enableAdmin": false,
      "scanNetwork": null,
      "active": true,
      "defaultNetwork": false,
      "assignPublicIp": false,
      "noProxy": null,
      "applianceUrlProxyBypass": true,
      "zonePool": {
        "id": 12,
        "name": "labs-den-pool"
      },
      "allowStaticOverride": null,
      "subnets": [

      ]
    }
  ],
  "subnets": [

  ]
}
```

This endpoint retrieves a specific Network Group.


### HTTP Request

`GET https://api.gomorpheus.com/api/networks/groups/:id`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the Network Group to retrieve


## Create a Network Group

```shell
curl -XPOST "$MORPHEUS_API_URL/api/networks/groups" \
  -H "Authorization: BEARER $MORPHEUS_API_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
  "networkGroup": {
    "name": "test network group",
    "description": "a test network group",
    "networks": [
      1
    ],
    "subnets": [

    ]
  }
}'
```

> The above command returns JSON structured like getting a single Network Group: 

### HTTP Request

`POST https://api.gomorpheus.com/api/networks/groups`

### JSON Parameters

Parameter | Default | Description
--------- | ------- | -----------
name      |  | Name
description      |  | Description

## Update a Network Group

```shell
curl -XPUT "$MORPHEUS_API_URL/api/networks/groups/:id" \
  -H "Authorization: BEARER $MORPHEUS_API_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
  "networkGroup": {
    "name": "my network group",
    "description": "my test network group",
    "networks": [
      2
    ],
    "subnets": [

    ]
  }
}'
```

> The above command returns JSON structured like getting a single Network Group: 

### HTTP Request

`PUT https://api.gomorpheus.com/api/networks/groups/:id`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the Network Group

### JSON Parameters

Same as [Create](#create-a-network-group).

## Delete a Network Group

```shell
curl -XDELETE "$MORPHEUS_API_URL/api/networks/groups/1" \
  -H "Authorization: BEARER $MORPHEUS_API_TOKEN"
```

> The above command returns JSON Structured like this:

```json
{
  "success": true
}
```

Will delete a Network Group from the system and make it no longer usable.

### HTTP Request

`DELETE https://api.gomorpheus.com/api/networks/groups/:id`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the Network Group

