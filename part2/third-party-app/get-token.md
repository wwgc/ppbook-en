# Get Token

You need to get a token to use PPMessage's APIs. To get it, you must firstly get the authorization code, then get the token.

view demo [Here](https://github.com/PPMESSAGE/ppmessage/tree/master/ppmessage/ppauth/demo).

---

### Get Authorization Code

Request:

```
GET https://ppmessage.com/ppauth/auth?state=xxxx&client_id=xxxx&redirect_id=xxxx&response_type=code
```

Parameters:

Parameter        | Description
-----------------|----------------------------
`state`          | the state of client，can be any value，PPMessage Server will return this value unchanged
`client_id`      | the client's id (your `PPKefu api_key` or `PPConsole api_key` in `PPConsole/Team Settings/Basic Info`)
`redirect_uri`   | the redirect uri, in next step `Get Token`, PPMessage Server will redirect user to this uri
`response_type`  | the authorization type, we are using authorization code here, value is `code`

Response:

After getting authorization code, PPMessage Server will redirect user to PPMessage's Authorization page. 

In PPMessage's Authorization page, user enters his email and password, then click `Continue`. If the email and password matches, PPMessage Server will redirect user to the `redirect_uri` you provided in last step and attach `authorization code` and `state` with it.

the uri will something like this:
```
http://you-site.com?code=xxxxxx&state=xxxx
```

### get token

After PPMessage Server redirect user to your `redirect_uri`, you have got the `authorization code` and `state`.

The `state` should match the `state` you provided in last step.

Now you can use the `authorizaiton code` to get token.

Request: 

```
POST https://ppmessage.com/ppauth/token
```

Body Parameters:

Parameter         | Description
------------------|-------------------------
`code`            | the authorization code you get
`client_id`       | the client's id (your `PPKefu api_key` or `PPConsole api_key` in `PPConsole/Team Settings/Basic Info`)
`client_secret`   | the client's id (your `PPKefu api_secret` or `PPConsole api_secret` in `PPConsole/Team Settings/Basic Info`)
`redirect_uri`    | should be the same as last step's `redirect_uri`
`grant_type`      | token type, value is `authorization_code`


Response:

Parameter        | Description
-----------------|-----------------------
`access_token`   | the token you use to invoke PPMessage API
`token_type`     | the token type，value is `Bearer`
`expires_in`     | the token expire time，valuee is `3600*24s (24h)`


### Invoke API

After you get the token, you can use it to invoke PPMessage's API.

* `headers`： request headers must include `Content-Type` and `Authorization` (use your token to replace `xxxxxx`).
  ```
  {
      "Content-Type": "application/json",
      "Authorization": "OAuth xxxxxx"
  }
  ```
  
* `body`: some APIs need you to provide `app_uuid`(your service team's uuid) or `user_uuid`(the user' uuid your token is related to). In these cases, you must provide `app_uuid` or `user_uuid` in request body:
  ```
  {
      "app_uuid": "xxxx",
      "user_uuid": "xxxx",
      ...
  }
  ```

* `uri`: requst uri
  ```
  POST https://ppmessage.com/api/xxxx
  ```
 
* `response` (example): 
  ```
  {
      "list": [],
      "error_code": "0",
      "error_string": "success",
      "uri": "/PP_GET_APP_SERVICE_USER_LIST"
  }
  ```
  
  For all api details, check [API List](./api/README.md)
