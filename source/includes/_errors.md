## Errors

When the Morpheus API encounters an error, the response will have an HTTP status of **400** of greater, instead of **200 OK**.  The error response body contains JSON with information to help troubleshoot the error.

### 400 Bad Request

```shell
curl -XPOST "$MORPHEUS_API_URL/api/contacts" \
  -H "Authorization: BEARER $MORPHEUS_API_TOKEN" \
  -d '{"contact":{"name":"example"}}'
```

> The above command returns HTTP 400 and JSON structured like this:

```json
{
  "success": false,
  "msg": "Unable to save contact",
  "errors": {
    "email": "Please enter a valid email address"
  }
}
```

This error is returned if your request is invalid. Usually this is because a parameter is missing or the value is invalid. Try modifying your payload and retrying the request.

### 401 Unauthorized

```shell
curl "$MORPHEUS_API_URL/api/instances"
```

> The above command returns HTTP 401 and JSON structured like this:

```json
{
  "error": "unauthorized",
  "error_description": "Full authentication is required to access this resource"
}
```

The unauthorized error will be encountered unless you pass the authorization header.

<!-- ### 401 Invalid Token -->

```shell
curl "$MORPHEUS_API_URL/api/instances" \
-H "Authorization: BEARER BOGUS_TOKEN"
```

> The above command returns HTTP 401 and JSON structured like this:

```json
{
  "error": "invalid_token",
  "error_description": "Invalid access token: BOGUS_TOKEN"
}
```

The 401 error code is returned if your access token is invalid or expired.

### 403 Forbidden

```shell
curl "$MORPHEUS_API_URL/api/setup" \
  -H "Authorization: BEARER $MORPHEUS_API_TOKEN"
```

> The above command returns HTTP 403 and JSON structured like this:

```json
{
  "success": false,
  "msg": "You do not have permissions to access this api endpoint"
}
```

This error is seen if you try to access an endpoint without the required permissions.  

For this error example, use the token of user that does not have any admin permissions.

### 404 Not Found

```shell
curl "$MORPHEUS_API_URL/api/foobar" \
  -H "Authorization: BEARER $MORPHEUS_API_TOKEN"

```
> The above command returns HTTP 404 and JSON structured like this:

```json
{
  "success": false,
  "msg": "Unable to find api endpoint GET /api/foobar"
}
```


This error indicates the specified endpoint path does not exist. Check the URL of your request and try again.

<!-- ### 404 ID Not Found -->

```shell
curl "$MORPHEUS_API_URL/api/apps/99999" \
  -H "Authorization: BEARER $MORPHEUS_API_TOKEN"
```

> The above command returns HTTP 404 and JSON structured like this:

```json
{
  "success": false,
  "msg": "App not found"
}
```

The 404 error code is returned if a resource could be not be found by the specified ID.

### 500 Internal Server Error

```shell
curl "$MORPHEUS_API_URL/api/test/500" \
  -H "Authorization: BEARER $MORPHEUS_API_TOKEN"
```
> The above command returns HTTP 500 and JSON structured like this:

```json
{
  "success": false,
  "msg": "Looks like the server threw a gasket"
}
```

This error indicates something went wrong with the request and an unexpected error has occured. 

This example does not actually work and will return 404 instead.  Hopefully you do not encounter a 500 error.

### List of Error Codes

The Morpheus API uses the following error codes:

Error Code | Description
---------- | -------
400 | Bad Request -- Your request failed. Check your request parameters and try again.
401 | Unauthorized -- Your API key is invalid. Check your Authorization header.
403 | Forbidden -- Your API key does not have the required role or permissions.
404 | Not Found -- The specified resource could not be found.
405 | Method Not Allowed -- You tried to access a resource with an invalid method.
406 | Not Acceptable -- You requested a format that isn't json.
410 | Gone -- The entity requested has been removed from our servers.
418 | I'm a teapot.
429 | Too Many Requests -- You're asking too much of the server. Slow down!
500 | Internal Server Error -- We had a problem with our server. Try again later.
503 | Service Unavailable -- We're temporarially offline for maintanance. Please try again later.

