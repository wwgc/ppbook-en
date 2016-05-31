# Config PPMessage

Before bootstrap PPMessage, we need to config PPMessage.

---

### Create config.py
Suppose your PPMessage is in `~/Documents/ppmessage`.

```bash
cd ~/Documents/ppmessage/ppmessage/bootstrap
cp config.template.py config.py
```

### Describe config.py

config.py contains following settings.

#### Super Administrator

```python
"user": {
    "user_language": "",
    "user_firstname": "",
    "user_lastname": "",
    "user_fullname": "",
    "user_email": "",
    "user_password": "",
},
```

This user is the super administrator of PPMessage, who has access to all users and service teams. When PPMessage bootstrap, super administrator will be created.

Parameter        | Description
-----------------|-------------------------------
`user_language`  | language decides what language PPMessage will use to create PPCom anonymous user and set PPCom's default welcome note, can be "zh_cn", "en", "zh_tw" 
`user_firstname` | admin's firstname
`user_lastname`  | admin's lastname
`user_fullname`  | admin's fullname
`user_email`     | admin's email
`user_password`  | admin's password



#### Super Administrator's Service Team

```python
"team": {
    "app_name": "",
    "company_name": "",
}
```

This is the service team of super administrator.


Parameter        | Description
-----------------|------------------------------
`app_name`       | service team name
`company_name`   | company name


#### Mysql Settings

```python
"mysql": {
    "db_host": "127.0.0.1",
    "db_user": "root",
    "db_pass": "test",
    "db_name": "ppmessage",
},
```

Parameter        | Description
-----------------|---------------------------------------------------
`db_host`        | msyql server address, default to be `127.0.0.1`
`db_user`        | mysql login user, default to be `root`
`db_pass`        | mysql login password, should match your msql password (when you install mysql, it will tell you to set password)
`db_name`        | ppmessage database name, default to be `ppmessage`, no need to change


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
name             | server ip, such as `192.168.0.52`, PPKefu need this to connect to right server
identicon_store  | PPCom user icon store path
generic_store    | common file store path


#### js Settings
```python
"js": {
    "min": "no", # "no" or "yes"
},
```

If you set `js.min` to `yes`, when run gulp task for PPCom, PPKefu, PPConsole, their javascript, css files will be compressed.

#### Nginx Settings

```python
"nginx": {
    "nginx_conf_path": "/usr/local/nginx/conf/nginx.conf",
    "server_name": ["ppmessage.com", "www.ppmessage.com"],
    "listen": "8080", #80
    "upload_store": "/usr/local/opt/ppmessage/uploads 1",
    "upload_state_store": "/usr/local/opt/ppmessage/upload_state",
    "ssl": "off", # off/on
    "ssl_listen": "443",
    "ssl_certificate": "/Users/dingguijin/ppmessage/ppmessage/certs/ppmessage.cn.instant/issue/ssl_bundle.crt",
    "ssl_certificate_key": "/Users/dingguijin/ppmessage/ppmessage/certs/ppmessage.cn.instant/server.key",
},

```

Parameter               | Description
------------------------|---------------------------------------------------
`nginx_conf_path`       | nginx conf path, When set up in Mac, it's `/usr/local/etc/nginx/nginx.conf`. When set up in Linux or Docker, it's `/usr/local/nginx/conf/nginx.conf`
`server_name`           | server name, should be like: `[some-server.com`, `www.some-server.com]`
`listen`                | nginx listen port, `8080` for development, `80` for production
`upload_store`          | nginx upload store
`upload_state_store`    | nginx upload state store
`ssl`                   | set to `on` for `https` protocol, set to `off` for `http` protocol
`ssl_listen`            | ssl listen port
`ssl_certificate`       | ssl certificate
`ssl_certificate_key`   | ssl certificate key


#### Apns Settings (optional)

```python
"apns": {
    "name": "your-app's-bundle-id",
    "dev": "/path-to-your-apns-development.p12",
    "pro": "/path-to-your-apns-production.p12"
},
```

#### GCM Settings (optional)

```python
"gcm": {
    "api_key": "your gcm api key",
    "sender_id": "your gcm sender id"
},
```





















