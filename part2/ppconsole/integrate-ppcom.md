# App Integrate 

`App Integrate` shows the `PPCom` insert code and `PPCom` preview website address.

------

#### integrate PPCom

Here we only introduce the `insert code` way to integrate PPCom. For more details please check [PPCom Web SDK](../ppcom/web-sdk.md).

The code to insert is as follows. `app_uuid` in `window.ppSettings` is your service team's uuid, which you can find in `PPConsole/Team Settings/Basic Info`.

```html
<script> 
  window.ppSettings = {app_uuid:'cd0cb63d-0b7f-11e6-a37b-ac87a30c6610'};
  (function(){var w=window,d=document;function l(){var a=d.createElement('script');a.type='text/javascript';a.async=!0;a.src='https://ppmessage.com/ppcom/assets/pp-library.min.js';var b=d.getElementsByTagName('script')[0];b.parentNode.insertBefore(a,b)}w.attachEvent?w.attachEvent('onload',l):w.addEventListener('load',l,!1);})()
</script>
```

`App Integrate` shows above code. To integrate `PPCom` with your website, you need to copy the code and insert it between `<body></body>` tag in the source file(index.html e.g.) of your website. Like this:

```html
<!DOCTYPE html>
<html>
  <head>
    <!-- your-code -->
  </head>
  <body>
    <!-- your-code -->
    <script> 
      window.ppSettings = {app_uuid:'cd0cb63d-0b7f-11e6-a37b-ac87a30c6610'};
      (function(){var w=window,d=document;function l(){var a=d.createElement('script');a.type='text/javascript';a.async=!0;a.src='https://ppmessage.com/ppcom/assets/pp-library.min.js';var b=d.getElementsByTagName('script')[0];b.parentNode.insertBefore(a,b)}w.attachEvent?w.attachEvent('onload',l):w.addEventListener('load',l,!1);})()
    </script>
  </body>
</html>
```

Then open your website, `PPCom` will show in the right bottom corner of the website.

#### Preview `PPCom`

Concept of previewing PPCom: in `App Integrate` interface, if you click `Preview PPCom` button, your browser will open a temporary website. This website is integrate with PPCom (using your service team uuid). You can test PPCom in this website before actually integrate PPCom with your own website.
