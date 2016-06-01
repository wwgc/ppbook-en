## `PPCom iOS SDK`

### Interface

#### iOS SDK includes three interfaces:

- `Conversation List`
- `Conversation Window`
- `Conversation Member`

#### Conversation List

`Conversation List` is corresponding to `PPConversationsViewController`. All conversations that belongs to current user will show in this `Controller`. Click a conversation will open this conversation's `Conversation Window` interface. This is also the root interface of `PPCom iOS SDK`.

#### Conversation Window

`Conversation Window` is corresponding to `PPMessagesViewController`. `PPCom` user can chat with service agents in conversation window.

#### Conversation Member

In `Conversation Window`, if you click the `group` button in right-top corner, it will open `Conversation Member` (corresponding to `PPGroupMembersViewController`). It shows all members of current conversation. Conversation members include the `PPCom` user and one or more service agents. You can click one of service agents to open a new conversation with him.

### Integration

#### Download `PPComLib.framework` and `PPComLib.bundle`
  [Download PPCom iOS SDK](https://github.com/PPMESSAGE/ppmessage/tree/master/ppmessage/ppcom/ios)

#### Import Into Your Project

Open your project via `Xcode`, then drag `PPComLib.framework` and `PPComLib.bundle` into it. In the window `Xcode` popups, check `Copy items if needed` option to ensure files are copied to your project.

#### Import Dynamic Link Library

Click the "+" button in the bottom of `TARGET/general` interface. In the window `Xcode` popups, search `libicucore.dylib` or `libicucore.tbd` and add it to your project.

#### Modify Project Compile Parameters

In `TARGETS/Build Settings` interface, find `Other Linker Flags` option, and add parameter `-ObjC -all_load` to it.

#### Import Header Files

```obj-c
#import <PPComLib/PPComLib.h>
```

#### Inherit `PPConversationsViewController`, Initialize

```obj-c
// FeedbackMessagesViewController.h
#import <PPComLib/PPComLib.h>

@interface FeedbackMessagesViewController : PPConversationsViewController
@end

// FeedbackMessagesViewController.m
#import FeedbackMessagesViewController.h

@implementation FeedbackMessagesViewController ()

- (void)viewWillAppear:(BOOL)animated {
    [super viewWillAppear:animated];

    self.title = @"Conversation List";
    self.appUUID = `your-app-uuid`;

    // use one of below two method to initialize
    [self initialize];                         // initializa without email
    [self initializeWithUserEmail:USER_EMAIL]  // initializa with email
}

@end
```

### Demos
You can check `PPComDemo` project to find how to use the iOS SDK. You can ask us in [PPMessage Official site](https://ppmessage.com) if you have any questions.
