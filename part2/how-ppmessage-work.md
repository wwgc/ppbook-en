# How PPMessage Work

`PPMessage` includes `PPConfig`, `PPKefu`, `PPCom` and `PPMessage Server`. The former three are clients that must connect to `PPMessage Server` to run.

--------

#### PPConfig, PPKefu, PPCom, PPMessage Server


+--------------------+     3      +-----------------------+      4      +--------------------+
|  Customer Client   +----------->+        Server         +------------>+   Service Client   |
|                    |  message   |                       |   message   |                    |
|     [PPCom]        +<-----------+      [PPMessage]      +<------------+      [PPKefu]      |
+--------+-----------+     6      +--------+----+---------+      5      +----------+---------+
                                           |    ^
                                           |    |
                                         1 |    | 2
                                           |    |
                                           v    |
                                  +--------+----+---------+
                                  |   Service Management  |
                                  +                       +
                                  |      [PPConfig]       |
                                  +-----------------------+


1. PPConfig config and init PPMessage Server.

2. PPMessage Server show init status to PPConfig.

3. Website visitor sends message to service agents via `PPCom`. `PPMessage Server` receives and handles the message before sending it to service agents.

4. `PPMessage Server` sends the message to service agents, who receive and view it by using `PPKefu`.

5. Service agents send message to Website user via `PPKefu`. `PPMessage Server` receives and handles the message before sending it to Website visitor.

6. `PPMessage Server` send the message to Website visitor who get the message via `PPCom`.

