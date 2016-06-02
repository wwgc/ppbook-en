# Get Token

You need to get a token to use PPMessage's APIs. To get it, you must firstly get the authorization code, then get the token.

View demo [Here](https://github.com/PPMESSAGE/ppmessage/tree/master/ppmessage/ppauth/demo).

---

### Get Authorization Code

Request:

```
GET https://ppmessage.com/ppauth/auth?state=xxxx&client_id=xxxx&redirect_id=xxxx&response_type=code
```

Parameters:

Parameter        | Description
-----------------|----------------------------
`state`          | The state of client, can be any value, `PPMessage Server` will return this value unchanged
`client_id`      | The client's id (your `PPKefu api_key` or `PPConsole api_key` in `PPConsole/Team Settings/Basic Info`)
`redirect_uri`   | The redirect uri, `PPMessage Server` will redirect user to this uri if the your request successes.
`response_type`  | The authorization type, we are using authorization code here, value is `code`

Response:

After generating a authorization code, `PPMessage Server` will redirect user to `PPMessage Authorization page`. 

In `PPMessage Authorization page`, user enters his email and password, then click `Continue`. If the email and password matches, `PPMessage Server` will redirect user to the `redirect_uri` you provided in last step and attach `authorization code` and `state` with it.

The uri is something like this:
```
http://you-site.com?code=xxxxxx&state=xxxx
```


### Get Token

After `PPMessage Server` redirect user to your `redirect_uri`, you have got the `authorization code` and `state`.

The `state` should match the `state` you provided in last step.

Now you can use the `authorizaiton code` to get token.

Request: 

```
POST https://ppmessage.com/ppauth/token
```

Body Parameters:

Parameter         | Description
------------------|-------------------------
`code`            | The authorization code you get
`client_id`       | The client's id (your `PPKefu api_key` or `PPConsole api_key` in `PPConsole/Team Settings/Basic Info`)
`client_secret`   | The client's id (your `PPKefu api_secret` or `PPConsole api_secret` in `PPConsole/Team Settings/Basic Info`)
`redirect_uri`    | Should be the same as last step's `redirect_uri`
`grant_type`      | Token type, value is `authorization_code`


Response:

Parameter        | Description
-----------------|-----------------------
`access_token`   | The token you use to invoke PPMessage's API
`token_type`     | The token type, value is `Bearer`
`expires_in`     | The token expire time, value is `3600*24s (24h)`


### Invoke API

After you get the token, you can use it to invoke PPMessage's API.
* `uri`: Request uri
  ```
  POST https://ppmessage.com/api/xxxx
  ```
  
* `headers`: Request headers must include `Content-Type` and `Authorization` (use your token to replace `xxxxxx`).
  ```
  {
      "Content-Type": "application/json",
      "Authorization": "OAuth xxxxxx"
  }
  ```
  
* `body`: Some APIs need you to provide `app_uuid`(your service team's uuid) or `user_uuid`(the user uuid related to your token). In these cases, you must provide `app_uuid` or `user_uuid` in request body:
  ```
  {
      "app_uuid": "xxxx",
      "user_uuid": "xxxx",
      ...
  }
  ```
 
* `response` (Example): 
  ```
  {
      "list": [],
      "error_code": "0",
      "error_string": "success",
      "uri": "/PP_GET_APP_SERVICE_USER_LIST"
  }
  ```
  
  For all API details, check [API List](./api/README.md).
