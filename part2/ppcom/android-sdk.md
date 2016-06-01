# PPCom Android SDK

---

#### Download

[ ![Download](https://api.bintray.com/packages/ppmessage/maven/ppcomsdk/images/download.svg) ](https://bintray.com/ppmessage/maven/ppcomsdk/_latestVersion)

======

You can download the sdk through `Maven` or `Gradle`.

* Maven

```xml
<dependency>
  <groupId>com.ppmessage</groupId>
  <artifactId>ppcomsdk</artifactId>
  <version>0.0.2</version>
  <type>pom</type>
</dependency>
```

* Gradle

```groovy
compile 'com.ppmessage:ppcomsdk:0.0.2'
```

#### Interface

Android SDK includes three interfaces:

- `Conversation List`
- `Conversation Window`
- `Conversation Member`

1. `Conversation List`

All conversations that belongs to current user will show in this `Conversation List`. Click a conversation will open this conversation's `Conversation Window` interface.

2. `Conversation Window`

`PPCom` user chats with service agents in `Conversation Window`. It shows all messages in this conversation. `PPCom` user enter words in text area below the `Conversation Window`, and send message by click `Send` button.

3. `Conversation Member`

In `Conversation Window`, if you click the `group` button in right-top corner, it will open `Conversation Member`. It shows all members of current conversation. Conversation members include the `PPCom` user and one or more service agents. You can click one of service agents to open a new conversation with him.


#### Usage
======

1. Initialize

```java
public class App extends Application {

    private static final String PPMESSAGE_APP_UUID = "xxx";

    @Override
    public void onCreate() {
        super.onCreate();

        PPComSDK sdk = PPComSDK.getInstance();
        sdk.init(new PPComSDKConfiguration
            .Builder(this)
            .setAppUUID(PPMESSAGE_APP_UUID)
            .build());

    }

}
```

2. Startup

```java
public class MainActivity extends ConversationsActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);

        startUp();
    }

}
```
