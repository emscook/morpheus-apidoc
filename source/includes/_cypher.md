# Cypher

Cypher at its core is a secure Key/Value store. But what makes cypher useful is the ability to securely store or generate credentials to connect to your instances. Not only are these credentials encrypted but by using a cypher you don't have to burn in connection credentials between instances into your apps.

Cypher keys can be revoked, either through lease timeouts or manually. So even if somebody were to gain access to your keys you could revoke access to the keys and generate new ones for your applications.

<aside class="info">
<b>Deprecation notice.</b> The endpoint <code>/api/cypher/v1</code> is now deprecated and will be removed in the future. The new endpoint is </code>/api/cypher</code>.
</aside>

### Cypher Authentication

The Cypher API endpoints allow authentication via a special header or the standard [Authorization] header. Instead of an access token, an execution lease token can be used to authenticate.
An execution lease will be issued by Morpheus for certain tasks, such as Ansible, which can then use the token to read cypher keys.

Cypher has the following headers and url parameters available for authentication:

Name | Type | Description
--------- | ----------- | -----------
X-Cypher-Token | HTTP Header | An access token or an execution lease token.
X-Vault-Token | HTTP Header | An access token or an execution lease token.
X-Morpheus-Lease | HTTP Header | An execution lease token.
leaseToken | URL Parameter | An execution lease token.


## List Cypher Keys

```shell
curl -XLIST "$MORPHEUS_API_URL/api/cypher?list=true" \
  -H "Authorization: BEARER $MORPHEUS_API_TOKEN"
```

> The above command returns JSON structured like this:

```json
{
  "data": {
    "keys": [
      "password/15/mypassword",
      "secret/foo"
    ]
  },
  "cyphers": [
    {
      "itemKey": "password/15/mypassword",
      "leaseTimeout": 2764800000,
      "expireDate": "2019-03-23T10:17:52Z",
      "dateCreated": "2019-02-19T10:17:52Z",
      "lastUpdated": "2019-02-19T10:17:52Z",
      "lastAccessed": "2019-02-19T10:17:52Z"
    },
    {
      "itemKey": "secret/foo",
      "leaseTimeout": 2764800000,
      "expireDate": "2019-03-25T17:14:33Z",
      "dateCreated": "2019-02-21T17:14:33Z",
      "lastUpdated": "2019-02-21T17:14:33Z",
      "lastAccessed": "2019-02-21T17:14:33Z"
    }
  ],
  "meta": {
    "size": 2,
    "total": 2,
    "max": 25,
    "offset": 0
  }
}
```

This endpoint retrieves all cypher keys associated with the account, or user.

This endpoint is available http method `LIST`. The `GET` method can be used to list keys as well, by passing the query parameter `list=true`.

### HTTP Request

`LIST https://api.gomorpheus.com/api/cypher/:key?list=true`

### URL Parameters

Parameter | Description
--------- | -----------
key | If specified will match the start of the key.

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
list | Set to `true` for list behavior with HTTP `GET`.
phrase |  | If specified will match any part of key
key |  | If specified will return an exact match of key
max | 25 | Max number of results to return
offset | 0 | Offset of records you want to load
sort | key | Sort order
direction | asc | Sort direction, use 'desc' to reverse sort

## Read a Cypher Key


```shell
curl "$MORPHEUS_API_URL/api/cypher/secret/foo" \
  -H "Authorization: BEARER $MORPHEUS_API_TOKEN"
```

> The above command returns JSON structured like this:

```json
{
  "success": true,
  "data": {
    "foo":"bar",
    "briefing":"top secret info"
  },
  "type": "object",
  "lease_duration": 2764800,
  "cypher": {
    "itemKey": "secret/foo",
    "leaseTimeout": 2764800000,
    "expireDate": "2019-03-18T20:15:51Z",
    "dateCreated": "2019-02-14T20:15:51Z",
    "lastUpdated": "2019-02-14T20:15:51Z",
    "lastAccessed": "2019-02-14T20:15:51Z"
  }
}
```

This endpoint retrieves a specific cypher key.
The value of the key is decrypted and returned as `data`.
It may be a String or an object with many `{"key":"value"}` pairs.
The type depends on the cypher mount's capabilities and what type of data was written to the key.  For example the `secret/` mount allows either a string or an object, while the `password/` mount will always store and return a string.

### HTTP Request

`GET https://api.gomorpheus.com/api/cypher/:key`

### URL Parameters

Parameter | Description
--------- | -----------
key | The full cypher key including the mount prefix.

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
ttl | `0` | Time to Live. The lease duration in seconds, or a human readable format eg. `15m`, `8h`, `7d`. The default is `0` meaning Never expires. This only is applied if the cypher does not yet exist and is created.
readonly | false | Do not automatically create a key. This only applies to mount types `uuid`, `key`, `password`.

## Read a Cypher with Lease

```shell
curl "$MORPHEUS_API_URL/api/cypher/password/15/mypassword" \
  -H "X-Lease-Token: 6f4d3563-22ef-404f-8b81-c13d093cd55a"
```

> The above command returns JSON structured like reading a key with normal authentication:

```
{
  "data": "B[,t;ng[5[lg&th",
  "type": "string",
  "lease_duration": 432000000,
  "cypher": {
    "itemKey": "password/15/mypassword",
    "leaseTimeout": 432000000,
    "expireDate": "2019-02-26T21:35:20Z",
    "dateCreated": "2019-02-21T21:35:20Z",
    "lastUpdated": "2019-02-21T21:35:20Z",
    "lastAccessed": "2019-02-21T21:35:20Z"
  }
}
```

### HTTP Request

`GET https://api.gomorpheus.com/api/cypher/:key`


### URL Parameters

Parameter | Default | Description
--------- | ------- | -----------
key | | The cypher key including the mount prefix.

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
ttl | `0` | Time to Live. The lease duration in seconds, or a human readable format eg. `15m`, `8h`, `7d`. The default is `0` meaning Never expires. This only is applied if the cypher does not yet exist and is created.

## Write a Cypher

```shell
curl -XPOST "$MORPHEUS_API_URL/api/cypher/secret/foo" \
  -H "Authorization: BEARER $MORPHEUS_API_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"foo":"bar", "zip":"zap"}'
```

> The above command returns JSON structured like readding a cypher key:.

This endpoint will create or update a cypher key.

### HTTP Request

`POST https://api.gomorpheus.com/api/cypher/:key`

This endpoint is available via both methods `POST` and `PUT`.

### URL Parameters

Parameter | Description
--------- | -----------
key | The full cypher key including the mount prefix.

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
ttl | 0 | Time to Live. The lease duration in seconds, or a human readable format eg. '15m', 8h, '7d'.
value |  | The secret value to be stored. Only required for certain mounts. Some mounts generate their own value and do not require a value to be passed. eg. `uuid`, `key` and `password`.
type |  | The type of data being stored, `string` or `object`. The data type depends on the cypher mount being used. Most mounts use `string` as their data type, but `secret` uses `object` by default. You can store a string instead by passing `type=string`. This means the `data` value returned by the API will be a string instead of an object.

### JSON Parameters

The following parameters are available under the root context of the JSON body.

Parameter | Default | Description
--------- | ------- | -----------
ttl | `0` | Time to Live. The lease duration in seconds, or a human readable format eg. `15m`, `8h`, `7d`. The default is `0` meaning Never expires. This only is applied if the cypher does not yet exist and is created.
value | | The secret value to be stored. This is only parsed if `type` is passed as `string`.

The `secret` mount is capable of storing the entire JSON object as key=value pairs, or just a single string. To store a string instead, use the `value` query parameter instead of JSON, or pass `type=string`.

There are a couple of special keys that the API will look for in the payload.

The `ttl` key is a special key that if present in the payload will be parsed and used as the `ttl` parameter (lease duration in seconds).

The `value` key is a special key that if present in the payload will be parsed and used as the secret data (instead of the entire payload). This is true when `type=string`.

#### Key

The *key* includes a *mount* prefix separated by a */*. For example, the key `secret/foo` uses the `secret` mount.

##### Available mounts

Keys can have different behaviors depending on the specified mount engine.

Mount | Description | Example
--------- | ------- | ---------
password | Generates a secure password of specified character length in the key pattern (or 15) with symbols, numbers, upper case, and lower case letters (i.e. password/15/mypass generates a 15 character password). | password/15/mypass
tfvars | This is a module to store a tfvars file for terraform. | tfvars/mytfvar
secret | This is the standard secret module that stores a key/value in encrypted form. Capable of storing entire JSON object or a String. | secret/foo
uuid | Returns a new UUID by key name when requested and stores the generated UUID by key name for a given lease timeout period. | uuid/autoMac1
key | Generates a Base 64 encoded AES Key of specified bit length in the key pattern (i.e. key/128/mykey generates a 128-bit key) | key/128/mykey

#### Lease Time

Quick MS Time Reference:

Time | MS
--------- | -------
Day      | 86400000
Week      | 604800000
Month (30 days)      |  2592000000
Year      | 31536000000

## Delete a Cypher

```shell
curl -XDELETE "$MORPHEUS_API_URL/api/cypher/secret/foo" \
  -H "Authorization: BEARER $MORPHEUS_API_TOKEN"
```

> The above command returns JSON Structured like this:

```json
{
  "success": true
}
```

Will delete a cypher from the system and make it no longer usable.

### HTTP Request

`DELETE https://api.gomorpheus.com/api/cypher/:key`

### URL Parameters

Parameter | Description
--------- | -----------
key | The full cypher key including the mount prefix.
