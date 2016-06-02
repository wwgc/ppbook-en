# Set Up PPMessage With Docker 

Following below steps, you can set up PPMessage with docker in Mac and Linux.

---

#### Concept of Docker 
> Docker allows you to package an application with all of its dependencies into a standardized unit for software development. Docker containers wrap up a piece of software in a complete filesystem that contains everything it needs to run: code, runtime, system tools, system libraries – anything you can install on a server. This guarantees that it will always run the same, regardless of the environment it is running in.


#### Install Docker
Firstly read [docker getting started](https://docs.docker.com/mac/) to have a basic understanding of docker and install docker in your machine.

After installing docker, you should check whether docker command is available.

* Mac
 
  Open LaunchPad and click `Docker Quickstart Terminal` to open a terminal.
  
  Wait unitl docker is started, type command: `docker info`. If nothing goes wrong, docker command is available.
  
* Linux
  
  Open a terminal， type command: `docker info`.  If nothing goes wrong, docker command is available.
  
  If terminal shows below error:

  > Cannot connect to the Docker daemon. Is 'docker -d' running on this host?

  You should at first check docker service is started. type command:

  ```
  sudo service docker restart
  ```

  If that doesn't work, you need to add your current user to docker group, run 

  ```bash
  sudo usermod -aG docker $USER
  ```
  
  Then logout & login with current user, now docker command should be available.


#### Download PPMessage Docker Mirror
After install docker, the next step is to download PPMessage docker mirror. It is hosted in [Docker Hub](https://hub.docker.com/r/ppmessage/ppmessage/), you can find it by searching `ppmessage` in docker hub. To download it, open a terminal and run

```
docker pull ppmessage/ppmessage
```

while waiting for download to complete, you can continue performing below steps.


#### Download PPMessage Source Files
Before starting PPMessage, you need to download PPMessage source files from [github](https://github.com/PPMESSAGE/ppmessage).

Suppose you save PPMessage to `~/Documents/ppmessage`.

```
git clone git@github.com:PPMESSAGE/ppmessage.git  ~/Documents/ppmessage
```

#### Download Geolite2
Enter `~/Documents/ppmessage`, run

```
./ppmessage/scripts/download_geolite2.sh
```

#### Download Bower Components, Npm Packages
Firstly you need to download `nodejs`.

In Mac, to install `nodejs`, run 

```
brew install nodejs
```

In Linux(Debian\Ubuntu), to install `nodejs 4.x`, run 

```
curl -sL https://deb.nodesource.com/setup_4.x | sudo -E bash -
sudo apt-get install -y nodejs
```

Then, use `npm` to install `bower, gulp`

```
sudo npm install -g bower gulp
```

Finally, Download bower & npm dependencies of `PPCom, PPKefu, PPConsole`. Enter`~/Documents/ppmessage`, run

```
./dist.sh bower
./dist.sh npm
```

#### Config PPMessage
Check [Config PPMessage](./config-ppmessage.md) and create your config.py.

#### Start PPMessage
Before starting PPMessage, ensure you have finished following steps:
* Download PPMessage docker mirror
* Download PPMessage source files
* Config PPMessage
* Download bower, npm dependencies

Then, run following command to bootstrap PPMessage (You may modify this command based on your PPMessage Configuration).

```
docker run -it -p 8080:8080 -v ~/Documents/ppmessage:/ppmessage ppmessage/ppmessage
```

`-p 8080:8080` means mapping local port 8080 to docker container port 8080, thus you can access PPMessage in docker container via port 8080.

`-v ~/Documents/ppmessage:/ppmessage` means mapping local PPMessage directory(`~/Docuemnts/ppmessage`) to docker container PPMessage directory(`/ppmessage`).

You can run `~/Documents/ppmessage/ppmessage/docker/run-ppmessage.sh` to bootstrap PPMessage too.


#### Use PPMessage
After start PPMessage with docker, we need to generate javascript and css files of PPCom, PPKefu, PPConsole to visit them.

Enter`~/Documents/ppmessage`, run 

```
./dist.sh gulp
```

Now, you can visit modules of PPMessage.

The address is like: `http_protocol://server_ip:server_port/xxxx`, such as `http://127.0.0.1:8080/ppkefu`, `http://192.168.99.100:8080/user`.

* `http_protocol` is related to your PPMesssage configuration `nginx.ssl`, `on` for `https`, `off` for `http`

* `server_port` is related to your PPMessage configuration `nginx.listen`

* `server_ip` is the ip of docker Machine

  * in Linux
  
    docker is running directly on your system, `server_ip` is '127.0.0.1'.

  * in Mac

    docker is runing on virtual machine, `server_ip` is the ip of docker virtual machine. To get this ip, open terminal, run

    ```
    docker-machine ip default
    ```

    It will give the ip of docker virtual machine, such as `192.168.99.100`.

Possible errors：

* When sign in to PPConsole, browser console throw ppauth 400 error.
  
  Solution: Firstly update PPMessage (`git pull`), then run `./dist.sh gulp`, finally clean browser cache.


#### Stop, Restart PPMessage
Using `docker run` to start PPMessage will always create a new container and init PPMessage in it. 

In fact, you may want to reuse the container that you create at the first time, thus the data created during running PPMessage will be kept.

To do that, you need to get the id of that container, then perform start, restart, close operations to it.

Check following commands.

* View All Containers
  
  ```
  docker ps -a
  ```
  This will give list of all docker container. You need to record the if of PPMessage container.

* Stop Container
  
  ```
  docker stop container_id
  ```

* Start Container
  
  ```
  docker start container_id
  ```

* Restart Container
  
  ```
  docker restart container_id
  ```

* Remove Container
 
 ```
 docker rm contaniner_id
 ```
