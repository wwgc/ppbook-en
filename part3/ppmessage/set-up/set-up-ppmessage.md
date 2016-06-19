# Set Up PPMessage In Mac & Linux

Following below steps, you can set up PPMessage in Mac & Linux(Debia/Ubuntu).

---

#### Download PPMessage
Firstly, you need to install git, then clone PPMessage from github.com. Suppose you save PPMessage to `~/Documents/ppmessage`.

```
git clone git@github.com:PPMESSAGE/ppmessage.git  ~/Documents/ppmessage
```

#### Install Dependency Softwares
Enter `~/Documents/ppmessage/ppmessage/scripts`.

* In Mac, run

  ```
  bash set-up-ppmessage-on-mac.sh
  ```

* In Linux(Debian/Ubuntu), run

  ```
  bash set-up-ppmessage-on-linux.sh
  ```

Notice: when run shell script to install software, your system's software may be upgraded. You need to know following tips and change the install script if necessary.

* In Mac, run the script will install `mysql-connector-python-2.1.3`.

* In Linux, run the script will install `mysql-connector-python-2.1.3`.


#### Config PPMessage
Check [Config PPMessage](./config-ppmessage.md), and create your config file.


#### Bootstrap PPMessage
Firstly, ensure `redis-server` is started.

* In Mac, run them by

  ```
  brew services start redis
  ```

* In Linux(Debian/Ubuntu), run them by
  
  ```
  sudo service redis-server start
  ```

Then, run ppmessage.py

```bash
python ppmessage.py
```

#### Using PPMessage

Once PPMessage is running, we can visit modules of PPMessage.

The address is: `http_protocol://server_ip:server_port/service_name`.

it is related to your PPMessage configuration.

`http_protocol` default is `http`, maybe `https`.
`server_ip` default is `server.name`
`server_port` default is `8945`

Example：

    PPKefu: http://127.0.0.1:8945/ppkefu/
    PPConsole: http://127.0.0.1:8945/ppconsole/

