## Subnets

Provides API for managing Network Subnets.

<!--## Get All Subnets-->

```shell
curl "$MORPHEUS_API_URL/api/subnets"
  -H "Authorization: BEARER $MORPHEUS_API_TOKEN"
```

> The above command returns JSON structured like this:

```json

{
  "subnets": [
    {
      "id": 26,
      "code": null,
      "name": "test-subnet",
      "active": true,
      "description": null,
      "externalId": "/subscriptions/88213e1e-d4c5-467f-b029-aa3021a798/resourceGroups/ARMUbuntu16/providers/Microsoft.Network/virtualNetworks/test-subnets",
      "uniqueId": null,
      "addressPrefix": null,
      "cidr": "192.168.1.0/24",
      "gateway": null,
      "netmask": "255.255.255.0",
      "subnetAddress": "192.168.1.0/24",
      "tftpServer": null,
      "bootFile": null,
      "pool": null,
      "dhcpServer": true,
      "hasFloatingIps": false,
      "dhcpIp": null,
      "dnsPrimary": null,
      "dnsSecondary": null,
      "dhcpStart": "192.168.1.1",
      "dhcpEnd": "192.168.1.254",
      "dhcpRange": null,
      "networkProxy": null,
      "networkDomain": null,
      "searchDomains": null,
      "defaultNetwork": false,
      "assignPublicIp": false,
      "visibility": "private",
      "status": {
        "enumType": "com.morpheus.NetworkSubnet$Status",
        "name": "AVAILABLE"
      },
      "network": {
        "id": 55,
        "name": "our-subnet"
      },
      "type": {
        "id": 6,
        "code": "azure",
        "name": "Azure Subnet"
      },
      "account": {
        "id": 1,
        "name": "root"
      },
      "securityGroups": [

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

        ],
        "allPlans": true,
        "plans": [

        ]
      }
    },
    {
      "id": 77,
      "code": null,
      "name": "test-subnet2",
      "active": true,
      "description": null,
      "externalId": "/subscriptions/88213e1e-d4c5-467f-b029-aa3021a798/resourceGroups/ARMUbuntu16/providers/Microsoft.Network/virtualNetworks/test-subnets2",
      "uniqueId": null,
      "addressPrefix": null,
      "cidr": "192.168.2.0/24",
      "gateway": null,
      "netmask": "255.255.255.0",
      "subnetAddress": "192.168.2.0/24",
      "tftpServer": null,
      "bootFile": null,
      "pool": null,
      "dhcpServer": true,
      "hasFloatingIps": false,
      "dhcpIp": null,
      "dnsPrimary": null,
      "dnsSecondary": null,
      "dhcpStart": "192.168.2.1",
      "dhcpEnd": "192.168.2.254",
      "dhcpRange": null,
      "networkProxy": null,
      "networkDomain": null,
      "searchDomains": null,
      "defaultNetwork": false,
      "assignPublicIp": false,
      "visibility": "private",
      "status": {
        "enumType": "com.morpheus.NetworkSubnet$Status",
        "name": "AVAILABLE"
      },
      "network": {
        "id": 55,
        "name": "our-subnet"
      },
      "type": {
        "id": 6,
        "code": "azure",
        "name": "Azure Subnet"
      },
      "account": {
        "id": 1,
        "name": "root"
      },
      "securityGroups": [

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

        ],
        "allPlans": true,
        "plans": [

        ]
      }
    }
  ],
  "meta": {
    "size": 2,
    "total": 2,
    "offset": 0,
    "max": 25
  }
}
```

This endpoint retrieves all Subnets associated with the account.

### HTTP Request

`GET https://api.gomorpheus.com/api/subnets`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
name |  | If specified will return an exact match on name
phrase |  | If specified will return a partial match on name

## Get Subnets for a Network

```shell
curl "$MORPHEUS_API_URL/api/networks/55/subnets"
  -H "Authorization: BEARER $MORPHEUS_API_TOKEN"
```

> The above command returns JSON structured like this:

```json

{
  "subnets": [
    {
      "id": 26,
      "code": null,
      "name": "test-subnet",
      "active": true,
      "description": null,
      "externalId": "/subscriptions/88213e1e-d4c5-467f-b029-aa3021a798/resourceGroups/ARMUbuntu16/providers/Microsoft.Network/virtualNetworks/test-subnets",
      "uniqueId": null,
      "addressPrefix": null,
      "cidr": "192.168.1.0/24",
      "gateway": null,
      "netmask": "255.255.255.0",
      "subnetAddress": "192.168.1.0/24",
      "tftpServer": null,
      "bootFile": null,
      "pool": null,
      "dhcpServer": true,
      "hasFloatingIps": false,
      "dhcpIp": null,
      "dnsPrimary": null,
      "dnsSecondary": null,
      "dhcpStart": "192.168.1.1",
      "dhcpEnd": "192.168.1.254",
      "dhcpRange": null,
      "networkProxy": null,
      "networkDomain": null,
      "searchDomains": null,
      "defaultNetwork": false,
      "assignPublicIp": false,
      "visibility": "private",
      "status": {
        "enumType": "com.morpheus.NetworkSubnet$Status",
        "name": "AVAILABLE"
      },
      "network": {
        "id": 55,
        "name": "our-subnet"
      },
      "type": {
        "id": 6,
        "code": "azure",
        "name": "Azure Subnet"
      },
      "account": {
        "id": 1,
        "name": "root"
      },
      "securityGroups": [

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

        ],
        "allPlans": true,
        "plans": [

        ]
      }
    },
    {
      "id": 77,
      "code": null,
      "name": "test-subnet2",
      "active": true,
      "description": null,
      "externalId": "/subscriptions/88213e1e-d4c5-467f-b029-aa3021a798/resourceGroups/ARMUbuntu16/providers/Microsoft.Network/virtualNetworks/test-subnets2",
      "uniqueId": null,
      "addressPrefix": null,
      "cidr": "192.168.2.0/24",
      "gateway": null,
      "netmask": "255.255.255.0",
      "subnetAddress": "192.168.2.0/24",
      "tftpServer": null,
      "bootFile": null,
      "pool": null,
      "dhcpServer": true,
      "hasFloatingIps": false,
      "dhcpIp": null,
      "dnsPrimary": null,
      "dnsSecondary": null,
      "dhcpStart": "192.168.2.1",
      "dhcpEnd": "192.168.2.254",
      "dhcpRange": null,
      "networkProxy": null,
      "networkDomain": null,
      "searchDomains": null,
      "defaultNetwork": false,
      "assignPublicIp": false,
      "visibility": "private",
      "status": {
        "enumType": "com.morpheus.NetworkSubnet$Status",
        "name": "AVAILABLE"
      },
      "network": {
        "id": 55,
        "name": "our-subnet"
      },
      "type": {
        "id": 6,
        "code": "azure",
        "name": "Azure Subnet"
      },
      "account": {
        "id": 1,
        "name": "root"
      },
      "securityGroups": [

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

        ],
        "allPlans": true,
        "plans": [

        ]
      }
    }
  ],
  "meta": {
    "size": 2,
    "total": 2,
    "offset": 0,
    "max": 25
  }
}
```

This endpoint retrieves all Subnets under a specific network.

### HTTP Request

`GET https://api.gomorpheus.com/api/networks/:networkId/subnets`


### URL Parameters

Parameter | Description
--------- | -----------
:networkId | The ID of the Network.

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
name |  | If specified will return an exact match on name
phrase |  | If specified will return a partial match on name


## Get a Specific Subnet

```shell
curl "$MORPHEUS_API_URL/api/subnets/77" \
  -H "Authorization: BEARER $MORPHEUS_API_TOKEN"
```

> The above command returns JSON structured like this:

```json
{
  "subnet": {
    "id": 77,
    "code": null,
    "name": "def2",
    "active": true,
    "description": null,
    "externalId": "/subscriptions/88213e1e-d4c5-467f-b029-aa3021a798/resourceGroups/ARMUbuntu16/providers/Microsoft.Network/virtualNetworks/test-subnets2",
    "uniqueId": null,
    "addressPrefix": null,
    "cidr": "192.168.2.0/24",
    "gateway": null,
    "netmask": "255.255.255.0",
    "subnetAddress": "192.168.2.0/24",
    "tftpServer": null,
    "bootFile": null,
    "pool": null,
    "dhcpServer": true,
    "hasFloatingIps": false,
    "dhcpIp": null,
    "dnsPrimary": null,
    "dnsSecondary": null,
    "dhcpStart": "192.168.2.1",
    "dhcpEnd": "192.168.2.254",
    "dhcpRange": null,
    "networkProxy": null,
    "networkDomain": null,
    "searchDomains": null,
    "defaultNetwork": false,
    "assignPublicIp": false,
    "visibility": "private",
    "status": {
      "enumType": "com.morpheus.NetworkSubnet$Status",
      "name": "AVAILABLE"
    },
    "network": {
      "id": 55,
      "name": "our-subnet"
    },
    "type": {
      "id": 6,
      "code": "azure",
      "name": "Azure Subnet"
    },
    "account": {
      "id": 1,
      "name": "root"
    },
    "securityGroups": [

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

      ],
      "allPlans": true,
      "plans": [

      ]
    }
  }
}
```

This endpoint retrieves a specific Subnet.


### HTTP Request

`GET https://api.gomorpheus.com/api/subnets/:id`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the Subnet to retrieve

## Create a Subnet

```shell
curl -XPOST "$MORPHEUS_API_URL/api/1/subnets" \
  -H "Authorization: BEARER $MORPHEUS_API_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
  "subnet": {
    "type": {
      "id": 6
    },
    "config": {
      "subnetName": "My Subnet",
      "subnetCidr": "192.168.2.0/24"
    }
  },
  "resourcePermissions": {
    "all": true
  }
}'
```

> The above command returns JSON structured like getting a single Subnet: 

### HTTP Request

`POST https://api.gomorpheus.com/api/:networkId/subnets`

### URL Parameters

Parameter | Description
--------- | -----------
:networkId | The ID of the Network this subnet will belong to.

### JSON Parameters

Parameter | Default | Description
--------- | ------- | -----------
type.id      |  | [Subnet Types](#subnet-types) ID
config      |  | Configuration object. Settings vary by type.
visibility      | private | private or public
tenantPermissions.accounts  |  | Array of tenant account ids that are allowed access
resourcePermissions.all  |  | Pass true to allow access all groups
resourcePermissions.sites  |  | Array of groups that are allowed access

This endpoint allows creating a Subnet.  Only certain types of clouds support creating and deleting subnets. Configuration options vary for each [Subnet Type](#subnet-types).


## Update a Subnet

```shell
curl -XPUT "$MORPHEUS_API_URL/api/subnets/1" \
  -H "Authorization: BEARER $MORPHEUS_API_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
  "subnet": {
    "config": {
      "subnetName": "Our Subnet"
    }
  }
}'
```

> The above command returns JSON structured like getting a single Subnet: 

### HTTP Request

`PUT https://api.gomorpheus.com/api/subnets/:id`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the Subnet

### JSON Parameters

Parameter | Default | Description
--------- | ------- | -----------
type.id      |  | [Subnet Types](#subnet-types) ID
config      |  | Configuration object. Settings vary by type.
visibility      | private | private or public
tenantPermissions.accounts  |  | Array of tenant account ids that are allowed access
resourcePermissions.all  |  | Pass true to allow access all groups
resourcePermissions.sites  |  | Array of groups that are allowed access

This endpoint allows updating a Subnet.  Only certain types of clouds support this action. Configuration options vary for each [Subnet Type](#subnet-types).

## Delete a Subnet

```shell
curl -XDELETE "$MORPHEUS_API_URL/api/subnets/1" \
  -H "Authorization: BEARER $MORPHEUS_API_TOKEN"
```

> The above command returns JSON Structured like this:

```json
{
  "success": true
}
```

Will delete a Subnet from the system and make it no longer usable.

### HTTP Request

`DELETE https://api.gomorpheus.com/api/subnets/:id`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the Subnet

