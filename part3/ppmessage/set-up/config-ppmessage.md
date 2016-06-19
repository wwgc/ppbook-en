# Config PPMessage

Before bootstrap PPMessage, we need to config PPMessage.

---

#### Config PPMessage if PPMessage is never configed. If configed `config.json` is created and `configed` is `true`.
Suppose your are under root of PPMessage is in `~/Documents/ppmessage`.

```
python ppmessage.py
```
> Access `http://127.0.0.1:8945` with your browser to config PPMessage, once configed, the config.json will be created. If you want reconfig PPMessage, delete the config.json file, and run ppmessage.py.

```bash
cd ~/Documents/ppmessage/ppmessage/bootstrap
more config.json
```



#### Describe config.json


**The first user of PPMessage is the administrator of PPMessage**

```python
"user": {
    "user_language": "",
    "user_fullname": "",
    "user_email": "",
    "user_password": "",
},
```

This user is the super administrator of PPMessage, who has access to all users and service teams. When PPMessage bootstrap, super administrator will be created.

Parameter        | Description
-----------------|-------------------------------
`user_language`  | language decides what language PPMessage will use, especially the anonymous user's name.
`user_fullname`  | fullname
`user_email`     | email
`user_password`  | password


#### Service Team

```python
"team": {
    "app_uuid": "",
    "app_name": "",
}
```

This is the service team of super administrator.


Parameter        | Description
-----------------|------------------------------
`app_uuid`       | service team uuid
`app_name`       | service team name


#### Mysql Settings

```python
"mysql": {
    "db_host": "127.0.0.1",
    "db_port": "3306",
    "db_user": "root",
    "db_pass": "test",
    "db_name": "ppmessage",
},
```

Parameter        | Description
-----------------|---------------------------------------------------
`db_host`        | msyql server address, default to be `127.0.0.1`
`db_user`        | mysql login user, default to be `root`
`db_pass`        | mysql login password
`db_name`        | ppmessage database name, default to be `ppmessage`

#### Server Settings

```python
"server": {
    "name": "127.0.0.1",
    "identicon_store": "/usr/local/opt/ppmessage/identicon",
    "generic_store": "/usr/local/opt/ppmessage/generic",
},
```

Parameter        | Description
-----------------|-------------------------------------------------------------------------------
name             | server name or ip address, PPKefu PPCom need this to know where is the server.
identicon_store  | PPCom user icon store path
generic_store    | common file store path


#### iOS apns config (optional)

> if iOS push is configed, it is true, otherwise no ios field in this json or configed is false.

```python
"ios": {
   "configed": true
},
```

#### GCM Settings (optional)

```python
"gcm": {
    "api_key": "your gcm api key",
},
```
