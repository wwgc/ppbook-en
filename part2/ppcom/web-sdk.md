# `PPCom Web SDK`

`PPCom Web SDK` enables developer to integrate `PPCom` in websites.

----

#### Integrate `PPCom Web SDK`
First of all, you must register an account in `PPConsole` (`PPConsole` will automatically create a service team for you and set you as the `Service Agent Administrator`). After that, you can find your service team's `app_uuid` in `PPConsole/Team Settings/Basic Info`.

There is two ways to integrate `PPCom` with your website.

#### Insert Code
`PPConsole` settings page(**Team Settings/Integration**) provides the min-version insert code.

To integrate `PPCom` with a website, open the source file(`index.html` e.g.) of the website, then copy the code and insert it between `<body></body>` tag. 

After refreshing the website, you should see `PPCom` appear in the right bottom corner of the website. 

The min-version insert code is as follows. You can change `window.ppSettings` if you want(check the `Web SDK API`). If you want to have access to all SDK APIs, please use the second way to integrate `PPCom`.

```html
<script>
window.ppSettings = {
    // replace app_uuid
    app_uuid:'your-app-uuid'
};
(function(){var w=window,d=document;function l(){var a=d.createElement('script');a.type='text/javascript';a.async=!0;a.src='https://ppmessage.com/ppcom/assets/pp-library.min.js';var b=d.getElementsByTagName('script')[0];b.parentNode.insertBefore(a,b)}w.attachEvent?w.attachEvent('onload',l):w.addEventListener('load',l,!1);})()
</script>
```

#### Load File
This is the recommended way to integrate `PPCom` for developers who want to access all PPCom Web SDK APIs. 

Using this way to integrate `PPCom` gurantee that `PPCom Web SDK` is fully loaded before you invoke any SDK APIs. 

Just insert below code to your website's source file(`index.html` e.g.). Then you can invoke all SDK APIs in you `javascript` code. Check below **Web SDK APIs** for more details.

```html
<script src="https://ppmessage.com/ppcom/assets/pp-library.min.js" type="text/javascript"></script>
```

#### Web SDK APIs

- ppSettings
  
  When invoke `PP.boot` or `PP.update`, the parameter you pass should have the same format as `window.ppSettings`. If you don't provide a parameter, `window.ppSettings` is used instead.
  
  The format of `window.ppSettings` is:

  ```javascript
  window.ppSettings = {
    // required, it is your service team' uuid, can be found in PPConsole/Team Settings/Basic Info
    app_uuid: "xxxxxx",
	
    // optional, it is the website visitor's email. If provided, PPMessage Server uses this email to target this visitor. Otherwise PPMessage Server treats this visitor as an anonymous user.
	user_email: "somebody.web@ppmessage.com",
    
    // optional, it is the website visitor's display name.
    user_name: "张三",

    // optional, it is the website visitor's avatar
    user_icon: "http://xxxx.com/avatar.png",
    
    // optional, it is the language PPCom uses. it can be either 'zh-CN' or 'en', default is 'zh-CN'.
	language: "zh-CN",
  };
  ```

- `PPCom.boot`
  
  Bootstrap `PPCom`. Once `PPCom` bootstraps, invoke `PP.boot` again will not re-bootstrap `PPCom`. If you need to re-bootstrap `PPCom`, you need to at first invoke `PP.shoutdown`, then invoke `PP.boot` again.
  
  The parameter is optional. If you don't provide parameter, `window.ppSettings` will be used instead.

  ```javascript
  PP.boot({
    app_uuid: 'your-app-uuid',
    user_name: 'ppcom-user-name',
    user_icon: 'ppcom-user-icon',
    language: 'zh-CN'
  }, function(isSucess, errorCode) {
    // callback
  });
  ```

- `PPCom.update`
  
  Invoke `PP.update` to change `PPCom` current user, or update `PPCom` user's information(email, icon, name).
  
  The parameter is optional. If you don't provide it, `window.ppSettings` will be used instead.

  ```javascript
  PP.update({
    app_uuid: 'your-app-uuid',
    user_email: 'somebody.web@ppmessage.com',
    user_name: 'new-user-name',
    user_icon: 'new-user-icon'
    user_language: 'zh-CN'
  });
  ```
  
- `PP.show`
 
  Show `PPCom Message Interface`.
  
  `PPCom Message Interface` is either the `conversation list`  or `chat window`. User can hide `PPCom Message Interface` by click the `Minimize` button. 
  
  To show `PPCom Message Interface`, invoke `PP.show`.

  ```javascript
  PP.show();
  ```

- `PP.hide`
 
  Hide `PPCom Message Interface`.
  
  `PPCom Message Interface` is either the `conversation list` or `chat window`. User can hide `PPCom Message Interface` by click the `Minimize` button. 
  
  To hide `PPCom Message Interface` programmatically, invoke `PP.hide`.
  
  ```javascript
  PP.dismiss();
  ```

- `PPCom.shutdown`
  
  Remove `PPCom`. 
  
  It will not delete `window.ppSettings` though. To display `PPCom` again, invoke `PP.boot`. 

  ```javascript
  PP.shutdown();
  ```


#### Usage Occasions

When `PPCom` bootstrap, it sends a request to `PPMessage Server` to create(if that user doesn't exist) and return a `PPMessage User` based on the parameter passed to `PP.boot`. If `user_email` is not specified, `PPMessage Server` will generate a random email address for this user.

Classic occasions: suppose you have a website with its own user system and you integrate PPCom with you website. Your website user can perform operations like sign in, change profile and log out. When user performs these operations, you should invoke `Web SDK API` to display `PPCom` correctly.

Consider below user operations:

* **User open your website**

  User opens your website and remains as a visitor. You should bootstrap `PPCom` as a visitor. The parameter you pass to `PP.boot` should not contain `user_email`. `user_icon` and `user_name` are optional, if you don't provide them, `PPMessage Server` will generate random icon and name for this user.
  
  If you want `PPCom` to appear upon website opens, just create `window.ppSettings` and load it before `pp-library-min.js`. When the SDK loads, it will bootstrap `PPCom` automatically based on `window.ppSettings`.

  ```html
  <script>
  window.ppSettings = {
      app_uuid: 'your-app-uuid',
      user_name: 'anonymous-user',
      user_icon: 'http://xxx/anonymous-user/icon.png',
      language: 'zh-CN'
  };
  </script>
  <script src="https://ppmessage.com/ppcom/assets/pp-library.min.js" type="text/javascript"></script>
  ```
  
  If you want to manually control when `PPCom` bootstrap, don't create `window.ppSettings`, invoke `PP.boot` instead.
  
  ```javascript
  PP.boot({
    app_uuid: 'your-app-uuid',
    user_name: 'anonymous-user',
    user_icon: 'http://xxx/anonymous-user/icon.png',
    language: 'zh-CN'
  });
  ```
  
* **User sign in** 
  
  When a visitor signs in to your website, you should change `PPCom` current user to be current sign-in user.
  
  The key is to provide `user_email` when pass parameter to invoke `PP.update`. `PPMessage Server` will create or return the `PPMessage User` based on `user_email`.
  
  You can provide `user_name` and `user_icon` if needed, or `PPMessage Server` will generate random `user_name` or `user_icon` instead.
  
  ```javascript
  PP.update({
    app_uuid: 'your-app-uuid',
    user_email: 'nameduser@test.com',
    user_name: 'named-user',
    user_icon: 'http://xxx/named-user/icon.png',
    language: 'zh-CN'
  });
  ```

* **User modify his profile**

  When user modify his profile in your website, you should invoke `PP.update` to tell `PPMessage Server` to update `PPMessage User`(use `user_email` to target the `PPMessage User`).
  
  ```javascript
  PP.update({
    app_uuid: 'your-app-uuid',
    user_email: 'nameduser@test.com',
    user_name: 'named-user-123',
    user_icon: 'http://xxx/named-user-123/icon.png',
    language: 'en'
  });
  ```
 
* **User sign out from your website**

  When user sign out from your website, you should update `PPCom` to reset current user to be a website visitor.
  
  ```javascript
    PP.update({
      app_uuid: 'your-app-uuid'
      user_name: 'anonymous-user',
      user_icon: 'http://xxx/anonymous-user/icon.png',
      language: 'zh-CN'
    });
  ```
  
#### Error Code

When something goes wrong and PPCom fails to bootstrap, it will print error info and erro code in browser console.

Error Code        | Error description
----------------- | -------------------------------
10000             | `app_uuid` is not valid
10001             | can't get `PPMessage User` linked to provided `user_email`
10002             | `PPCom` can't run in IE browser (version<=9)
10003             | `PPCom` can't connect to `PPMessage Server`
10004             | `user_email` is not valid
