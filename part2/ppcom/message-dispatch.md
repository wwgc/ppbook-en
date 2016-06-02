# Message Dispatch Policy

`Service Agent Administrator` can set `Message Dispatch Policy` in `PPConsole/Team Settings/Message Dispatch`. It decides which service agents should be added to chat when `PPCom` user establishes chat with service agents.

--------

#### Target Service Agents

`Target Service Agents`: When `PPCom` user establishes chat with service agents, service agents who can be added to the chat is `Target Service Agents`.

When `PPCom` opens, it will firstly try to find an existing conversation. If it doesn't find one, it will request `PPMessage Server` to find `Target Service Agents` and establish a conversation between current `PPCom` User and `Target Service Agents`.

`PPMessage Server` searches for `Target Service Agents` based on service agent status, which includes:

> BUSY: Service agent who is in BUSY status will not be added to any new conversation.
> 
> REST: Service agent who is in REST status will not be added to any new conversation.
>
> READY: Service agents who is in READY status will be added to new conversation.


#### Message Dispatch Policy

**All**

When `PPCom` user establishes conversation, `PPMessage Server` will add all service agents in service team to it.


**SMART**

When `PPCom` user establishes conversation, `PPMessage Server` will try to find service agents who is in Ready status and add one of them to it. If there is not service agents in Ready status, fall back to ALL policy and add all service agents to it.


**GROUP**

In GROUP policy, you(`Service Agent Administrator`) must create a `primary group` and add some service agents to it. You can create more service groups. `PPCom` user can establish chat with a specific service group.

In GROUP policy, `PPCom` user can establish chat in two ways.

* Click `PPCom Icon`

  In this way, `PPMessage Server` will try to find `Target Service Agents` in primary group and add one of them to the conversation. If there is not any available service agents, add all service agents in primary group to the conversation.

* Click a service group in `PPCom Conversation List`

  In this way, `PPMessage Server` will try to find `Target Service Agents` in this service group and add one of them to the conversation. If there is not any available service agents, add all service agents in this service group to the conversation.
