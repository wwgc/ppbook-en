# Cordova PPKefu

PPKefu is a [Cordova](https://cordova.apache.org/) project, support Android, iOS.

#### Preparation
install nodejs, check [nodejs](https://nodejs.org/) for install method. Then use npm to install cordova and ionic.

    sudo npm install -g cordova
    sudo npm install -g ionic
    
#### initialize
enter ppkefu root directory

    cd ~/Documents/ppmessage/ppmessage/ppkefu/ppkefu
    
1. Open package.json, find `phonegap-plugin-push`

        {
          "variables": {
              "SENDER_ID": "878558045932"
          },
          "locator": "phonegap-plugin-push",
          "id": "phonegap-plugin-push"
        },
    
    Change `SENDER_ID` to your `gcm sender id`. About gcm, please check [google cloud message](https://developers.google.com/cloud-messaging/).
    If You don't need gcm push, you can set `SENDER_ID` to random string.
    
2. Use ionic restore plugins and platforms

        ionic state restore
    
3. Use ionic to run PPKefu in Andorid and iOS

        ionic run android
        ionic build android

    for iOS, firstly
    
        ionic prepare ios
        open platforms/ios/PPMessage.xcodeproj
    
    then run PPKefu using Xcode.
