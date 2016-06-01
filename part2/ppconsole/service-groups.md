# Service Group

In `Service Group` interface, you can create, modify and remove service group. You can also add service agent to a service group or remove service agent from it.

-----

#### Manage Service Group

* Create Service Group

  In `Service Group` interface, click `Create` button. In the window pops up afterwards, enter service group name, description, check whether it is a primary group, then click `Create Group` button to finish creating service group.

  Primary group is a special group under service team. A service team can only have one primary group. If you choose `GROUP` policy for your service team in `Message Dispatch Policy` interface, when a PPCom user requests to establish conversation with service agents, PPMessage Server will try to choose a service agent who is in READY status and assign him to this PPCom user.
  
* Modify Service Group
  
  `Service Group` interface shows all service groups under your service team. click `modify` button of a service group, you can modify service group's name, description and whether it is a primary group.

* Remove Service Group

  `Service Group` interface shows all service groups under your service team. click `remove` button of a service group, you can remove this service group from your service team. all service agent in this service group will move to service group: `Not grouped`.
  

#### Manage Service Agents

* Add Service Agents to Service Group

  In `Service Group` interface, click `All Service Agents` button, you will see all service agents in your service team. each service agent shows following info:
      
        email: the sign in email of service agent
        role: the role service agent play in service team, either `Admin` or `Service Agent`
        group: the service group that this service user belongs to, a service user can belong to up to one service group
  
  To add service agents into a service group, you need to choose one or more service agents, then click `Select Group` button, finally click the target service group to finish.

* Remove Service Agents from Service Group

  One service agent can only belongs to one service group. If you want to remove a service agent from a service group, you can move him to another service group.
