# `PPCom` Interface

`PPCom` includes three interfaces: `PPCom Icon`, `PPCom Conversation`, `PPCom Conversation List`.

-----

#### `PPCom Icon`

When you open a website integrated with `PPCom`, the floating icon in right bottom corner is `PPCom Icon`.

When you move mouse over `PPCom Icon`, a floating card will show above it. The card shows service team name and team's welcome note.

`Service Agent Administrator` can change service team in `PPConsole/Team Settings/Basic info`, team's welcome note and `PPCom Icon` color in `PPConsole/Team Settings/User interface`.
    

#### `PPCom Conversation` 
When you click `PPCom Icon`, it will open `PPCom Conversation` interface.

* In the header bar of `PPCom Conversation` interface, left side is `Toggle` button, right side is `Minimize` button, center area is conversation name and `Show Member` icon button.

  `Toggle` button: open `PPCom Conversation List` interface

  `Minimize` button: hide `PPCom Conversation` interface, and show `PPCom Icon` interface
  
  `Show Member` button: click the button will show all members of this conversation. You can click a service agent and open a conversation with him.
  
* The footer bar of `PPCom Conversation` interface is the chat text area, you can type words in chat text area and send message to service agents.

#### `PPCom Conversation List`
In `PPCom Conversation`, if you click `Toggle` button, `PPCom` will show `PPCom Conversation List`.

* If `PPCom Message Dispatch Policy` is `ALL` or `SMART`, `PPCom Conversation List` interface will show all conversations. If you click a conversation, `PPCom` will open that conversation.

* If `PPCom Message Dispatch Policy` is `GROUP`, `PPCom Conversation List` interface will show all service groups and conversations. If you click a service group, `PPCom` will establish a conversation with the service group.

#### Establish Conversation

The usage of `PPCom` is to establish conversation with service agents. When `PPCom` user open `PPCom`, he must wait `PPMessage Server` to assign one or more service agents to him before conversation is established. If `PPMessage Server` can't find any available service agents, `PPCom` user will continue waiting. `PPCom` user can cancel this process at any time though.

Check [PPCom Message Dispatch Policy](./message-dispatch.md) for more details.
