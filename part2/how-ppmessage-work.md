# How PPMessage work

PPMessage includes PPConsole, PPKefu, PPCom and PPMessage Server. The former three are client applicaitons that connect to PPMessage Server when they run.
--------

#### PPKefu, PPConsole, PPCom and PPMessage Server

    +--------------------+     1      +-----------------------+      2      +--------------------+
    |  Customer Client   +----------->+        Server         +------------>+   Service Client   |
    |                    |  message   |                       |   message   |                    |
    |     [PPCom]        +<-----------+      [PPMessage]      +<------------+      [PPKefu]      |
    +--------+-----------+     4      +--------+----+---------+      3      +----------+---------+
             ^                                 |    ^                                  ^
             |                                 |    |                                  |
           7 |                               5 |    | 6                              8 |
             |                                 |    |                                  |
             |                                 v    |                                  |
             |                        +--------+----+---------+                        |
             |                        |   Service Management  |                        |
             +------------------------+                       +------------------------+
                                      |      [PPConsole]      |
                                      +-----------------------+


1. Website visitor send message to service agent via PPCom. PPMessage Server receives and handle the message before sending it to service agent.

2. PPMessage Server sends the message to service agents, who receive and view it by PPKefu.

3. Service agents send message to Website user via PPKefu. PPMessage Server receives and handle the message before sending it to Website user.

4. PPMessage Server send the message to Website user, who recevie and view the message via PPCom.

5. Service Agent Administrator sign in to PPConsole, which loads all information about the service team from PPMessage Server.

6. Service Agent Administrator modify service team settings, add/remove service agents, save changes to PPMessage Server.

7. Service Agent Administrator gets the code to deploy PPCom in PPConsole, and modify settings to change PPCom's looking.

8. Service Agent Adminstrator can sign in to PPKefu in PPConsole.
