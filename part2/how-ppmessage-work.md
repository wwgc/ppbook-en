# How PPMessage Work

`PPMessage` includes `PPConsole`, `PPKefu`, `PPCom` and `PPMessage Server`. The former three are clients that must connect to `PPMessage Server` when they run.

--------

#### `PPKefu`, `PPConsole`, `PPCom`, `PPMessage Server`

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


1. Website visitor sends message to service agents via `PPCom`. `PPMessage Server` receives and handles the message before sending it to service agents.

2. `PPMessage Server` sends the message to service agents, who receive and view it by using `PPKefu`.

3. Service agents send message to Website user via `PPKefu`. `PPMessage Server` receives and handles the message before sending it to Website user.

4. `PPMessage Server` send the message to Website user, who receives and views the message via `PPCom`.

5. `Service Agent Administrator` sign in to `PPConsole`, which loads all information about the service team from `PPMessage Server`.

6. `Service Agent Administrator` modify service team settings, add/remove service agents, `PPConsole` saves these changes to `PPMessage Server`.

7. `Service Agent Administrator` gets the code to integrate `PPCom` from `PPConsole`, and modify settings to change `PPCom` style.

8. `Service Agent Adminstrator` can sign in to `PPKefu` from `PPConsole`.
