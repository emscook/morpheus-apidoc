## Whoami

```shell
curl "$MORPHEUS_API_URL/api/whoami" \
  -H "Authorization: BEARER $MORPHEUS_API_TOKEN"
```

> The above command returns JSON structured like this:

```json
{
  "user": {
    "id": 1,
    "accountId": 1,
    "username": "test",
    "displayName": "Test U",
    "email": "testuser@morpheusdata.com",
    "firstName": "Test",
    "lastName": "User",
    "dateCreated": "2016-08-27T19:28:09+0000",
    "lastUpdated": "2020-01-07T05:19:20+0000",
    "enabled": true,
    "accountExpired": false,
    "accountLocked": false,
    "passwordExpired": false,
    "loginCount": 1575,
    "loginAttempts": 0,
    "lastLoginDate": "2020-01-07T05:19:20+0000",
    "roles": [
      {
        "id": 5,
        "authority": "Standard User",
        "description": "A basic user role"
      }
    ],
    "account": {
      "id": 1,
      "name": "root"
    },
    "windowsUsername": "morphtest",
    "linuxUsername": "morphtest"
  },
  "isMasterAccount": true,
  "permissions": [
    {
      "name": "Provisioning: Blueprints",
      "code": "app-templates",
      "access": "full"
    },
    {
      "name": "Provisioning: Apps",
      "code": "apps",
      "access": "full"
    },
    {
      "name": "Logs",
      "code": "logs",
      "access": "full"
    },
    {
      "name": "Monitoring",
      "code": "monitoring",
      "access": "full"
    },
    {
      "name": "Operations: Wiki",
      "code": "operations-wiki",
      "access": "full"
    },
    {
      "name": "Provisioning: Instances",
      "code": "provisioning",
      "access": "full"
    },
    {
      "name": "Operations: Reports",
      "code": "reports",
      "access": "full"
    },
    {
      "name": "Provisioning: Tasks - Script Engines",
      "code": "task-scripts",
      "access": "full"
    },
    {
      "name": "Provisioning: Tasks",
      "code": "tasks",
      "access": "full"
    },
    {
      "name": "Remote Console: Auto Login",
      "code": "terminal-access",
      "access": "yes"
    },
    {
      "name": "Remote Console",
      "code": "terminal",
      "access": "full"
    },
    {
      "name": "Provisioning: Blueprints - Terraform",
      "code": "terraform-template",
      "access": "full"
    },
    {
      "name": "Provisioning: Virtual Images",
      "code": "virtual-images",
      "access": "full"
    }
  ],
  "appliance": {
    "buildVersion": "4.1.2"
  }
}
```

Provides API to retrieve information about yourself, including your roles and permissions.

The appliance build version is also returned.

### HTTP Request

`GET https://api.gomorpheus.com/api/whoami`


