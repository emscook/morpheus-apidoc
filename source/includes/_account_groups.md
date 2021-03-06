## Subtenant Groups

Groups belonging to a subtenant can be managed by the master account.

<!--
## Get All Groups for Subtenant
-->

```shell
curl "$MORPHEUS_API_URL/api/accounts/20/groups" \
  -H "Authorization: BEARER $MORPHEUS_API_TOKEN"
```

> The above command returns JSON structured like this:

```json
{
  "groups": [
    {
      "id": 365,
      "name": "testgroup",
      "code": "testgroup",
      "location": "West",
      "accountId": 20,
      "visibility": "public",
      "active": true,
      "dateCreated": "2018-03-20T20:34:22+0000",
      "lastUpdated": "2018-03-31T18:32:56+0000",
      "zones": [
        {
          "id": 32,
          "name": "test-google"
        },
        {
          "id": 33,
          "name": "test-vmware"
        }
      ]
    }
  ],
  "meta": {
    "offset": 0,
    "max": 25,
    "size": 1,
    "total": 1
  }
}
```

This endpoint retrieves all groups and a list of zones associated with the group by id.

### HTTP Request

`GET https://api.gomorpheus.com/api/accounts/:accountId/groups`

### URL Parameters

Parameter | Description
--------- | -----------
accountId | The ID of the subtenant account

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
phrase |  | Filter on partial match of name or location
name |  | Filter on exact match of name
lastUpdated |  | A date filter, restricts query to only load groups updated more recent or equal to the date specified

## Get a Specific Group for Subtenant

```shell
curl "$MORPHEUS_API_URL/api/accounts/20/groups/365" \
  -H "Authorization: BEARER $MORPHEUS_API_TOKEN"
```

> The above command returns JSON structured like this:

```json
{
  "group": {
      "id": 365,
      "name": "testgroup",
      "code": "testgroup",
      "location": "West",
      "accountId": 20,
      "visibility": "public",
      "active": true,
      "dateCreated": "2018-03-20T20:34:22+0000",
      "lastUpdated": "2018-03-31T18:32:56+0000",
      "zones": [
        {
          "id": 32,
          "name": "test-google"
        },
        {
          "id": 33,
          "name": "test-vmware"
        }
      ]
    }
}
```

This endpoint retrieves a specific group.


### HTTP Request

`GET https://api.gomorpheus.com/api/accounts/:accountId/groups/:id`

### URL Parameters

Parameter | Description
--------- | -----------
accountId | The ID of the subtenant account
id | The ID of the group to retrieve

## Create a Group for Subtenant

```shell
curl -XPOST "$MORPHEUS_API_URL/api/accounts/20/groups" \
  -H "Authorization: BEARER $MORPHEUS_API_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"group":{
    "name": "My Group",
    "description": "My description",
    "location": "West"
  }}'
```

> The above command returns JSON structured like getting a single group:

### HTTP Request

`POST https://api.gomorpheus.com/api/accounts/:accountId/groups`

### URL Parameters

Parameter | Description
--------- | -----------
accountId | The ID of the subtenant account

### JSON Parameters

Parameter | Default | Description
--------- | ------- | -----------
name      |  | A unique name scoped to the subtenant for the group
description |  | Optional description field if you want to put more info there
code      |  | Optional code for use with policies
location  |  | Optional location argument for the group

## Updating a Group for Subtenant

```shell
curl -XPUT "$MORPHEUS_API_URL/api/accounts/20/groups/365" \
  -H "Authorization: BEARER $MORPHEUS_API_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"group":{
    "name": "My Group",
    "description": "My description",
    "location": "West"
  }}'
```

> The above command returns JSON structured like getting a single group:

### HTTP Request

`PUT https://api.gomorpheus.com/api/accounts/:accountId/groups/:id`

### URL Parameters

Parameter | Description
--------- | -----------
accountId | The ID of the subtenant account
id | The ID of the group

### JSON Parameters

Parameter | Default | Description
--------- | ------- | -----------
name      |  | A unique name scoped to the subtenant for the group
description |  | Optional description field if you want to put more info there
code      |  | Optional code for use with policies
location  |  | Optional location for the group

## Updating Group Zones for Subtenant

```shell
curl -XPUT "$MORPHEUS_API_URL/api/accounts/20/groups/365/update-zones" \
  -H "Authorization: BEARER $MORPHEUS_API_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"group":{
    "zones": [
      {"id": 32}, {"id": 33}, {"id": 34}
    ]
  }}'
```

> The above command returns JSON Structured like this:

```json
{
  "success": true
}
```

This will update the zones that are assigned to the group.
Any zones that are not passed in the `zones` parameter will be removed from the group.

### HTTP Request

`PUT https://api.gomorpheus.com/api/accounts/:id/groups/:groupId/update-zones`

### JSON Parameters

Parameter | Default | Description
--------- | ------- | -----------
zones      |  | An array of all the zones assigned to this group.


## Delete a Group for Subtenant

```shell
curl -XDELETE "$MORPHEUS_API_URL/api/accounts/20/groups/365" \
  -H "Authorization: BEARER $MORPHEUS_API_TOKEN"
```

> The above command returns JSON Structured like this:

```json
{
  "success": true
}
```

### HTTP Request

`DELETE https://api.gomorpheus.com/api/accounts/:id/groups/:groupId`

If a group has zones or servers still tied to it, a delete action will fail
