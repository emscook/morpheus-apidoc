# Key Pairs

Morpheus provides a database for keeping track of Key Pairs in the system. These can be used for provisioning servers and auto assigning added keypairs.

<!--## Get All Key Pairs-->

```shell
curl "$MORPHEUS_API_URL/api/key-pairs"
  -H "Authorization: BEARER $MORPHEUS_API_TOKEN"
```

> The above command returns JSON structured like this:

```json
{
  "keyPairCount": 1,
  "keyPairs": [
    {
      "accountId": 1,
      "id": 2,
      "name": "Test",
      "privateKey": null,
      "publicKey": "ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDXhVj5Oe88bXPmNA32iZ0ijlgbTkeCgnTkLwDyGfOTBH56QR9gwU66B1mh+ceU/lm1jS0zNuHtGFiMabbL+7a+MgJ7HVuaV4CR2/a/cp1yEzvvuJE6IvoGzDiXIdafasdfxcvdfadfvcEyOn+TW16rbS6GR/IwuvS81GqSJ6Z5/IJh4R5IW5yzK6z6BTHtX+vQQN9xv60JmwBC1NO5UVps2KVDBSCildlNlPR4AFrtVYDPSjRmjvj3DjGnJ6YlgjFIgc23bk1t0pknocgkB+7QZrkt1ed6AWVojGTUo2B9Cd/MphCKfZ mykey"
    }
  ],
  "success": true
}
```

This endpoint retrieves all key pairs associated with the account.

### HTTP Request

`GET https://api.gomorpheus.com/api/key-pairs`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
lastUpdated |  | A date filter, restricts query to only load keypairs updated more recent or equal to the date specified
name |  | If specified will return an exact match keypair


## Get a Specific Key Pair


```shell
curl "$MORPHEUS_API_URL/api/key-pairs/2" \
  -H "Authorization: BEARER $MORPHEUS_API_TOKEN"
```

> The above command returns JSON structured like this:

```json
{
  "keyPair": {
    "accountId": 1,
    "id": 2,
    "name": "Test",
    "privateKey": null,
    "publicKey": "ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDXhVj5Oe88bXPmNA32iZ0ijlgbTkeCgnTkLwDyGfOTBH56QR9gwU66B1mh+ceU/lm1jS0zNuHtGFiMabbL+7a+MgJ7HVuaV4CR2/a/cp1yEzvvuJE6IvoGzDiXIdafasdfxcvdfadfvcEyOn+TW16rbS6GR/IwuvS81GqSJ6Z5/IJh4R5IW5yzK6z6BTHtX+vQQN9xv60JmwBC1NO5UVps2KVDBSCildlNlPR4AFrtVYDPSjRmjvj3DjGnJ6YlgjFIgc23bk1t0pknocgkB+7QZrkt1ed6AWVojGTUo2B9Cd/MphCKfZ mykey"
  },
  "success": true
}
```

This endpoint retrieves a specific key.


### HTTP Request

`GET https://api.gomorpheus.com/api/key-pairs/:id`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the key pair

## Create a KeyPair

```shell
curl -XPOST "$MORPHEUS_API_URL/api/key-pairs" \
  -H "Authorization: BEARER $MORPHEUS_API_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"keyPair":{
    "name": "My Key",
    "publicKey": "ssh-rsa",
    "privateKey": "privateKey Optional for most cases"
  }}'
```

> The above command returns JSON structured like getting a single keyPair: 

### HTTP Request

`POST https://api.gomorpheus.com/api/key-pairs`

### JSON Key Pair Parameters

Parameter | Default | Description
--------- | ------- | -----------
name      |  | A unique name scoped to your account for the key
publicKey |  | The public key pair value
privateKey |  | The private key pair value (optional)

**NOTE** The Public and Private key are stored in encrypted form in the database.

## Delete a Key Pair

```shell
curl -XDELETE "$MORPHEUS_API_URL/api/key-pairs/1" \
  -H "Authorization: BEARER $MORPHEUS_API_TOKEN"
```

> The above command returns JSON Structured like this:

```json
{
  "success": true
}
```


Will delete a key pair from the system and make it no longer usable.

<aside class="info">
If a key pair is actively in use, a delete will fail.
</aside>

### HTTP Request

`DELETE https://api.gomorpheus.com/api/key-pairs/:id`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the key pair
