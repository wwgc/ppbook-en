# PPCom Web SDK

`PPCom Web SDK` enables developer to integrate `PPCom` in websites.

----

#### Integrate PPCom Web SDK
> Get app_uuid from PPKefu/Settings/Developer Keys.

There is two ways to integrate `PPCom` with your website.

#### Insert Code
`PPKefu` settings page(**Settings/Widget Code**) provides the min-version insert code.

To integrate `PPCom` with a website, open the source file(`index.html` e.g.) of the website, then copy the code and insert it between `<head></head>` tag. 

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
    // required, it is your service team' uuid, can be found in PPKefu/Settings/Developer Keys
    app_uuid: "xxxxxx",


    // required if a registered user
    user_uuid: "1231",

    // required if a registered user, timestamp (ms)
    user_createtime: 1231321312,

    // optional, it is visitor's email. 
	user_email: "somebody.web@ppmessage.com",

    // optional, it is visitor's mobile. 
	user_mobile: "+81xxxxxxxxxx",
        
    // optional, it is the website visitor's display name.
    user_name: "Alex Z",

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
  
  `PPCom Message Interface` is either the `conversation list`  or `chat window`. User can hide `PPCom Message Interface` by click the chat button again. 
  
  To show `PPCom Message Interface`, invoke `PP.show`.

  ```javascript
  PP.show();
  ```

- `PP.hide`
 
  Hide `PPCom Message Interface`.
  
  `PPCom Message Interface` is either the `conversation list` or `chat window`. 
  
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

