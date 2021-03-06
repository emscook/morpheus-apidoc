# File Templates

Provides API interfaces for managing file templates within Morpheus.

A File Template may also be referred to as a *Container Template* or *containerTemplate*.

## Get All File Templates

```shell
curl "$MORPHEUS_API_URL/api/library/container-templates" \
  -H "Authorization: BEARER $MORPHEUS_API_TOKEN"
```

> The above command returns JSON structured like this:

```json
{
  "containerTemplates": [
    {
      "id": 83,
      "code": "b94bb003-31c4-418a-a067-562fa58d0dea",
      "account": {
        "id": 1,
        "name": "root"
      },
      "name": "testfile.txt",
      "fileName": "testfile.txt",
      "filePath": "/tmp",
      "templateType": null,
      "templatePhase": "preProvision",
      "template": "# this is a test file template\ntest:",
      "category": null,
      "settingCategory": null,
      "settingName": null,
      "autoRun": true,
      "runOnScale": false,
      "runOnDeploy": false,
      "fileOwner": null,
      "fileGroup": null,
      "permissions": null,
      "dateCreated": "2018-05-23T09:42:51Z",
      "lastUpdated": "2018-05-23T09:46:56Z"
    }
  ],
  "meta": {
    "size": 25,
    "total": 119,
    "max": 25,
    "offset": 0
  }
}
```

This endpoint retrieves all file templates.

The value of `template` will be masked as `************` for system owned file templates.

### HTTP Request

`GET https://api.gomorpheus.com/api/library/container-templates`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
max | 25 | Max number of results to return
offset | 0 | Offset of records you want to load
sort | name | Sort order
direction | asc | Sort direction, use 'desc' to reverse sort
phrase |  | Name, fileName, category and settingCategory, restricts query to only load file templates which contain the phrase specified
name |  | Name filter, restricts query to only load file template matching name specified
fileName |  | Filename filter, restricts query to only load file template matching fileName specified


## Get a Specific File Template

```shell
curl "$MORPHEUS_API_URL/api/library/container-templates/27" \
  -H "Authorization: BEARER $MORPHEUS_API_TOKEN"
```

> The above command returns JSON structured like this:

```json
{
  "containerTemplate": {
    "id": 27,
    "code": "nginx-1.9",
    "account": null,
    "name": "Nginx Config",
    "fileName": "default.conf",
    "filePath": "/etc/nginx/conf.d",
    "templateType": null,
    "templatePhase": "preProvision",
    "template": "************",
    "category": null,
    "settingCategory": "nginx",
    "settingName": "siteConf",
    "autoRun": true,
    "runOnScale": null,
    "runOnDeploy": null,
    "fileOwner": null,
    "fileGroup": null,
    "permissions": null,
    "dateCreated": "2016-08-27T19:26:15Z",
    "lastUpdated": "2019-10-02T00:31:54Z"
  }
}
```

This endpoint retrieves a specific file template.

The value of `template` will be masked as `************` for system owned file templates.

### HTTP Request

`GET https://api.gomorpheus.com/api/library/container-templates/:id`

### URL Parameters

Parameter | Description
--------- | -----------
id | ID of the file template


## Create a File Template

Use this command to create a file template.

```shell
curl -XPOST "$MORPHEUS_API_URL/api/library/container-templates" \
  -H "Authorization: BEARER $MORPHEUS_API_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"containerTemplate": {
    "templatePhase": "provision",
    "name": "appconfig",
    "fileName": "appconfig.yml",
    "template": "# this is a test file template\ntest:"
  }
}'
```

> The above command returns JSON Structured like this:

```json
{
  "id": 104,
  "success": true
}
```

### HTTP Request

`POST https://api.gomorpheus.com/api/library/container-templates`

### JSON Parameters

Parameter | Required | Description
--------- | -------- | -----------
name | Y | File template name
fileName | Y | Filename for the file template
filePath | N | Path for the file template
category | N | Category
templatePhase | N | Template Phase, `provision`, `start`, etc.
template | N | Template content, that is, the file template content itself.
fileOwner | N | File Owner
settingName | N | Setting Name
settingCategory | N | Setting Category


## Update a File Template

Use this command to update an existing file template.

```shell
curl -XPUT "$MORPHEUS_API_URL/api/library/container-templates/:id" \
  -H "Authorization: BEARER $MORPHEUS_API_TOKEN"
  -H "Content-Type: application/json" \
  -d '{"containerTemplate": {
    "name":"appconfig.yml"
  }
}'
```

> The above command returns JSON structured like this:

```json
{
  "success": true
}
```

### HTTP Request

`PUT https://api.gomorpheus.com/api/library/container-templates/:id`

### URL Parameters

Parameter | Description
--------- | -----------
id | The ID of the file template

### JSON Parameters

Parameter | Required | Description
--------- | -------- | -----------
name | Y | File template name
fileName | Y | Filename for the file template
filePath | N | Path for the file template
category | N | Category
templatePhase | N | Template Phase, `provision`, `start`, etc.
template | N | Template content, that is, the file template content itself.
fileOwner | N | File Owner
settingName | N | Setting Name
settingCategory | N | Setting Category
 

## Delete a File Template

```shell
curl -XDELETE "$MORPHEUS_API_URL/api/library/container-templates/:id" \
  -H "Authorization: BEARER $MORPHEUS_API_TOKEN"
```

> The above command returns JSON structure like this:

```json
{
  "success": true
}
```

Will delete a file template 

### HTTP Request

`DELETE https://api.gomorpheus.com/api/library/container-templates/:id`

### URL Parameters

Parameter | Description
--------- | -----------
id | The ID of the file template
