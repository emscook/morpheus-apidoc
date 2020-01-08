# Virtual Images

Virtual Images can be managed via the API.


## Get List of Virtual Images

```shell
curl "$MORPHEUS_API_URL/api/virtual-images"
  -H "Authorization: BEARER $MORPHEUS_API_TOKEN"
```

> The above command returns JSON structured like this:

```json
{
  "virtualImages": [
    {
      "id": 764,
      "name": "testimage",
      "description": null,
      "ownerId": 1,
      "imageType": "vmware",
      "userUploaded": true,
      "userDefined": false,
      "systemImage": false,
      "isCloudInit": true,
      "sshUsername": "root",
      "sshPassword": "****",
      "sshKey": null,
      "osType": {
        "id": 9,
        "name": "ubuntu 64-bit",
        "description": null,
        "vendor": "canonical",
        "category": "ubuntu",
        "osFamily": "debian",
        "osVersion": "all",
        "bitCount": 64,
        "platform": "linux"
      },
      "minDisk": null,
      "minRam": null,
      "rawSize": 56077536,
      "trialVersion": false,
      "virtioSupported": true,
      "isAutoJoinDomain": false,
      "vmToolsInstalled": true,
      "installAgent": true,
      "isForceCustomization": false,
      "isSysprep": false,
      "userData": null,
      "storageProvider": {
        "id": 2,
        "name": "local-images"
      },
      "externalId": null,
      "visibility": "private",
      "accounts": [
        {
          "id": 1,
          "name": "root"
        }
      ]
    }
  ],
  "meta": {
    "offset": 0,
    "max": 25,
    "size": 25,
    "total": 43
  }
}
```

This endpoint retrieves a list of virtual images for the specified filter.

### HTTP Request

`GET https://api.gomorpheus.com/api/virtual-images`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
max | 25 | Max number of results to return
offset | 0 | Offset of records you want to load
name |  | Filter by name
phrase |  | Filter by wildcard search of name
lastUpdated |  | Date filter, restricts query to only records with a timestamp is more recent or equal to the date specified
filterType | "User" | Filter by type, "User", "System" or "All"
imageType |  | Filter by image type code, "vmware", "ami", etc

## Get a Specific Virtual Image


```shell
curl "$MORPHEUS_API_URL/api/virtual-images/764" \
  -H "Authorization: BEARER $MORPHEUS_API_TOKEN"
```

> The above command returns JSON structured like this:

```json
{
  "virtualImage": {
    "id": 764,
    "name": "testimage",
    "description": null,
    "ownerId": 1,
    "imageType": "vmware",
    "userUploaded": true,
    "userDefined": false,
    "systemImage": false,
    "isCloudInit": true,
    "sshUsername": "root",
    "sshPassword": "****",
    "sshKey": null,
    "osType": {
      "id": 9,
      "name": "ubuntu 64-bit",
      "description": null,
      "vendor": "canonical",
      "category": "ubuntu",
      "osFamily": "debian",
      "osVersion": "all",
      "bitCount": 64,
      "platform": "linux"
    },
    "minDisk": null,
    "minRam": null,
    "rawSize": 56077536,
    "trialVersion": false,
    "virtioSupported": true,
    "isAutoJoinDomain": false,
    "vmToolsInstalled": true,
    "isForceCustomization": false,
    "isSysprep": false,
    "userData": null,
    "storageProvider": {
      "id": 2,
      "name": "testdrive2"
    },
    "externalId": null,
    "visibility": "private",
    "accounts": [
      {
        "id": 1,
        "name": "root"
      }
    ]
  },
  "cloudFiles": [
    {
      "name": "testimage.vmdk",
      "size": 1034592
    },
    {
      "name": "testimage.ovf",
      "size": 28038768
    }
  ]
}
```

This endpoint retrieves a specific virtual image and its files.

### HTTP Request

`GET https://api.gomorpheus.com/api/virtual-images/:id`

### URL Parameters

Parameter | Description
--------- | -----------
id | The ID of the virtual image

## Create a Virtual Image

```shell
curl -XPOST "$MORPHEUS_API_URL/api/virtual-images" \
  -H "Authorization: BEARER $MORPHEUS_API_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"virtualImage":{
    "name": "testimage2",
    "imageType": "vmware",
    "isCloudInit": true,
    "installAgent": true,
    "sshUsername": "root",
    "sshPassword": "mygoodpassword123",
    "sshKey": null,
    "osType": {
      "id": 9
    },
    "virtioSupported": true,
    "vmToolsInstalled": true,

  }}'
```

> The above command returns JSON structured like getting a single virtual image.

This endpoint creates a new virtual image, without any files yet.

### HTTP Request

`POST https://api.gomorpheus.com/api/virtual-images`

### JSON Virtual Image Parameters

Parameter | Default | Description
--------- | ------- | -----------
name  |  | A name for the virtual image
imageType  |  | Code of image type. eg. vmware, ami, etc.
storageProvider |  | A Map containing the id of the Storage Provider
isCloudInit | false | Cloud Init Enabled? true or false
userData |  | Cloud-Init User Data, a bash script
installAgent | false | Install Agent? true or false
sshUsername |  | SSH Username
sshPassword |  | SSH Password
sshKey |  | SSK Key
osType |  | A Map containing the id of the OS Type. This can also be passed as a string (code or name) instead.
visibility | "private" | private or public
accounts  |  | Array of tenant account ids that are allowed access.
isAutoJoinDomain | false | Auto Join Domain?
virtioSupported | true | VirtIO Drivers Loaded?
vmToolsInstalled | true | VM Tools Installed?
isForceCustomization | false | Force Guest Customization?
trialVersion | false | Trial Version
isSysprep | false | Sysprep Enabled?

## Upload Virtual Image File

```shell
curl -XPOST "$MORPHEUS_API_URL/api/virtual-images/765/upload?filename=disk-0.vmdk" \
  -H "Authorization: BEARER $MORPHEUS_API_TOKEN" \
  --data-binary '@/path/to/file'
```

> The above command returns JSON structure like this:

```json
{
  "success": true
}
```

This will upload the file and associate it to the Virtual Image.

### HTTP Request

`POST https://api.gomorpheus.com/api/virtual-images/:id/upload`

### URL Parameters

Parameter | Description
--------- | -----------
id | The ID of the virtual image

### Query Parameters

Parameter | Description
--------- | -----------
url | Download the file from a remote url. This can be used instead of uploading a local file.
filename | Specify a filename for new file.

## Remove Virtual Image File

```shell
curl -XDELETE "$MORPHEUS_API_URL/api/virtual-images/765/files?filename=testimage.ovf" \
  -H "Authorization: BEARER $MORPHEUS_API_TOKEN"
```

> The above command returns JSON structure like this:

```json
{
  "success": true
}
```

### HTTP Request

`DELETE https://api.gomorpheus.com/api/virtual-images/:id/files?filename=`

### URL Parameters

Parameter | Description
--------- | -----------
id | The ID of the virtual image

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
filename  |  | The name of the file to be deleted

## Update a Virtual Image

```shell
curl -XPUT "$MORPHEUS_API_URL/api/virtual-images/764" \
  -H "Authorization: BEARER $MORPHEUS_API_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"virtualImage":{
    "installAgent": true,
    "sshUsername": "root",
    "sshPassword": "mygreatpassword12345!",
    "sshKey": null,
    "osType": {
      "id": 9
    },
    "virtioSupported": true,
    "vmToolsInstalled": true,

  }}'
```

> The above command returns JSON structured like getting a single virtual image.

This endpoint updates an existing virtual image.

### HTTP Request

`PUT https://api.gomorpheus.com/api/virtual-images/:id`

### URL Parameters

Parameter | Description
--------- | -----------
id | The ID of the virtual image

### JSON Virtual Image Parameters

The same parameters as [Create a Virtual Image](#Create-a-Virtual-Image) are supported.

## Delete a Virtual Image

```shell
curl -XDELETE "$MORPHEUS_API_URL/api/virtual-images/765" \
  -H "Authorization: BEARER $MORPHEUS_API_TOKEN"
```

> The above command returns JSON structure like this:

```json
{
  "success": true
}
```

Will delete a virtual image and any associated files.

### HTTP Request

`DELETE https://api.gomorpheus.com/api/virtual-images/:id`

### URL Parameters

Parameter | Description
--------- | -----------
id | The ID of the virtual image
