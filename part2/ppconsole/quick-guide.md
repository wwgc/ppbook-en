# Quick Guide

`Quick Guide` introduce account registration, team management, `PPCom` integration, `PPKefu` usage.

-----

#### Account Registration
    
1. Open [ppmessage.com](https://ppmessage.com), click `Start to use PPMessage` button and open `PPConsole` sign up page.

2. Choose `Sign Up` interface. Enter `service team name`, your `full name`, `email` and `password`, choose `language`, then click `Sign Up` button. 

3. After signing up, you have an account and a service team. Your account is the first service agent and also the service agent administrator of your service team. You will use this account to manage your service team and other service agents.

3. Next step, we start to integrate `PPCom`.


#### Integrate PPCom
    
In `PPConsole` settings page, open `PPConsole/Team Settings/App Integrate` interface. It shows `PPCom`'s insert code and `PPCom` preview website address. 
   
If you don't want to integrate `PPCom` with your website yet, you can open the preview website to try using `PPCom`, and skip to next step `Using PPKefu` directly.
  
If you want to integrate `PPCom` with your own website, finish following steps:

1. Copy `PPCom`'s insert code and insert it between the `<body></body>` tag in the source file of your website.
 
2. Refresh your website and `PPCom` will appear in the right-bottom corner. You can open PPCom and send message to service agents.

3. The service team you created before only have one service agent (your `PPConsole` account). You will use `PPKefu` to sign in to this service agent and receive PPCom user' message. Go to next step `Using PPKefu`.


#### Using PPKefu

1. Sign in to `PPConsole` using your account, you will see `Start Service` button in `PPConsole`'s navbar.

2. Click `Start Service` button, it will open `PPKefu` in new browser tab and automatically sign in with your account.

3. Now you can see the message `PPCom` user has sent to you, and send message back to him.

#### Conclusion

`PPConsole` is the key to use `PPMessage`. For more details about `PPConsole`, check [PPConsole](./README.md).
