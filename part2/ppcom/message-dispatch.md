# PPCom Message Dispatch Policy

`Service Agent Administrator` can set `PPCom Message Dispatch Policy` in `PPConsole/Team Settings/Message Dispatch`. Dispatch Policy decides which service agents should be added to chat when `PPCom User` establishs chat with service agents.

--------

#### Target Service Agents

`Target Service Agents`: When `PPCom User` establishs chat with service agents, service agents who can be added to the chat is `Target Service Agents`.

When `PPCom user` open PPCom, if there is not any chat established before, PPCom will request PPMessage Server to find `Target Service Agents` and establish chat between this `PPCom User` and `Target Service Agents`

`PPMessage Server` searches `Target Service Agents` based on service agent status, which includes:

> Busy: Service agent who is in Busy status will not be added to any new chat.
> Rest: Service agent who is in Rest status will not be added to any new chat.
> Ready: Service agents who is in Ready status will be added to new chat.


#### Message Dispatch Policy

**All**

When PPCom user establishs chat, PPMessage Server will add all service agents in service team to this chat.


**SMART**

When PPCom user establishs chat, PPMessage Server will try to find service agents who is in Ready status and add one of them to the chat. If there is not service agents in Ready status, fall back to ALL policy and add all service agents to the chat.


**GROUP**

In GROUP policy, you(service agent administrator) must create a `primary group` and add some service agents to it. You can create more service groups. PPCom user can establish chat with a specific service group.

In GROUP policy, PPCom user can establish chat in two ways.

* Click PPCom(the floating icon)

  In this way, PPMessage Server will try to find `Target Service Agents` in primary group and add one of them to the chat. If there is not any available service agents, all service agents in primary group will be added to the chat.

* Click a service group in `PPCom chat list interface`

  In this way, PPMessage Server will try to find `Target Service Agents` in this service group and add one of them to the chat. If there is not any available service agents, all service agents in this service group will be added to the chat.
