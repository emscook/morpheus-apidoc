# Tenants

Provides API interfaces for managing the creation and modification of tenants within Morpheus. Typically this is only accessible by users of the Master Tenant.

<!--
  JD: uhh this "(Typically only accessible by the Master Account)." needs to be investigated. non master account users should not be able to edit other tenant accounts, only their own...
-->

A Tenant may also be referred to as an *Account* or *account*.

## Get All Tenants

```shell
curl "$MORPHEUS_API_URL/api/accounts" \
  -H "Authorization: BEARER $MORPHEUS_API_TOKEN"
```

> The above command returns JSON structured like this:

```json
{
  "accounts": [
    {
      "id": 1,
      "name": "Master",
      "subdomain": "subdomain",
      "description": "The master tenant",
      "subdomain": null,
      "currency": "USD",
      "lastUpdated": "2015-11-10T18:58:55+0000",
      "dateCreated": "2015-11-10T18:58:55+0000",
      "role": {
        "id": 1,
        "authority": "System Admin",
        "description": "Super User"
      },
      "active": true
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

This endpoint retrieves all tenants.

### HTTP Request

`GET https://api.gomorpheus.com/api/accounts`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
max | 25 | Max number of results to return
offset | 0 | Offset of records you want to load
sort | name | Sort order
direction | asc | Sort direction, use 'desc' to reverse sort
phrase |  | Filter by matching name or description
name |  | Filter by name
lastUpdated |  | Date filter, restricts query to only load tenants updated more recently than the date specified


## Get a Specific Tenant

```shell
curl "$MORPHEUS_API_URL/api/accounts/1" \
  -H "Authorization: BEARER $MORPHEUS_API_TOKEN"
```

> The above command returns JSON structured like this:

```json
{
  "account": {
    "id": 1,
    "name": "Master",
    "subdomain": "subdomain",
    "description": "The master tenant",
    "subdomain": null,
    "currency": "USD",
    "externalId": null,
    "lastUpdated": "2015-11-10T18:58:55+0000",
    "dateCreated": "2015-11-10T18:58:55+0000",
    "role": {
      "id": 1,
      "authority": "System Admin",
      "description": "Super User"
    },
    "active": true
  }
}
```

This endpoint will retrieve a specific account by ID.

### HTTP Request

`GET https://api.gomorpheus.com/api/accounts/:id`

## Create a Tenant

```shell
curl -XPOST "$MORPHEUS_API_URL/api/accounts" \
  -H "Authorization: BEARER $MORPHEUS_API_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"account":{
    "name": "My Account",
    "description": "My description",
    "subdomain": "myaccount",
    "role": {"id": 2}
  }}'
```

> The above command returns JSON structured like getting a single account:

### HTTP Request

`POST https://api.gomorpheus.com/api/accounts`

### JSON Account Parameters

Parameter | Default | Description
--------- | ------- | -----------
name      |  | A unique name for the account
description |  | Optional description field if you want to put more info there
subdomain |  | Sets the custom login url or login prefix for logging into a sub-tenant user.
role      | Account Admin | A nested id of the default base role for the account. See [Get Available Roles for a Tenant](#get-available-roles-for-a-tenant).

## Updating a Tenant

```shell
curl -XPUT "$MORPHEUS_API_URL/api/accounts/2" \
  -H "Authorization: BEARER $MORPHEUS_API_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"account":{
    "name": "My Tenant",
    "description": "My new description",
    "subdomain": "mytenant",
    "role": {"id": 2}
  }}'
```

> The above command returns JSON structured like getting a single account:

### HTTP Request

`PUT https://api.gomorpheus.com/api/accounts/:id`

### JSON Account Parameters

Parameter | Default | Description
--------- | ------- | -----------
name      |  | A unique name for the account
description |  | Optional description field if you want to put more info there
subdomain |  | Sets the custom login url or login prefix for logging into a sub-tenant user.
role      |  | A nested id of the default base role for the account
active |  | Set to false to deactvate the account

## Delete a Tenant

```shell
curl -XDELETE "$MORPHEUS_API_URL/api/accounts/1" \
  -H "Authorization: BEARER $MORPHEUS_API_TOKEN"
```

> The above command returns JSON Structured like this:

```json
{
  "success": true
}
```

If a tenant still has users or instances tied to it, The delete will fail.

<aside class="info">This restriction should be lifted in a forthcoming API release</aside>

### HTTP Request

`DELETE https://api.gomorpheus.com/api/accounts/:id`


## Get Available Roles for a Tenant

```shell
curl "$MORPHEUS_API_URL/api/accounts/available-roles" \
  -H "Authorization: BEARER $MORPHEUS_API_TOKEN"
```

> The above command returns JSON structured like this:

```json
{
  "roles": [
     {
      "id": 1,
      "authority": "System Admin",
      "name": "System Admin",
      "description": "Super User",
      "roleType": null,
      "owner": null
    },
    {
      "id": 2,
      "authority": "Tenant Admin",
      "name": "Tenant Admin",
      "description": "Tenant Role Template",
      "roleType": "account",
      "owner": null
    }
  ]
}
```

This endpoint will retrieve a list of roles that can be assigned as the base role for a tenant account.  These are roles that have `roleType` set to `account` or `null`.

### HTTP Request

`GET https://api.gomorpheus.com/api/accounts/available-roles`
