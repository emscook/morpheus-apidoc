## Resource Folders

Resource Folders can be managed for each Compute Zone (Cloud) in your infrastructure.

<!--## Get All Resource Folders for Cloud-->

```shell
curl "$MORPHEUS_API_URL/api/zones/5/folders"
  -H "Authorization: BEARER $MORPHEUS_API_TOKEN"
```

> The above command returns JSON structured like this:

```json
{
  "folders": [
    {
      "id": 50,
      "name": "My Folder",
      "zone": {
        "id": 5,
        "name": "test-vmware"
      },
      "parent": null,
      "type": "default",
      "externalId": "group-v2342",
      "visibility": "private",
      "readOnly": false,
      "defaultFolder": false,
      "defaultStore": false,
      "active": true,
      "tenants": [
        {
          "id": 1,
          "name": "root",
          "defaultStore": false,
          "defaultTarget": false
        }
      ],
      "resourcePermission": {
        "all": true,
        "sites": [

        ],
        "allPlans": true,
        "plans": [

        ]
      },
      "depth": 0
    }
  ],
  "meta": {
    "size": 1,
    "total": 30,
    "offset": 0,
    "max": 25
  }
}
```

This endpoint retrieves all resource folders under a cloud.

### HTTP Request

`GET https://api.gomorpheus.com/api/zones/:zoneId/folders`

### URL Parameters

Parameter | Description
--------- | -----------
zoneId | The ID of the cloud

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
phrase |  | Filter on partial match of name
name |  | Filter on exact match of name

## Get a Specific Resource Folder

```shell
curl "$MORPHEUS_API_URL/api/zones/5/folders/50" \
  -H "Authorization: BEARER $MORPHEUS_API_TOKEN"
```

> The above command returns JSON structured like this:

```json
{
  "folder": {
    "id": 50,
    "name": "My Folder",
    "zone": {
      "id": 5,
      "name": "test-vmware"
    },
    "parent": null,
    "type": "default",
    "externalId": "group-v2342",
    "visibility": "private",
    "readOnly": false,
    "defaultFolder": false,
    "defaultStore": false,
    "active": true,
    "tenants": [
      {
        "id": 1,
        "name": "root",
        "defaultStore": false,
        "defaultTarget": false
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

This endpoint retrieves a specific resource folder.


### HTTP Request

`GET https://api.gomorpheus.com/api/zones/:zoneId/folders/:id`

### URL Parameters

Parameter | Description
--------- | -----------
zoneId | The ID of the cloud
id | The ID of the resource folder to retrieve

## Updating a Resource Folder

```shell
curl -XPUT "$MORPHEUS_API_URL/api/zones/5/folders/50" \
  -H "Authorization: BEARER $MORPHEUS_API_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"folder":{
    "active": true,
    "visibility": "private",
    "tenantPermissions": {
      "accounts": [1]
    },
    "resourcePermissions": {
      "all": false,
      "sites": [
        {"id": 1}, {"id": 2}, {"id": 3}
      ]
    }
  }}'
```

> The above command returns JSON structured like getting a single resource folder:

This endpoint allows updating settings for a resource folder.

### HTTP Request

`PUT https://api.gomorpheus.com/api/zones/:zoneId/folders/:id`

### URL Parameters

Parameter | Description
--------- | -----------
zoneId | The ID of the cloud
id | The ID of the resource folder

### JSON Parameters

Parameter | Default | Description
--------- | ------- | -----------
defaultFolder      | false | Set as the Default Folder
defaultImage      | false | Set as the Default Image Target
active      |  | Activate (true) or disable (false) the resource folder
visibility      | private | private or public
tenantPermissions.accounts  |  | Array of tenant account ids that are allowed access
resourcePermissions.all  |  | Pass true to allow access all groups
resourcePermissions.sites  |  | Array of groups that are allowed access
resourcePermissions.allPlans  |  | Pass true to allow access all plans
resourcePermissions.plans  |  | Array of plans that are allowed access
