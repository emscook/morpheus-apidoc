# Option Types

Provides API interfaces for managing Library: Option Types within Morpheus.

## Get All Option Types

```shell
curl "$MORPHEUS_API_URL/api/library/option-types" \
  -H "Authorization: BEARER $MORPHEUS_API_TOKEN"
```

> The above command returns JSON structured like this:

```json
{
  "optionTypes": [
    {
      "id": 811,
      "name": "DB Version",
      "description": "Database Version",
      "code": null,
      "fieldName": "dbVersion",
      "fieldLabel": "DB Version",
      "fieldContext": "config.customOptions",
      "fieldGroup": null,
      "fieldClass": null,
      "fieldAddOn": null,
      "fieldComponent": null,
      "placeHolder": "yourversion",
      "helpBlock": null,
      "defaultValue": null,
      "optionSource": null,
      "optionList": null,
      "type": "text",
      "advanced": false,
      "required": false,
      "editable": false,
      "creatable": true,
      "config": {
      },
      "displayOrder": 0,
      "wrapperClass": null,
      "enabled": true,
      "noBlank": false,
      "dependsOnCode": null,
      "contextualDefault": false
    },
    {
      "id": 1236,
      "name": "myselect",
      "description": "a select option type",
      "code": "myselect",
      "fieldName": "myselect",
      "fieldLabel": "My Select",
      "fieldContext": "config.customOptions",
      "fieldGroup": null,
      "fieldClass": null,
      "fieldAddOn": null,
      "fieldComponent": null,
      "placeHolder": null,
      "helpBlock": null,
      "defaultValue": null,
      "optionSource": "list",
      "optionList": {
        "id": 51,
        "name": "my groups"
      },
      "type": "select",
      "advanced": false,
      "required": false,
      "editable": false,
      "creatable": true,
      "config": {
      },
      "displayOrder": 3,
      "wrapperClass": null,
      "enabled": true,
      "noBlank": false,
      "dependsOnCode": null,
      "contextualDefault": false
    }
  ],
  "meta": {
    "offset": 0,
    "max": 25,
    "size": 2,
    "total": 2
  }
}
```

This endpoint retrieves all option types.

### HTTP Request

`GET https://api.gomorpheus.com/api/library/option-types`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
max | 25 | Max number of results to return
offset | 0 | Offset of records you want to load
sort | name | Sort order
direction | asc | Sort direction, use 'desc' to reverse sort
phrase |  | Name, code or description, restricts query to only load option types which contain the phrase specified
name |  | Name filter, restricts query to only load type matching name specified
code |  | Code filter, restricts query to only load type matching code specified
fieldName |  | Field Name filter, restricts query to only load type matching fieldName specified
fieldContext |  | Field Context filter, restricts query to only load type matching fieldContext specified
fieldLabel |  | Field Label filter, restricts query to only load type matching fieldLabel specified


## Get a Specific Option Type

```shell
curl "$MORPHEUS_API_URL/api/library/option-types/811" \
  -H "Authorization: BEARER $MORPHEUS_API_TOKEN"
```

> The above command returns JSON structured like this:

```json
{
  "optionType": {
    "id": 811,
    "name": "DB Version",
    "description": "Database Version",
    "code": null,
    "fieldName": "dbVersion",
    "fieldLabel": "DB Version",
    "fieldContext": "config.customOptions",
    "fieldGroup": null,
    "fieldClass": null,
    "fieldAddOn": null,
    "fieldComponent": null,
    "placeHolder": "yourversion",
    "helpBlock": null,
    "defaultValue": null,
    "optionSource": null,
    "optionList": null,
    "type": "text",
    "advanced": false,
    "required": false,
    "editable": false,
    "creatable": true,
    "config": {
    },
    "displayOrder": 0,
    "wrapperClass": null,
    "enabled": true,
    "noBlank": false,
    "dependsOnCode": null,
    "contextualDefault": false
  }
}
```

This endpoint retrieves a specific option type.

### HTTP Request

`GET https://api.gomorpheus.com/api/library/option-types/:id`

### URL Parameters

Parameter | Description
--------- | -----------
id | ID of the option type


## Create an Option Type

Use this command to create an option type.

```shell
curl -XPOST "$MORPHEUS_API_URL/api/library/option-types" \
  -H "Authorization: BEARER $MORPHEUS_API_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"optionType": {
       "name": "Test Input",
       "type": "text",
       "description": "A test option type",
       "fieldName": "testinput",
       "fieldLabel": "Test Input"
     }}'
```

> The above command returns JSON Structured like this:

```json
{
  "id": 104,
  "success": true
}
```

### HTTP Request

`POST https://api.gomorpheus.com/api/library/option-types`

### JSON Parameters

Parameter | Required | Description
--------- | -------- | -----------
name | Y | Name
description | N | Description
fieldName | N | Field Name, the name for user input. This along with fieldContext determines the configuration property name.
type | N | Type, the type of input. eg. `text`, `checkbox`, `select`, etc. Default is `text`.
fieldLabel | N | Field Label, the label for user input.
placeHolder | N | Placeholder
defaultValue | N | Default Value
required | N | Required, Default is `false`.
exportMeta | N | Export as Tag, Default is `false`.
optionList.id | N | ID of [Option List](#option-lists). For use with type `select`, this will set optionSource to `list`.

## Update an Option Type

Use this command to update an existing option type.

```shell
curl -XPUT "$MORPHEUS_API_URL/api/library/option-types/:id" \
  -H "Authorization: BEARER $MORPHEUS_API_TOKEN"
  -H "Content-Type: application/json" \
  -d '{"optionType": {
        "description": "An example input"
      }}
```

> The above command returns JSON structured like this:

```json
{
  "success": true
}
```

### HTTP Request

`PUT https://api.gomorpheus.com/api/library/option-types/:id`

### URL Parameters

Parameter | Description
--------- | -----------
id | The ID of the option type

### JSON Parameters

Parameter | Required | Description
--------- | -------- | -----------
name | Y | Name
description | N | Description
fieldName | N | Field Name, the name for user input. This along with fieldContext determines the configuration property name.
type | N | Type, the type of input. eg. `text`, `checkbox`, `select`, etc. Default is `text`.
fieldLabel | N | Field Label, the label for user input.
placeHolder | N | Placeholder
defaultValue | N | Default Value
required | N | Required, Default is `false`.
exportMeta | N | Export as Tag, Default is `false`.
optionList.id | N | ID of [Option List](#option-lists). For use with type `select`, this will set optionSource to `list`.

## Delete an Option Type

```shell
curl -XDELETE "$MORPHEUS_API_URL/api/library/option-types/:id" \
  -H "Authorization: BEARER $MORPHEUS_API_TOKEN"
```

> The above command returns JSON structure like this:

```json
{
  "success": true
}
```

Will delete an option type 

### HTTP Request

`DELETE https://api.gomorpheus.com/api/library/option-types/:id`

### URL Parameters

Parameter | Description
--------- | -----------
id | The ID of the option type
