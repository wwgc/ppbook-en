# Set Up PPMessage In Mac & Linux

Following below steps, you can set up PPMessage in Mac & Linux(Debia/Ubuntu).

---

#### Download PPMessage
Firstly, you need to install git, then clone PPMessage from github.com. Suppose you save PPMessage to `~/Documents/ppmessage`.

```
git clone git@github.com:PPMESSAGE/ppmessage.git  ~/Documents/ppmessage
```

#### Download Geolite2
After downloading PPMessage, enter `~/Documents/ppmessage` and run:

```
./ppmessage/scripts/download_geolite2.sh
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

* In Linux, run the script will install `nginx-1.8.0`，`ffmpeg-3.0.2`，`mysql-connector-python-2.1.3`.


#### Install Bower Components, Npm Packages
Enter `~/Documents/ppmessage`, run 

```
./dist.sh bower
./dist.sh npm
```

#### Config PPMessage
Check [Config PPMessage](./config-ppmessage.md), and create your config file.


#### Bootstrap PPMessage
Firstly, ensure `mysql server`, `redis-server`, `nginx` is started.

* In Mac, run them by

  ```
  brew services start mysql
  brew services start redis
  nginx
  ```

* In Linux(Debian/Ubuntu), run them by
  
  ```
  sudo service mysql start
  sudo service redis-server start
  sudo nginx
  ```

Then, enter `~/Documents/ppmessage`, perform following operations.

1. add `ppmessage` into `Python PATH`

  ```
  sudo ./dist.sh dev
  ```
  
2. init databse, cache, update nginx conf (need `sudo` in Linux)

  ```
  ./dist.sh bootstrap
  ```
  
3. reload nginx conf (needd `sudo` in Linux)

  ```
  nginx -s reload
  ```

4. generate PPKefu, PPConsole, PPCom javascript, css files
  
  ```
  ./dist.sh gulp
  ```
  
5. start PPMessage(need `sudo` in Linux)

  ```
  ./dist.sh start
  ```


#### Using PPMessage

Once PPMessage is running, we can visit modules of PPMessage.

The address is: `http_protocol://server_ip:server_port/service_name`.

it is related to your PPMessage configuration.

`http_protocol` is related to `nginx.ssl`, `on` for `https`, `off` for `http`.
`server_ip` is `server.name`
`server_port` is `nginx.listen`

Example：

    PPKefu: http://192.168.0.52:8080/ppkefu
    PPConsole: http://192.168.0.52:8080

Possible errors：

* When sign in to PPConsole, browser console throw ppauth 400 error.
  
  Solution: Firstly update PPMessage (`git pull`), then run `./dist.sh gulp`, finally clean browser cache.

Other commands:

* Start `PPMessage` (need `sudo` in Linux)

  Run `./dist.sh bootstrap` will init database. After initialization, to start `PPMessage`, just run

  ```
  ./dist.sh start
  ```

* Stop PPmessage (need `sudo` in Linux)

  ```
  ./dist.sh stop
  ```
  
* View PPMessage running status
    
  ```
  supervisorctrl
  ```
    
* View Logs
  
  Logs are saved in `/usr/local/var/log`.

  ```
  ./dist.sh log                                  # view all logs
  tail -f /usr/local/var/log/ppmessage-api.log   # view log of a module seperatly
  ```
