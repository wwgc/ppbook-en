# API List


request uri:
```
POST https://ppmessage.com/api/xxxxx
```

`headers`:
```
{
    'Content-Type': 'application/json',
    'Authorization': 'OAuth xxxxx'
}
```

`api_level`: Each api support one or more api_level. You must use token with the right api_level to invoke certain API.

api_level                 | Description
--------------------------|-------------
`PPCOM`                   | To invoke the api, you must request a token using PPCom `api_key` and `api_secret`
`PPKEFU`                  | To invoke the api, you must request a token using PPKefu `api_key` and `api_secret`
`PPCONSOLE`               | To invoke the api, you must request a token using PPConsole `api_key` and `api_secret`
`PPCONSOLE_BEFORE_LOGIN`  | To invoke the api, you must request a token using PPConsole `api_key` and `api_secret`
`THIRD_PARTY_KEFU`        | To invoke the api, you must request a token using THIRD PARTY Kefu `api_key` and `api_secret`
`THIRD_PARTY_CONSOLE`     | To invoke the api, you must request a token using THIRD PARTY Console `api_key` and `api_secret`

As this doc is for third party app, we only care about `THIRD_PARTY_KEFU` and `THIRD_PARTY_CONSOLE` api_level.

note:

* required parameters will show with bold font.

---

#### Create Anonymous User
```
POST /PP_CREATE_ANONYMOUS
```

api_level:
```
PPCom
```

Parameters:

Name                   | Type      | Description
-----------------------|-----------|------------
**app_uuid**           | string    | your service team's uuid
**ppcom_trace_uuid**   | string    | ppcom trace uuid to target user in browser

Response (example):
```
{
    'error_code': 0,
    'error_string': 'success.',
    'uri': '/PP_CREATE_ANONYMOUS',
    'user_fullname': 'Unknown Area.User',
    'user_icon': 'http://127.0.0.1:8080/identicon/7dac54f4-1b11-11e6-8b7a-0242ac110002.png',
    'user_uuid': '7dac54f4-1b11-11e6-8b7a-0242ac110002',
    'user_email': '7dac54@1ca35f'
}
```


#### Create User
```
POST /PP_CREATE_USER
```

api_level:
```
PPCONSOLE, THIRD_PARTY_CONSOLE
```

Parameters:

Name                   | Type      | Description
-----------------------|-----------|-----------------------------
**app_uuid**           | string    | your service team's app_uuid
**user_email**         | string    | user's sign in email
**user_fullname**      | string    | user's fullname
user_language          | string    | user's language, can be: "en", "zh-cn"
user_password          | string    | user's password
is_service_user        | boolean   | whether user is a sevice agent or not
user_status            | string    | user's status, can be: "OWNER_0", "OWNER_1", "OWNER_2", "OWNER_3", "ADMIN", "SERVICE", "ANONYMOUS", "THIRDPARTY". default is "THIRDPARTY"

Response (example):
```
{
    'user_status': u'SERVICE',
    'uuid': '97f90762-1c10-11e6-9869-0242ac110002',
    'error_string': 'success.',
    'is_anonymous_user': False,
    'user_name': u'dancer-info@ppmessage.com',
    'user_password': u'40bd001563085fc35165329ea1ff5c5ecbdbbeef',
    'user_fullname': u'dancer-info',
    'uri': '/PP_CREATE_USER',
    'user_language': None,
    'error_code': 0,
    'user_email': u'dancer-info@ppmessage.com'
}
```


#### Remove User
```
POST /PP_REMOVE_USER
```

api_level:
```
PPCONSOLE, THIRD_PARTY_CONSOLE
```

Parameters:

Name                   | Type      | Description
-----------------------|-----------|------------------------
**user_uuid**          | string    | user's uuid
**user_password**      | string    | user's password

Response (example):

```
{
    'error_cdoe': 0,
    'error_string': 'success.',
    'uri': '/PP_REMOVE_USER'
}
```


#### Update User
```
POST /PP_UPDATE_USER
```

api_level:
```
PPCOM, PPKEFU, PPCONSOLE, THIRD_PARTY_KEFU, THIRD_PARTY_CONSOLE
```

Parameters:

Name                   | Type      | Description
-----------------------|-----------|------------
**app_uuid**           | string    | service team's uuid
**user_uuid**          | string    | user's uuid
is_distributor_user    | boolean   | whether use is a distributor user
old_password           | string    | old password
new_password           | string    | new password

Response (example):

```
{
    'error_cdoe': 0,
    'error_string': 'success.',
    'uri': '/PP_UPDATE_USER'
}
```


#### Create Device
```
POST /PP_CREATE_DEVICE
```

api_level:
```
PPCOM
```

Parameters:

Name                   | Type      | Description
-----------------------|-----------|------------
**app_uuid**           | string    | service team's uuid
**user_uuid**          | string    | user's uuid
**device_id**          | string    | device id
**device_ostype**      | string    | device os type
**ppcom_trace_uuid**   | string    | ppcom trace uuid to target use in browser

device ostype:
```
"AND", # ANDROID
"IOS", # IOS
"ANB", # ANDROID BROWSER
"IOB", # IOS BROWSER
"WIP", # WIN PHONE
"MAC", # MAC OS X PC
"LIN", # LINUX PC
"WIN", # WINDOWS PC
"MAB", # MAC BROWSER
"LIB", # LINUX BROWSER
"WIB", # WINDOWS BROWSER
"W32", # WINDOWS 32 BIT
"W64", # WINDOWS 64 BIT
```

Response (example):
```
{
    'error_code': 25,
    'uri': '/PP_CREATE_DEVICE',
    'error_string': 'device existed.',
    'device_uuid': '3534d9da-1828-11e6-946e-0242ac110002'
}
```


#### Update Device
```
POST /PP_UPDATE_DEVICE
```

api_level:
```
PPCOM, PPKEFU, THIRD_PARTY_KEFU
```

Parameters:

Name                   | Type      | Description
-----------------------|-----------|------------
**device_uuid**        | string    | device uuid
device_fullname        | string    | device fullname
device_phonenumber     | string    | device phone number
device_ostype          | string    | device os type
device_osversion       | string    | device os version
device_android_apilevel| string    | android device api level
device_android_gcmtoken| string    | android device gcm token
device_android_gcmpush | boolean   | whether android device use gcm push
device_ios_model       | string    | iOS device model
device_ios_token       | string    | iOS device token
device_is_online       | boolean   | whether device is online


Response (example):

```
{
    'error_cdoe': 0,
    'error_string': 'success.',
    'uri': '/PP_UPDATE_DEVICE'
}
```


#### Create Conversation
```
POST /PP_CREATE_CONVERSATION
```

api_level:
```
PPCOM, PPKEFU, THIRD_PARTY_KEFU
```

Parameters:

Name                   | Type      | Description
-----------------------|-----------|-----------------------------
**app_uuid**           | string    | service team's uuid
**user_uuid**          | string    | user's uuid
**conversation_type**  | string    | conversation type, can be: "P2S", "S2S"
conversation_name      | string    | conversation name
member_list            | list      | conversation member list, must provided if conversation type is "S2S"
group_uuid             | string    | conversation's group uuid

Response (example):

```
{
    'uri': '/PP_CREATE_CONVERSATION',
    'error_code': 0,
    'error_string': 'success.',
    'status': 'NEW',
    'conversation_type': u'S2S',
    'conversation_icon': None,
    'uuid': '92035b7a-1c1d-11e6-a4dd-0242ac110002',
    'createtime': datetime.datetime(2016, 5, 17, 10, 53, 21, 73728),
    'updatetime': datetime.datetime(2016, 5, 17, 10, 53, 21, 73728),
    'group_uuid': None,
    'createtimestamp': 1463482401.073728,
    'app_uuid': u'1ca35f40-17f1-11e6-9d01-0242ac110003',
    'conversation_name': 'right',
    'updatetimestamp': 1463482401.073728,
    'assigned_uuid': u'89d63aee-1c1d-11e6-a4dd-0242ac110002',
    'user_uuid': u'1ca235d4-17f1-11e6-9d01-0242ac110003',
    'user_list': [u'89d63aee-1c1d-11e6-a4dd-0242ac110002']
}
```

#### Get Conversation Info
```
POST /PP_GET_CONVERSATION_INFO
```

api_level:
```
PPCOM, PPKEFU, PPCONSOLE, THIRD_PARTY_KEFU, THIRD_PARTY_CONSOLE
```

Parameters:

Name                   | Type      | Description
-----------------------|-----------|---------------------------
**conversation_uuid**  | string    | conversation uuid
**app_uuid**           | string    | service team's uuid
**user_uuid**          | string    | user's uuid

Response (example):

```
{
    'status': 'OPEN',
    'conversation_type': 'P2S',
    'updatetime': datetime.datetime(2016, 5, 17, 11, 13, 58, 509645),
    'uuid': '0ab12db4-1c1d-11e6-a4dd-0242ac110002',
    'error_string': 'success.',
    'conversation_data': {
        'conversation_type': 'P2S',
        'updatetime': datetime.datetime(2016, 5, 17, 11, 13, 58, 511172),
        'uuid': '0ab3f9c2-1c1d-11e6-a4dd-0242ac110002',
        'conversation_uuid': '0ab12db4-1c1d-11e6-a4dd-0242ac110002',
        'user_mute_notification': None,
        'conversation_icon': 'http://127.0.0.1:8080/identicon/351f147e-1828-11e6-946e-0242ac110002.png',
        'conversation_status': 'OPEN',
        'app_uuid': '1ca35f40-17f1-11e6-9d01-0242ac110003',
        'user_name': None,
        'conversation_name': 'Unknown Area.User',
        'user_uuid': '1ca235d4-17f1-11e6-9d01-0242ac110003',
        'createtime': datetime.datetime(2016, 5, 17, 10, 49, 34, 57641)
    },
    'latest_task': '119dab7d-98d9-42c7-f4ca-ad80f8a65fdb',
    'user_uuid': '351f147e-1828-11e6-946e-0242ac110002',
    'uri': '/PP_GET_CONVERSATION_INFO',
    'group_uuid': None,
    'conversation_icon': None,
    'app_uuid': '1ca35f40-17f1-11e6-9d01-0242ac110003',
    'conversation_name': None,
    'assigned_uuid': '1ca235d4-17f1-11e6-9d01-0242ac110003',
    'error_code': 0,
    'createtime': datetime.datetime(2016, 5, 17, 10, 49, 34, 56363)
}
```


#### Get All Conversations In A Service Team
```
POST /PP_GET_APP_CONVERSATION_LIST
```

api_level:
```
PPCOM, PPKEFU, PPCONSOLE, THIRD_PARTY_KEFU, THIRD_PARTY_CONSOLE
```

Parameters:

Name                   | Type      | Description
-----------------------|-----------|-------------------------
**app_uuid**           | string    | service team's uuid

Response (example):

```
{
    'list': [
        {
            'status': 'OPEN',
            'conversation_type': 'P2S',
            'updatetime': datetime.datetime(2016, 5, 17, 11, 13, 58, 509645),
            'uuid': '0ab12db4-1c1d-11e6-a4dd-0242ac110002',
            'latest_message': {
                'body': '2',
                'conversation_type': 'P2S',
                'updatetime': datetime.datetime(2016, 5, 17, 11, 13, 58, 519090),
                'uuid': '119dab7d-98d9-42c7-f4ca-ad80f8a65fdb',
                'from_uuid': '351f147e-1828-11e6-946e-0242ac110002',
                'conversation_uuid': '0ab12db4-1c1d-11e6-a4dd-0242ac110002',
                'title': None,
                'to_device_uuid': None,
                'from_type': 'DU',
                'from_device_uuid': '3534d9da-1828-11e6-946e-0242ac110002',
                'is_development': None,
                'to_type': 'AP',
                'app_uuid': '1ca35f40-17f1-11e6-9d01-0242ac110003',
                'to_uuid': '0ab12db4-1c1d-11e6-a4dd-0242ac110002',
                'message_body': '{
                    "ci": "0ab12db4-1c1d-11e6-a4dd-0242ac110002",
                    "ft": "DU",
                    "tt": "AP",
                    "bo": "2",
                    "ts": 1463483638.508707,
                    "mt": "NOTI",
                    "tl": null,
                    "ms": "TEXT",
                    "ti": "0ab12db4-1c1d-11e6-a4dd-0242ac110002",
                    "fi": "351f147e-1828-11e6-946e-0242ac110002",
                    "id": "119dab7d-98d9-42c7-f4ca-ad80f8a65fdb",
                    "ct": "P2S"
                 }',
                'task_status': 'PROCESSED',
                'message_type': 'NOTI',
                'createtime': datetime.datetime(2016, 5, 17, 11, 13, 58, 508707),
                'message_subtype': 'TEXT'
            },
            'latest_task': '119dab7d-98d9-42c7-f4ca-ad80f8a65fdb',
            'conversation_icon': None,
            'group_uuid': None,
            'create_user': {
                'user_firstname': None,
                'user_mute_other_mobile_device': None,
                'create_status': None,
                'user_wechat': None,
                'mobile_device_uuid': None,
                'user_company': None,
                'user_status': 'ANONYMOUS',
                'ppcom_browser_device_uuid': '3534d9da-1828-11e6-946e-0242ac110002',
                'uuid': '351f147e-1828-11e6-946e-0242ac110002',
                'user_lastname': None,
                'user_qq': None,
                'user_icon': 'http://127.0.0.1:8080/identicon/351f147e-1828-11e6-946e-0242ac110002.png',
                'user_defined': None,
                'user_mobile': None,
                'user_signature': None,
                'is_email_verified': None,
                'browser_device_uuid': None,
                'user_name': 'Unknown Area.User',
                'is_anonymous_user': True,
                'service_user_status': None,
                'ppcom_trace_uuid': 'ce4253cc-6fd6-45ae-ebe5-042e74aa46c1',
                'user_show_badge': None,
                'user_language': None,
                'latest_send_message_time': datetime.datetime(2016, 5, 12, 9, 59, 56),
                'updatetime': datetime.datetime(2016, 5, 17, 9, 59, 6, 686846),
                'user_silence_notification': None,
                'is_mobile_verified': None,
                'user_fullname': 'Unknown Area.User',
                'createtime': datetime.datetime(2016, 5, 12, 9, 59, 26),
                'user_mute_notification': None,
                'ppcom_mobile_device_uuid': None,
                'user_email': '351f14@1ca35f'
            },
            'app_uuid': '1ca35f40-17f1-11e6-9d01-0242ac110003',
            'conversation_name': None,
            'message_total_count': 1,
            'assigned_uuid': '1ca235d4-17f1-11e6-9d01-0242ac110003',
            'user_uuid': '351f147e-1828-11e6-946e-0242ac110002',
            'createtime': datetime.datetime(2016, 5, 17, 10, 49, 34, 56363)
        }
    ],
    'error_code': 0,
    'uri': '/PP_GET_APP_CONVERSATION_LIST',
    'error_string': 'success.'
}
```


#### Get User Conversation List
```
POST /PP_GET_USER_CONVERSATION_LIST
```

api_level:
```
PPCOM, PPKEFU, PPCONSOLE, THIRD_PARTY_KEFU, THIRD_PARTY_CONSOLE
```

Parameters:

Name                   | Type      | Description
-----------------------|-----------|------------
**app_uuid**           | string    | service team's uuid
**user_uuid**          | string    | user's uuid

Response (example):
```
{
    'list': [],
    'error_code': 0,
    'uri': '/PP_GET_USER_CONVERSATION_LIST',
    'error_string': 'success.'
}
```


#### Open Conversation

If a conversation status is `CLOSE`, when you invoke api to get conversation list, this conversation will always be ignored. To cancel this feature, you need to set conversation status to be `OPEN`.

```
POST /PP_OPEN_CONVERSATION
```

api_level:
```
PPCOM, PPKEFU, PPCONSOLE, THIRD_PARTY_KEFU, THIRD_PARTY_CONSOLE
```

Parameters:

Name                   | Type      | Description
-----------------------|-----------|------------
**app_uuid**           | string    | service team's uuid
**user_uuid**          | string    | user uuid
**conversation_uuid**  | string    | conversation uuid

Response (example):
```
{
    'uri': '/PP_OPEN_CONVERSATION',
    'error_code': 0,
    'error_string': 'success.'
}
```


#### Close Conversation

If a conversation status is `CLOSE`, when you invoke api to get conversation list, this conversation will always be ignored.

```
POST /PP_CLOSE_CONVERSATION
```

api_level:
```
PPCOM, PPKEFU, PPCONSOLE, THIRD_PARTY_KEFU, THIRD_PARTY_CONSOLE
```

Parameters:

Name                   | Type      | Description
-----------------------|-----------|------------
**app_uuid**           | string    | service team's uuid
**user_uuid**          | string    | user uuid
**conversation_uuid**  | string    | conversation uuid

Response (example):
```
{
    'uri': '/PP_OPEN_CONVERSATION',
    'error_code': 0,
    'error_string': 'success.'
}
```


#### Get service team info
```
POST /PP_GET_APP_INFO
```

api_level:
```
PPCOM, PPKEFU, PPCONSOLE, THIRD_PARTY_KEFU, THIRD_PARTY_CONSOLE
```

Parameters:

Name                   | Type      | Description
-----------------------|-----------|------------
**app_uuid**           | string    | service team's uuid

Response (example):
```
{
    'return_offline_message': None,
    'app_name': 'ppmessage',
    'app_secret': 'Mzg2ODliNjVlY2I2NzBlNTExMmJkMTE4YzM3MjRlMjUxN2U1MjEwMg==',
    'robot_user_uuid': None,
    'api_uuid': '1ca64836-17f1-11e6-9d01-0242ac110003',
    'robot_train_track': None,
    'app_billing_email': None,
    'uuid': '1ca35f40-17f1-11e6-9d01-0242ac110003',
    'welcome_message': None,
    'app_icon': None,
    'ppcom_powered_by_visible': None,
    'ppcom_powered_by_link': None,
    'company_name': 'YOURUI',
    'ppcom_launcher_style': None,
    'ppcom_powered_by_name': None,
    'robot_train_click': None,
    'offline_message': None,
    'app_key': 'NjZlZGNiMGEzOTg4NmNjYWQ2NDIxNDZiN2ZiZTljZTA1NTFiZjdlNw==',
    'show_ppcom_hover': None,
    'updatetime': datetime.datetime(2016, 5, 12, 3, 25, 1),
    'app_route_policy': None,
    'error_string': 'success.',
    'robot_train_method': None,
    'user_uuid': '1ca235d4-17f1-11e6-9d01-0242ac110003',
    'uri': '/PP_GET_APP_INFO',
    'robot_train_chat': None,
    'app_billing_uuid': None,
    'error_code': 0,
    'createtime': datetime.datetime(2016, 5, 12, 3, 25, 1),
    'ppcom_launcher_color': None
}
```


#### Get All Service User In A Service Team
```
POST /PP_GET_APP_SERVICE_USER_LIST
```

api_level:
```
PPCOM, PPKEFU, PPCONSOLE, THIRD_PARTY_KEFU, THIRD_PARTY_CONSOLE
```

Parameters:

Name                   | Type      | Description
-----------------------|-----------|------------
**app_uuid**           | string    | service team's uuid

Response (example):
```
{
    'list': [
        {
            'updatetime': datetime.datetime(2016, 5, 18, 2, 36, 19, 726229),
            'group': None,
            'uuid': '1ca235d4-17f1-11e6-9d01-0242ac110003',
            'user_fullname': 'Jin He',
            'user_icon': '01a17ddc-1821-11e6-9b56-0242ac110003',
            'is_browser_online': True,
            'user_signature': 'fight to the death ~',
            u'is_owner_user': True,
            'is_mobile_online': False,
            u'is_distributor_user': True,
            'user_email': 'jin.he@ppmessage.com',
            u'is_service_user': True
        },
        {
            'updatetime': datetime.datetime(2016, 5, 17, 10, 53, 7),
            'group': None,
            'uuid': '89d63aee-1c1d-11e6-a4dd-0242ac110002',
            'user_fullname': 'right',
            'user_icon': None,
            'is_browser_online': False,
            'user_signature': None,
            u'is_owner_user': False,
            'is_mobile_online': False,
            u'is_distributor_user': True,
            'user_email': 'right@ppmessage.com',
            u'is_service_user': True
        }
    ],
    'error_code': 0,
    'uri': '/PP_GET_APP_SERVICE_USER_LIST',
    'error_string': 'success.'
}
```

#### Get User Uuid

Check whether there is a user corresponding to a email. If there is no such user, create this user and return his uuid. Otherwise, if user is a service agent, return error, or return user's uuid.

```
POST /PP_GET_USER_UUID
```

api_level:
```
PPCOM
```

Parameters:

Name                   | Type      | Description
-----------------------|-----------|------------
**app_uuid**           | string    | service team's uuid
**user_email**         | string    | user email
user_icon              | string    | user icon, used when need to create user
user_fullname          | string    | user fullname, used when need to create user

Response (example):
```
{
    'error_code': 0,
    'error_string': 'success.',
    'uri': '/PP_GET_USER_UUID',
    'user_uuid': '1ca64836-17f1-11e6-9d01-0242ac110003'
}
```


#### Get History Message Of A Conversation

Get history messages in a conversation, by page(`page_size` and `page_offset`), or message id region(`since_id` and `max_id`)

```
POST /PP_GET_HISTORY_MESSAGE
```

api_level:
```
PPCOM, PPKEFU, PPCONSOLE, THIRD_PARTY_KEFU, THIRD_PARTY_CONSOLE
```

Parameters:

Name                   | Type      | Description
-----------------------|-----------|------------
**conversation_uuid**  | string    | conversation uuid
**page_offset**        | string    | which page server returns
page_size              | string    | how many messages server returns in one page
since_id               | string    | since message id
max_id                 | string    | max message id


Response (example):
```
{
   'error_code': 0,
   'error_code': 'success.',
   'uri': '/PP_GET_HISTORY_MESSAGE',
   'total_count': 23,
   'count': 12,
   'page_size': 12,
   'page_offset': 0,
   'list': [
       ...
   ],
   'max_id': 'xxxx'
}
```


#### Get User Info
```
POST /PP_GET_USER_INFO
```

api_level:
```
PPCOM, PPKEFU, PPCONSOLE, THIRD_PARTY_KEFU, THIRD_PARTY_CONSOLE
```

Parameters:

Name                   | Type      | Description
-----------------------|-----------|------------
**app_uuid**           | string    | servie team's uuid
**user_uuid**          | string    | user's uuid


Response (example):
```
{
...
}
```


#### Get All Service Group In A Service Team
```
POST /PP_GET_APP_ORG_GROUP_LIST
```

api_level:
```
PPCOM, PPKEFU, PPCONSOLE, THIRD_PARTY_KEFU, THIRD_PARTY_CONSOLE
```

Parameters:

Name                   | Type      | Description
-----------------------|-----------|------------
**app_uuid**           | string    | service team's uuid

Response (example):
```
{
    'list': [
        {
            'updatetime': '2016-05-18 04:56:45 515792',
            'user_count': 2,
            'group_icon': 'http://127.0.0.1:8080/identicon/be625d18d0b96a0b2e2e26c95a4b59e1625348ab.png',
            'uuid': 'e00ab5b0-1cb4-11e6-9894-0242ac110002',
            'conversation_uuid': None,
            'is_distributor': True,
            'group_desc': 'a dancer club',
            'group_name': 'Dancer Club',
            'app_uuid': '1ca35f40-17f1-11e6-9d01-0242ac110003',
            'createtime': '2016-05-18 04:56:26 024830'
        }
    ],
    'error_code': 0,
    'uri': '/PP_GET_APP_ORG_GROUP_LIST',
    'error_string': 'success.'
}
```


#### Get service group's info
```
POST /PP_GET_ORG_GROUP_DETAIL
```

api_level:
```
PPCOM, PPKEFU, PPCONSOLE, THIRD_PARTY_KEFU, THIRD_PARTY_CONSOLE
```

Parameters:

Name                   | Type      | Description
-----------------------|-----------|------------
**app_uuid**           | string    | service team's uuid
**group_uuid**         | string    | service group's uuid

Response (example):
```
{
    'group_route_algorithm': None,
    'group_visible_order_for_ppcom': None,
    'updatetime': datetime.datetime(2016, 5, 18, 4, 56, 45, 515792),
    'uuid': 'e00ab5b0-1cb4-11e6-9894-0242ac110002',
    'error_string': 'success.',
    'conversation_uuid': None,
    'createtime': datetime.datetime(2016, 5, 18, 4, 56, 26, 24830),
    'is_distributor': True,
    'uri': '/PP_GET_ORG_GROUP_DETAIL',
    'group_desc': 'a dancer club',
    'is_root': None,
    'group_uuid': 'e00ab5b0-1cb4-11e6-9894-0242ac110002',
    'app_uuid': '1ca35f40-17f1-11e6-9d01-0242ac110003',
    'group_work_time_str': None,
    'group_name': 'Dancer Club',
    'error_code': 0,
    'group_icon': 'http://127.0.0.1:8080/identicon/be625d18d0b96a0b2e2e26c95a4b59e1625348ab.png',
    'group_visible_for_ppcom': None
}
```


#### Get All Service Users In A Service Group

```
POST /PP_GET_ORG_GROUP_USER_LIST
```

api_level:
```
PPCOM, PPKEFU, PPCONSOLE, THIRD_PARTY_KEFU, THIRD_PARTY_CONSOLE
```

Parameters:

Name                   | Type      | Description
-----------------------|-----------|------------
**app_uuid**           | string    | service team's uuid
**group_uuid**         | string    | service group's uuid

Response (example):
```
{
    'list': [
        {
            'updatetime': 1463547414,
            'group': {
                'uuid': 'e00ab5b0-1cb4-11e6-9894-0242ac110002',
                'group_name': 'Dancer Club'
            },
            'uuid': '1ca235d4-17f1-11e6-9d01-0242ac110003',
            'user_fullname': 'Jin He',
            'user_icon': '01a17ddc-1821-11e6-9b56-0242ac110003',
            'is_browser_online': True,
            'user_signature': 'fight to the death ~',
            'is_mobile_online': False,
            'user_email': 'jin.he@ppmessage.com'
        },
        {
            'updatetime': 1463482387,
            'group': {
                'uuid': 'e00ab5b0-1cb4-11e6-9894-0242ac110002',
                'group_name': 'Dancer Club'
            },
            'uuid': '89d63aee-1c1d-11e6-a4dd-0242ac110002',
            'user_fullname': 'right',
            'user_icon': None,
            'is_browser_online': False,
            'user_signature': None,
            'is_mobile_online': False,
            'user_email': 'right@ppmessage.com'
        }
    ],
    'error_code': 0,
    'uri': '/PP_GET_ORG_GROUP_USER_LIST',
    'error_string': 'success.'
}
```


#### Create Service Group
```
POST /PP_CREATE_ORG_GROUP
```

api_level:
```
PPCONSOLE, THIRD_PARTY_CONSOLE
```

Parameters:

Name                   | Type      | Description
-----------------------|-----------|------------
**app_uuid**           | string    | service group's uuid
**group_name**         | string    | service group's name
**group_desc**         | string    | service group's decription
is_distributor         | boolean   | whether service group is primary group

Response (example):
```
{
    'group_visible_order_for_ppcom': None,
    'group_desc': 'a music club',
    'group_name': 'Music Club',
    'is_root': None,
    'group_work_time_str': None,
    'group_visible_for_ppcom': None,
    'group_route_algorithm': None,
    'updatetime': datetime.datetime(2016, 5, 18, 6, 22, 1, 125540),
    'uuid': 'd4c8c2bc-1cc0-11e6-b348-0242ac110002',
    'error_string': 'success.',
    'is_distributor': False,
    'uri': '/PP_CREATE_ORG_GROUP',
    'createtime': datetime.datetime(2016, 5, 18, 6, 22, 1, 125540),
    'app_uuid': '1ca35f40-17f1-11e6-9d01-0242ac110003',
    'error_code': 0,
    'group_icon': 'http://127.0.0.1:8080/identicon/d4c8c2bc-1cc0-11e6-b348-0242ac110002.png'
}
```


#### Update Service Group
```
POST /PP_UPDATE_ORG_GROUP
```

api_level:
```
PPCONSOLE, THIRD_PARTY_CONSOLE
```

Parameters:

Name                   | Type      | Description
-----------------------|-----------|-----------------------------
**app_uuid**           | string    | service team's uuid
**group_uuid**         | string    | service group's uuid
group_name             | string    | service group's name
group_icon             | string    | service group's icon
group_desc             | string    | service group's description
is_distributor         | boolean   | whether service group is primary group


Response (example):
```
{
    'group_route_algorithm': None,
    'group_visible_order_for_ppcom': None,
    'updatetime': datetime.datetime(2016, 5, 18, 4, 56, 45, 515792),
    'uuid': 'e00ab5b0-1cb4-11e6-9894-0242ac110002',
    'error_string': 'success.',
    'createtime': datetime.datetime(2016, 5, 18, 4, 56, 26, 24830),
    'is_distributor': True,
    'uri': '/PP_UPDATE_ORG_GROUP',
    'group_desc': u'a dancer club',
    'is_root': None,
    'group_uuid': 'e00ab5b0-1cb4-11e6-9894-0242ac110002',
    'app_uuid': '1ca35f40-17f1-11e6-9d01-0242ac110003',
    'group_work_time_str': None,
    'group_name': u'Dancer Club',
    'error_code': 0,
    'group_icon': 'http://127.0.0.1:8080/identicon/be625d18d0b96a0b2e2e26c95a4b59e1625348ab.png',
    'group_visible_for_ppcom': None
}
```


#### Remove Service Group
```
POST /PP_REMOVE_ORG_GROUP
```

api_level:
```
PPCONOSLE, THIRD_PARTY_CONSOLE
```

Parameters:

Name                   | Type      | Description
-----------------------|-----------|------------
**app_uuid**           | string    | service team's uuid
**group_uuid**         | string    | service group's uuid

Response (example):
```
{
    'error_code': 0,
    'uri': '/PP_REMOVE_ORG_GROUP',
    'error_string': 'success.'
}
```


#### Add Service Agent To A Service Group
```
POST /PP_ADD_ORG_GROUP_USER
```

api_level:
```
PPCONOSLE, THIRD_PARTY_CONSOLE
```

Parameters:

Name                   | Type      | Description
-----------------------|-----------|-----------------------------
**app_uuid**           | string    | service team's uuid
**group_uuid**         | string    | service group's uuid
**user_list**          | list      | service agents to add to service group

Response (example):
```
{
    'error_code': 0,
    'uri': '/PP_ADD_ORG_GROUP_USER',
    'error_string': 'success.'
}
```


#### Remove Service Agents From A Service Group
```
POST /PP_REMOVE_ORG_GROUP_USER
```

api_level:
```
PPCONOSLE, THIRD_PARTY_CONSOLE
```

Parameters:

Name                   | Type      | Description
-----------------------|-----------|------------
**app_uuid**           | string    | service team's uuid
**group_uuid**         | string    | service group's uuid
**user_list**          | list      | service agents to remove from service group

Response (example):
```
{
    'error_code': 0,
    'uri': '/PP_REMOVE_ORG_GROUP_USER',
    'error_string': 'success.'
}
```


#### Get All Service Agents That Don't Belong To Any Service Group In A Service Team.
```
POST /PP_GET_NO_GROUP_USER_LIST
```

api_level:
```
PPCOM, PPKEFU, PPCONOSLE, THIRD_PARTY_KEFU, THIRD_PARTY_CONSOLE
```

Parameters:

Name                   | Type      | Description
-----------------------|-----------|------------
**app_uuid**           | string    | service team's uuid

Response (example):
```
{
    'list': [
        {
            'user_status': 'ADMIN',
            'updatetime': '2016-05-18 04:56:54 905611',
            'uuid': '1ca235d4-17f1-11e6-9d01-0242ac110003',
            'is_anonymous_user': 'False',
            'user_lastname': 'He',
            'user_password': '40bd001563085fc35165329ea1ff5c5ecbdbbeef',
            'user_fullname': 'Jin He',
            'service_user_status': 'READY',
            'user_icon': '01a17ddc-1821-11e6-9b56-0242ac110003',
            'user_signature': 'fight to the death ~',
            'user_email': 'jin.he@ppmessage.com',
            'browser_device_uuid': '68a2feca-1c1d-11e6-a4dd-0242ac110002',
            'user_language': 'zh_cn',
            'createtime': '2016-05-12 03:25:01 000000',
            'latest_send_message_time': '2016-05-12 10:01:18 000000',
            'user_firstname': 'Jin'
        },
        {
            'user_status': 'SERVICE',
            'updatetime': '2016-05-17 10:53:07 000000',
            'uuid': '89d63aee-1c1d-11e6-a4dd-0242ac110002',
            'is_anonymous_user': 'False',
            'user_password': '40bd001563085fc35165329ea1ff5c5ecbdbbeef',
            'user_fullname': 'right',
            'user_name': 'right@ppmessage.com',
            'createtime': '2016-05-17 10:53:07 000000',
            'user_email': 'right@ppmessage.com'
        },
        {
            'user_status': 'SERVICE',
            'updatetime': '2016-05-18 08:15:16 552382',
            'uuid': 'a7341f62-1cd0-11e6-950f-0242ac110002',
            'is_anonymous_user': 'False',
            'user_password': '40bd001563085fc35165329ea1ff5c5ecbdbbeef',
            'user_fullname': 'gitar',
            'user_name': 'gitar@ppmessage.com',
            'createtime': '2016-05-18 08:15:16 552382',
            'user_email': 'gitar@ppmessage.com'
        }
    ],
    'error_code': 0,
    'uri': '/PP_GET_NO_GROUP_USER_LIST',
    'error_string': 'success.'
}
```


#### Get All Conversations Related To A Service Group

```
POST /PP_GET_ORG_GROUP_CONVERSATION
```

api_level:
```
PPCOM
```

Parameters:

Name                   | Type      | Description
-----------------------|-----------|----------------------------
**app_uuid**           | string    | service team's uuid
**group_uuid**         | string    | service group's uuid
**user_uuid**          | string    | user's uuid，this user is a PPCom user

Response (example):
```
{
    'conversation_uuid': '68a2feca-1c1d-11e6-a4dd-0242ac110002',
    'error_code': 0,
    'uri': '/PP_GET_NO_GROUP_USER_LIST',
    'error_string': 'success.'
}
```


#### Update Conversation Member
```
POST /PP_UPDATE_CONVERSATION_MEMBER
```

api_level:
```
PPCOM, PPKEFU, THIRD_PARTY_KEFU
```

Parameters:

Name                   | Type      | Description
-----------------------|-----------|------------
**app_uuid**           | string    | service team's uuid
**conversation_uuid**  | string    | conversation uuid
group_uuid             | string    | service group uuid, set this conversation related to that service group
action                 | string    | operation type，can be: "ADD" or "REMOVE"
member_list            | list      | the member list to add or remove

Response (example):
```
{
    'error_code': 0,
    'error_string': 'success.',
    'uri': '/PP_UPDATE_CONVERSATION_MEMBER'
}
```


#### Get Default Conversation

PPCom invoke this api the get default conversation.

```
POST /PPCOM_GET_DEFAULT_CONVERSATION
```

api_level:
```
PPCOM
```

Parameters:

Name                   | Type      | Description
-----------------------|-----------|------------
**app_uuid**           | string    | service team's uuid
**user_uuid**          | string    | user's uuid, this user is a PPCom user
**device_uuid**        | string    | user device uuid, this user is a PPCom user

Response (example):
```
{
    'status': 'OPEN',
    'conversation_type': 'P2S',
    'app_name': 'ppmessage',
    'latest_task': '771d934d-9629-46df-d635-380858dd114a',
    'conversation_icon': 'http://127.0.0.1:8080/identicon/be625d18d0b96a0b2e2e26c95a4b59e1625348ab.png',
    'group_uuid': None,
    'updatetime': datetime.datetime(2016, 5, 18, 4, 43, 55, 628687),
    'app_welcome': '\xe6\x9c\x89\xe4\xbb\x80\xe4\xb9\x88\xe5\x8f\xaf\xe4\xbb\xa5\xe5\xb8\xae\xe5\xbf\x99\xe7\x9a\x84\xef\xbc\x8c\xe4\xb8\x80\xe8\xb5\xb7\xe8\x81\x8a\xe4\xb8\xa4\xe5\x8f\xa5\xe5\x90\xa7\xef\xbc\x9f',
    'uuid': '1efd668e-1cb3-11e6-93e2-0242ac110002',
    'error_string': 'success.',
    'user_uuid': '9adb1032-1cac-11e6-bce9-0242ac110002',
    'uri': '/PPCOM_GET_DEFAULT_CONVERSATION',
    'user_list': [
        {
            'updatetime': 1463563427,
            'group': None,
            'uuid': '9adb1032-1cac-11e6-bce9-0242ac110002',
            'user_fullname': 'Unknown Area.User',
            'user_icon': 'http://127.0.0.1:8080/identicon/9adb1032-1cac-11e6-bce9-0242ac110002.png',
            'is_browser_online': False,
            'user_signature': None,
            'is_mobile_online': False,
            'user_email': '9adb10@1ca35f'
        },
        {
            'updatetime': 1463547414,
            'group': None,
            'uuid': '1ca235d4-17f1-11e6-9d01-0242ac110003',
            'user_fullname': 'Jin He',
            'user_icon': '01a17ddc-1821-11e6-9b56-0242ac110003',
            'is_browser_online': True,
            'user_signature': 'fight to the death ~',
            'is_mobile_online': False,
            'user_email': 'jin.he@ppmessage.com'
        },
        {
            'updatetime': 1463482387,
            'group': None,
            'uuid': '89d63aee-1c1d-11e6-a4dd-0242ac110002',
            'user_fullname': 'right',
            'user_icon': None,
            'is_browser_online': False,
            'user_signature': None,
            'is_mobile_online': False,
            'user_email': 'right@ppmessage.com'
        }
    ],
    'app_uuid': '1ca35f40-17f1-11e6-9d01-0242ac110003',
    'conversation_name': 'Jin He,right',
    'assigned_uuid': None,
    'error_code': 0,
    'createtime': datetime.datetime(2016, 5, 18, 4, 43, 52, 603049)
}
```


#### Select Service Agents By Group Algorithm
```
POST /PP_SELECT_USERS_BY_GROUP_ALGORITHM
```

api_level:
```
PPCOM, PPKEFU, PPCONSOLE, THIRD_PARTY_KEFU, THIRD_PARTY_CONSOLE
```

Parameters:

Name                   | Type      | Description
-----------------------|-----------|------------
**app_uuid**           | string    | service team's uuid
**group_uuid**         | string    | service group's uuid
**conversation_uuid**  | string    | conversation uuid

Response (example):
```
{
    'list': [
        '1ca235d4-17f1-11e6-9d01-0242ac110003',
        '89d63aee-1c1d-11e6-a4dd-0242ac110002'
    ],
    'error_code': 0,
    'uri': '/PP_SELECT_USERS_BY_GROUP_ALGORITHM',
    'error_string': 'success.'
}
```

#### Update Service Team Info
```
POST /PP_UPDATE_APP_INFO
```

api_level:
```
PPCONSOLE, THIRD_PARTY_CONSOLE
```

Parameters:

Name                   | Type      | Description
-----------------------|-----------|------------
**app_uuid**           | string    | service team uuid
app_name               | string    | service team name
app_icon               | string    | service team icon
app_route_policy       | string    | service team messsage dispatch policy, can be: "ALL", "SMART", "GROUP"
welcome_message        | string    | service team PPCom welcome note
ppcom_launcher_color   | string    | service team PPCom Icon color
ppcom_launcher_style   | string    | service team PPCom Icon style

Response (example):
```
{
    'return_offline_message': None,
    'app_name': 'ppmessage123',
    'robot_train_click': None,
    'app_secret': 'Mzg2ODliNjVlY2I2NzBlNTExMmJkMTE4YzM3MjRlMjUxN2U1MjEwMg==',
    'robot_user_uuid': None,
    'app_key': 'NjZlZGNiMGEzOTg4NmNjYWQ2NDIxNDZiN2ZiZTljZTA1NTFiZjdlNw==',
    'ppcom_powered_by_visible': None,
    'robot_train_method': None,
    'api_uuid': '1ca64836-17f1-11e6-9d01-0242ac110003',
    'ppcom_launcher_style': None,
    'robot_train_track': None,
    'show_ppcom_hover': None,
    'ppcom_powered_by_name': None,
    'app_billing_email': None,
    'updatetime': datetime.datetime(2016, 5, 18, 9, 57, 22, 455405),
    'app_route_policy': None,
    'uuid': '1ca35f40-17f1-11e6-9d01-0242ac110003',
    'error_string': 'success.',
    'welcome_message': None,
    'user_uuid': '1ca235d4-17f1-11e6-9d01-0242ac110003',
    'app_icon': None,
    'uri': '/PP_UPDATE_APP_INFO',
    'createtime': datetime.datetime(2016, 5, 12, 3, 25, 1),
    'ppcom_powered_by_link': None,
    'robot_train_chat': None,
    'company_name': 'YOURUI',
    'app_billing_uuid': None,
    'error_code': 0,
    'offline_message': None,
    'ppcom_launcher_color': None
}
```


#### Get Service Team Owned By User

```
POST /PP_GET_APP_OWNED_BY_USER
```

api_level:
```
PPCOM, PPKEFU, PPCONSOLE, THIRD_PARTY_KEFU, THIRD_PARTY_CONSOLE
```

Parameters:

Name                    | Type      | Description
------------------------|-----------|-------------------------
**user_uuid**           | string    | service team uuid

Response (example):
```
{
    'app': {
        'return_offline_message': None,
        'app_name': 'ppmessage123',
        'app_secret': 'Mzg2ODliNjVlY2I2NzBlNTExMmJkMTE4YzM3MjRlMjUxN2U1MjEwMg==',
        'robot_user_uuid': None,
        'api_uuid': '1ca64836-17f1-11e6-9d01-0242ac110003',
        'robot_train_track': None,
        'app_billing_email': None,
        'uuid': '1ca35f40-17f1-11e6-9d01-0242ac110003',
        'welcome_message': None,
        'robot_train_click': None,
        'ppcom_powered_by_visible': None,
        'ppcom_powered_by_link': None,
        'company_name': 'YOURUI',
        'ppcom_launcher_style': None,
        'ppcom_powered_by_name': None,
        'app_icon': None,
        'offline_message': None,
        'app_key': 'NjZlZGNiMGEzOTg4NmNjYWQ2NDIxNDZiN2ZiZTljZTA1NTFiZjdlNw==',
        'show_ppcom_hover': None,
        'updatetime': datetime.datetime(2016, 5, 18, 9, 57, 22, 455405),
        'app_route_policy': None,
        'robot_train_method': None,
        'robot_train_chat': None,
        'app_billing_uuid': None,
        'user_uuid': '1ca235d4-17f1-11e6-9d01-0242ac110003',
        'createtime': datetime.datetime(2016, 5, 12, 3, 25, 1),
        'ppcom_launcher_color': None
    },
    'bill': None,
    'error_code': 0,
    'uri': '/PP_GET_APP_OWNED_BY_USER',
    'error_string': 'success.'
}
```


#### Validate Email Is Valid
```
Post /PP_IS_EMAIL_VALID
```

api_level:
```
PPCONSOLE, THIRD_PARTY_CONSOLE
```

Parameters:

Name                    | Type      | Description
------------------------|-----------|------------
**user_email**          | string    | service team's uuid

Response (example):
```
{
    'valid': False,
    'uri': '/PP_IS_EMAIL_VALID',
    'error_code': 0,
    'error_string': 'success.'
}
```


#### Create Service Team
```
POST /PP_CREATE_APP
```

api_level:
```
PPCONSOLE, THIRD_PARTY_CONSOLE
```

Parameters:

Name                    | Type      | Description
------------------------|-----------|----------------------------------
**user_uuid**           | string    | user uuid, this user is the service team's administrator
**app_name**            | string    | service team's name

Response (example):
```
{
    'uri': '/PP_CREATE_APP',
    'error_code': 0,
    'error_string': 'success.',
    'uuid': '82baa504-1ce2-11e6-b4ca-0242ac110002',
    'app_name': 'nodejs',
    'app_billing_email': 'nodejs@ppmessage.com',
    'app_key': '82baa324-1ce2-11e6-b4ca-0242ac110002',
    'app_secret': '82baa464-1ce2-11e6-b4ca-0242ac110002',
    'app_route_policy': 'BROADCAST'
}
```


#### Remove Service Agents From A Service Team
```
POST /PP_LEAVE_APP
```

api_level:
```
PPCONSOLE, THIRD_PARTY_CONSOLE
```

Parameters:

Name                    | Type      | Description
------------------------|-----------|------------
**app_uuid**            | string    | service team uuid
**user_list**           | list      | the member list to remove from service team

Response (example):
```
{
    'uri': '/PP_LEAVE_APP',
    'error_code': 0,
    'error_string': 'success.'
}
```


#### Remove Service Team
```
POST /PP_REMOVE_APP
```

api_level:
```
PPCONSOLE, THIRD_PARTY_CONSOLE
```

Parameters:

Name                    | Type      | Description
------------------------|-----------|------------
**app_uuid**            | string    | service team's uuid
**user_uuid**           | string    | the service team administrator's uuid

Response (example):
```
{
    'uri': '/PP_REMOVE_APP',
    'error_code': 0,
    'error_string': 'success.'
}
```


#### Get Conversation Member List
```
POST /PP_GET_CONVERSATION_USER_LIST
```

api_level:
```
PPCOM, PPKEFU, PPCONSOLE, THIRD_PARTY_KEFU, THIRD_PARTY_CONSOLE
```

Parameters:

Name                    | Type      | Description
------------------------|-----------|------------
**app_uuid**            | string    | service team's uuid
**conversation_uuid**   | string    | conversation uuid

Response (example):
```
{
    'list': [
        {
            'updatetime': datetime.datetime(2016, 5, 18, 9, 39, 50, 243510),
            'group': {
                'uuid': '71a93470-1cdc-11e6-bdfe-0242ac110002',
                'group_name': 'Dancer Club'
            },
            'uuid': '1ca235d4-17f1-11e6-9d01-0242ac110003',
            'user_fullname': 'Jin He',
            'user_icon': '01a17ddc-1821-11e6-9b56-0242ac110003',
            'is_browser_online': True,
            'user_signature': 'fight to the death ~',
            'is_mobile_online': False,
            'user_email': 'jin.he@ppmessage.com'
        },
        {
            'updatetime': datetime.datetime(2016, 5, 17, 10, 53, 7),
            'group': {
                'uuid': '71a93470-1cdc-11e6-bdfe-0242ac110002',
                'group_name': 'Dancer Club'
            },
            'uuid': '89d63aee-1c1d-11e6-a4dd-0242ac110002',
            'user_fullname': 'right',
            'user_icon': None,
            'is_browser_online': False,
            'user_signature': None,
            'is_mobile_online': False,
            'user_email': 'right@ppmessage.com'
        },
        {
            'updatetime': datetime.datetime(2016, 5, 18, 9, 23, 47, 399007),
            'group': None,
            'uuid': '9adb1032-1cac-11e6-bce9-0242ac110002',
            'user_fullname': 'Unknown Area.User',
            'user_icon': 'http://127.0.0.1:8080/identicon/9adb1032-1cac-11e6-bce9-0242ac110002.png',
            'is_browser_online': False,
            'user_signature': None,
            'is_mobile_online': False,
            'user_email': '9adb10@1ca35f'
        }
    ],
    'error_code': 0,
    'uri': '/PP_GET_CONVERSATION_USER_LIST',
    'error_string': 'success.'
}
```


#### Get Conversations Related To A Service Agent By Page

```
POST /PP_PAGE_USER_CONVERSATION
```

api_level:
```
PPCOM, PPKEFU, THIRD_PARTY_KEFU
```

Parameters:

Name                    | Type      | Description
------------------------|-----------|------------
**app_uuid**            | string    | service team's uuid
**user_uuid**           | string    | user uuid
page_offset             | number    | page offset, need to provide when get by page
page_size               | number    | page size, need to provide when get by page
min_uuid                | string    | oldest conversation's uuid, need to provide when get by conversation uuid section
max_uuid                | string    | newest conversation's uuid, need to provide when get by conversation uuid section

Response (example):
```
{
    'list': [
        {
            'status': 'OPEN',
            'conversation_type': 'P2S',
            'updatetime': '2016-05-18 04:43:55 628687',
            'uuid': '1efd668e-1cb3-11e6-93e2-0242ac110002',
            'latest_message': {
                'message_body': '{
                    "ci": "1efd668e-1cb3-11e6-93e2-0242ac110002",
                    "ft": "DU",
                    "tt": "AP",
                    "bo": "hi",
                    "ts": 1463546635.627932,
                    "mt": "NOTI",
                    "tl": null,
                    "ms": "TEXT",
                    "ti": "1efd668e-1cb3-11e6-93e2-0242ac110002",
                    "fi": "9adb1032-1cac-11e6-bce9-0242ac110002",
                    "id": "771d934d-9629-46df-d635-380858dd114a",
                    "ct": "P2S"
                }',
                'body': 'hi',
                'updatetime': '2016-05-18 04:43:55 662741',
                'uuid': '771d934d-9629-46df-d635-380858dd114a',
                'from_uuid': '9adb1032-1cac-11e6-bce9-0242ac110002',
                'from_type': 'DU',
                'message_subtype': 'TEXT',
                'conversation_type': 'P2S',
                'message_type': 'NOTI',
                'createtime': '2016-05-18 04:43:55 627932'
            },
            'latest_task': '771d934d-9629-46df-d635-380858dd114a',
            'conversation_data': {
                'updatetime': '2016-05-18 04:43:55 631181',
                'uuid': '1efdcee4-1cb3-11e6-93e2-0242ac110002',
                'conversation_uuid': '1efd668e-1cb3-11e6-93e2-0242ac110002',
                'conversation_icon': 'http://127.0.0.1:8080/identicon/9adb1032-1cac-11e6-bce9-0242ac110002.png',
                'createtime': '2016-05-18 04:43:52 605386',
                'app_uuid': '1ca35f40-17f1-11e6-9d01-0242ac110003',
                'conversation_name': 'Unknown Area.User',
                'user_uuid': '1ca235d4-17f1-11e6-9d01-0242ac110003',
                'conversation_status': 'OPEN'
            },
            'app_uuid': '1ca35f40-17f1-11e6-9d01-0242ac110003',
            'from_user': {
                'user_fullname': 'Unknown Area.User',
                'user_email': '9adb10@1ca35f',
                'user_icon': 'http://127.0.0.1:8080/identicon/9adb1032-1cac-11e6-bce9-0242ac110002.png',
                'uuid': '9adb1032-1cac-11e6-bce9-0242ac110002'
            },
            'user_uuid': '9adb1032-1cac-11e6-bce9-0242ac110002',
            'createtime': '2016-05-18 04:43:52 603049'
        }
    ],
    'return_count': 1,
    'error_string': 'success.',
    'max_uuid': None,
    'total_count': 1,
    'uri': '/PP_PAGE_USER_CONVERSATION',
    'page_size': 15,
    'min_uuid': None,
    'page_offset': 0,
    'error_code': 0
}
```


#### Get History Messages By Page

```
POST /PP_PAGE_HISTORY_MESSAGE
```

api_level:
```
PPCOM, PPKEFU, PPCONSOLE, THIRD_PARTY_KEFU, THIRD_PARTY_CONSOLE
```

Parameters:

Name                    | Type      | Description
------------------------|-----------|------------
**conversation_uuid**   | string    | conversation uuid
page_offset             | number    | page offset, need to provide when get by page
page_size               | number    | page size, need to provide when get by page
min_uuid                | string    | oldest message's uuid, need to provide when get by message uuid section
max_uuid                | string    | newest message's uuid, need to provide when get by message uuid section

Response (example):
```
{
    'return_count': 1,
    'error_string': 'success.',
    'total_count': 1L,
    'list': [
        {
            'message_body': '{
                "ci": "1efd668e-1cb3-11e6-93e2-0242ac110002",
                "ft": "DU",
                "tt": "AP",
                "bo": "hi",
                "ts": 1463546635.627932,
                "mt": "NOTI",
                "tl": null,
                "ms": "TEXT",
                "ti": "1efd668e-1cb3-11e6-93e2-0242ac110002",
                "fi": "9adb1032-1cac-11e6-bce9-0242ac110002",
                "id": "771d934d-9629-46df-d635-380858dd114a",
                "ct": "P2S"
            }',
            'conversation_type': 'P2S',
            'updatetime': '2016-05-18 04:43:55 662741',
            'uuid': '771d934d-9629-46df-d635-380858dd114a',
            'message_subtype': 'TEXT',
            'conversation_uuid': '1efd668e-1cb3-11e6-93e2-0242ac110002',
            'from_uuid': '9adb1032-1cac-11e6-bce9-0242ac110002',
            'body': 'hi',
            'from_type': 'DU',
            'from_device_uuid': '9ae44076-1cac-11e6-bce9-0242ac110002',
            'to_type': 'AP',
            'app_uuid': '1ca35f40-17f1-11e6-9d01-0242ac110003',
            'from_user': {
                'user_fullname': 'Unknown Area.User',
                'user_email': '9adb10@1ca35f',
                'user_icon': 'http://127.0.0.1:8080/identicon/9adb1032-1cac-11e6-bce9-0242ac110002.png',
                'uuid': '9adb1032-1cac-11e6-bce9-0242ac110002'
            },
            'to_uuid': '1efd668e-1cb3-11e6-93e2-0242ac110002',
            'task_status': 'PROCESSED',
            'message_type': 'NOTI',
            'createtime': '2016-05-18 04:43:55 627932'
        }
    ],
    'uri': '/PP_PAGE_HISTORY_MESSAGE',
    'page_size': 12,
    'page_offset': 0,
    'error_code': 0
}
```


#### Get Online PPCom Users By Page
```
POST /PP_PAGE_ONLINE_PORTAL_USER
```

api_level:
```
PPKEFU, PPCONSOLE, THIRD_PARTY_KEFU, THIRD_PARTY_CONSOLE
```

Parameters:

Name                    | Type      | Description
------------------------|-----------|------------
**app_uuid**            | string    | service team's uuid
**page_offset**         | number    | page offset
**page_size**           | number    | page size

Response (example):
```
{
    'list': [],
    'page_offset': 0,
    'page_size': 12,
    'total_count': 0,
    'return_count': 0,
    'error_code': 0,
    'error_string': 'success',
    'uri': '/PP_PAGE_ONLINE_PORTAL_USER'
}
```


#### PPKefu User Login
```
POST /PPKEFU_LOGIN
```

api_level:
```
PPKEFU
```

Parameters:

Name                    | Type      | Description
------------------------|-----------|---------------------------------------
**user_email**          | string    | user email
**terminal**            | string    | device uuid
**ostype**              | string    | device ostype
token                   | string    | iOS device token
osmodel                 | string    | device model
osversion               | string    | device os version
device_fullname         | string    | device fullname
ios_app_development     | string    | whether ios app is under development

Response (example):
```
{
    'app': {
        'return_offline_message': None,
        'app_name': 'ppmessage123',
        'app_secret': 'Mzg2ODliNjVlY2I2NzBlNTExMmJkMTE4YzM3MjRlMjUxN2U1MjEwMg==',
        'robot_user_uuid': None,
        'api_uuid': '1ca64836-17f1-11e6-9d01-0242ac110003',
        'robot_train_track': None,
        'app_billing_email': None,
        'uuid': '1ca35f40-17f1-11e6-9d01-0242ac110003',
        'welcome_message': None,
        'robot_train_click': None,
        'ppcom_powered_by_visible': None,
        'ppcom_powered_by_link': None,
        'company_name': 'YOURUI',
        'ppcom_launcher_style': None,
        'ppcom_powered_by_name': None,
        'app_icon': None,
        'offline_message': None,
        'app_key': 'NjZlZGNiMGEzOTg4NmNjYWQ2NDIxNDZiN2ZiZTljZTA1NTFiZjdlNw==',
        'show_ppcom_hover': None,
        'updatetime': datetime.datetime(2016, 5, 18, 9, 57, 22, 455405),
        'app_route_policy': None,
        'robot_train_method': None,
        'robot_train_chat': None,
        'app_billing_uuid': None,
        'user_uuid': '1ca235d4-17f1-11e6-9d01-0242ac110003',
        'createtime': datetime.datetime(2016, 5, 12, 3, 25, 1),
        'ppcom_launcher_color': None
    },
    'user_language': 'zh_cn',
    'create_status': None,
    'user_wechat': None,
    'mobile_device_uuid': None,
    'user_company': None,
    'user_status': 'ADMIN',
    'ppcom_browser_device_uuid': None,
    'mqtt_topic': '68a2feca-1c1d-11e6-a4dd-0242ac110002/#',
    'uuid': '1ca235d4-17f1-11e6-9d01-0242ac110003',
    'user_lastname': 'He',
    'user_firstname': 'Jin',
    'user_qq': None,
    'user_icon': '01a17ddc-1821-11e6-9b56-0242ac110003',
    'user_defined': None,
    'user_mobile': None,
    'user_signature': 'fight to the death ~',
    'is_email_verified': None,
    'browser_device_uuid': '68a2feca-1c1d-11e6-a4dd-0242ac110002',
    'user_name': None,
    'is_anonymous_user': False,
    'service_user_status': 'READY',
    'ppcom_trace_uuid': None,
    'user_show_badge': None,
    u'is_owner_user': True,
    'user_mute_other_mobile_device': None,
    'latest_send_message_time': datetime.datetime(2016, 5, 12, 10, 1, 18),
    u'is_service_user': True,
    'updatetime': 1463571257,
    'user_silence_notification': None,
    'is_mobile_verified': None,
    'error_string': 'success.',
    'user_fullname': 'Jin He',
    'uri': '/PPKEFU_LOGIN',
    'ppcom_mobile_device_uuid': None,
    'user_mute_notification': None,
    u'is_distributor_user': True,
    'error_code': 0,
    'createtime': datetime.datetime(2016, 5, 12, 3, 25, 1),
    'user_email': 'jin.he@ppmessage.com'
}
```


#### PPKefu User Logout
```
POST /PPKEFU_LOGOUT
```

api_level:
```
PPKEFU
```

Parameters:

Name                    | Type      | Description
------------------------|-----------|------------
**app_uuid**            | string    | service team's uuid
**user_uuid**           | string    | user uuid
**device_uuid**         | string    | device uuid

Response (example):
```
{
    'uri': '/PPKEFU_LOGOUT',
    'error_code': 0,
    'error_string': 'success.'
}
```

#### Get User Detail
```
POST /PP_GET_USER_DETAIL
```

api_level:
```
PPCOM, PPKEFU, PPCONSOLE, THIRD_PARTY_KEFU, THIRD_PARTY_CONSOLE
```

Parameters:

Name                    | Type      | Description
------------------------|-----------|------------
**user_uuid**           | string    | user uuid
return_password         | boolean   | whether to return user's password

Response (example):
```
{
    'user_firstname': 'Jin',
    'user_language': 'zh_cn',
    'create_status': None,
    'user_wechat': None,
    'mobile_device_uuid': None,
    'user_company': None,
    'user_status': 'ADMIN',
    'ppcom_browser_device_uuid': None,
    'uuid': '1ca235d4-17f1-11e6-9d01-0242ac110003',
    'user_lastname': 'He',
    'user_qq': None,
    'user_icon': '01a17ddc-1821-11e6-9b56-0242ac110003',
    'user_defined': None,
    'user_mobile': None,
    'user_signature': 'fight to the death ~',
    'is_email_verified': None,
    'browser_device_uuid': '68a2feca-1c1d-11e6-a4dd-0242ac110002',
    'pinyinname1': u'Jin He',
    'user_name': None,
    'pinyinname0': u'Jin He',
    'is_anonymous_user': False,
    'service_user_status': 'READY',
    'ppcom_trace_uuid': None,
    'user_show_badge': None,
    'user_mute_other_mobile_device': None,
    'latest_send_message_time': datetime.datetime(2016, 5, 18, 11, 17, 23),
    'updatetime': datetime.datetime(2016, 5, 18, 11, 34, 23),
    'user_silence_notification': None,
    'is_mobile_verified': None,
    'error_string': 'success.',
    'user_fullname': 'Jin He',
    'uri': '/PP_GET_USER_DETAIL',
    'ppcom_mobile_device_uuid': None,
    'user_mute_notification': None,
    'error_code': 0,
    'createtime': datetime.datetime(2016, 5, 12, 3, 25, 1),
    'user_email': 'jin.he@ppmessage.com'
}
```

#### PPConsole Logout
```
POST /PPCONSOLE_LOGOUT
```

api_level:
```
PPCONSOLE
```

Parameters:

Name                    | Type      | Description
------------------------|-----------|------------
**user_uuid**           | string    | user uuid

Response (example):
```
{
    'uri': '/PPCONSOLE_LOGOUT',
    'error_code': 0,
    'error_string': 'success.'
}
```


#### PPConsole Service Agent Sign Up

When sign up, both your service agent administrator and service team is created.

```
POST /PPCONSOLE_SIGNUP
```

api_level:
```
PPCONSOLE, THIRD_PARTY_CONSOLE, PPCONSOLE_BEFORE_LOGIN
```

Parameters:

Name                    | Type      | Description
------------------------|-----------|------------
**app_uuid**            | string    | service team's uuid
**app_name**            | string    | service team's name
**user_email**          | string    | user email
**user_fullname**       | string    | user fullname
**user_password**       | string    | user password

Response (example):
```
{
    'app': {
        'app_billing_email': 'cordova@ppmessage.com',
        'app_route_policy': 'BROADCAST',
        'uuid': '10f2cf8e-1e39-11e6-8cec-0242ac110002',
        'app_secret': '10f2ce12-1e39-11e6-8cec-0242ac110002',
        'app_key': '10f2c5fc-1e39-11e6-8cec-0242ac110002',
        'user_uuid': '10f23592-1e39-11e6-8cec-0242ac110002',
        'app_name': u'cordova'
    },
    'error_code': 0,
    'uri': '/PPCONSOLE_SIGNUP',
    'error_string': 'success.',
    'user': {
        'user_status': 'OWNER_2',
        'is_anonymous_user': False,
        'uuid': '10f23592-1e39-11e6-8cec-0242ac110002',
        'user_language': u'English',
        'user_password': u'40bd001563085fc35165329ea1ff5c5ecbdbbeef',
        'user_fullname': u'cordova',
        'user_name': u'cordova@ppmessage.com',
        'user_email': u'cordova@ppmessage.com'
    }
}
```


#### PPConsole Get Data Overview Number

```
POST /PPCONSOLE_GET_OVERVIEW_NUMBER
```

api_level:
```
PPCONSOLE
```

Parameters:

Name                    | Type      | Description
------------------------|-----------|------------
**app_uuid**            | string    | service team's uuid

Response (example):
```
{
    'error_code': 0,
    'uri': '/PPCONSOLE_GET_OVERVIEW_NUMBER',
    'error_string': 'success.',
    'number': {
        'today_customer': 2,
        'all_customer': 9,
        'all_message': '10',
        'yesterday_customer': 0,
        'agent': 3
    }
}
```


#### PPConsole Get Real Time Customer Number
```
POST /PPCONSOLE_GET_REAL_TIME_CUSTOMER_NUMBER
```

api_level:
```
PPCONSOLE
```

Parameters:

Name                    | Type      | Description
------------------------|-----------|------------
**app_uuid**            | string    | service team's uuid

Response (example):
```
{
    'error_code': 0,
    'uri': '/PPCONSOLE_GET_REAL_TIME_CUSTOMER_NUMBER',
    'error_string': 'success.',
    'number': [
        {'0': 0}, {'1': 0}, {'2': 0}, {'3': 2}, {'4': 0}, {'5': 0},
        {'6': 0}, {'7': 0}, {'8': 0}, {'9': 0}, {'10': 0}, {'11': 0},
        {'12': 0}, {'13': 0}, {'14': 0}, {'15': 0}, {'16': 0}, {'17': 0},
        {'18': 0}, {'19': 0}, {'20': 0}, {'21': 0}, {'22': 0}, {'23': 0}
    ]
}
```


#### PPConsole Get Real Time Service Agent Number

```
POST /PPCONSOLE_GET_REAL_TIME_SERVICE_NUMBER
```

api_level:
```
PPCONSOLE
```

Parameters:

Name                    | Type      | Description
------------------------|-----------|--------------------
**app_uuid**            | string    | service team's uuid

Response (example):
```
{
    'error_code': 0,
    'uri': '/PPCONSOLE_GET_REAL_TIME_SERVICE_NUMBER',
    'error_string': 'success.',
    'number': [
        {'0': 0}, {'1': 0}, {'2': 0}, {'3': 0}, {'4': 0}, {'5': 0},
        {'6': 0}, {'7': 0}, {'8': 0}, {'9': 0}, {'10': 0}, {'11': 0},
        {'12': 0}, {'13': 0}, {'14': 0}, {'15': 0}, {'16': 0}, {'17': 0},
        {'18': 0}, {'19': 0}, {'20': 0}, {'21': 0}, {'22': 0}, {'23': 0}
    ]
}
```


#### PPConsole Get Real Time Message Number

```
POST /PPCONSOLE_GET_REAL_TIME_MESSAGE_NUMBER
```

api_level:
```
PPCONSOLE
```

Parameters:

Name                    | Type      | Description
------------------------|-----------|------------
**app_uuid**            | string    | service team's uuid

Response (example):
```
{
    'error_code': 0,
    'uri': '/PPCONSOLE_GET_REAL_TIME_MESSAGE_NUMBER',
    'error_string': 'success.',
    'number': [
        {'0': None}, {'1': None}, {'2': None}, {'3': None}, {'4': None}, {'5': None},
        {'6': None}, {'7': None}, {'8': None}, {'9': None}, {'10': None}, {'11': None},
        {'12': None}, {'13': None}, {'14': None}, {'15': None}, {'16': None}, {'17': None},
        {'18': None}, {'19': None}, {'20': None}, {'21': None}, {'22': None}, {'23': None}
    ]
}
```


#### PPConsole Get Customer Number By Range

```
POST /PPCONSOLE_GET_CUSTOMER_NUMBER_BY_RANGE"
```

api_level:
```
PPCONSOLE
```

Parameters:

Name                    | Type      | Description
------------------------|-----------|------------
**app_uuid**            | string    | service team's uuid

Response (example):
```
{
    'error_code': 0,
    'uri': '/PPCONSOLE_GET_CUSTOMER_NUMBER_BY_RANGE',
    'error_string': 'success.',
    'number': {
        '2016-05-19': 0, '2016-05-18': 0, '2016-05-17': 0, '2016-05-16': 0, '2016-05-15': 0, '2016-05-14': 0,
        '2016-05-13': 0, '2016-05-12': 0, '2016-05-11': 0, '2016-05-10': 0, '2016-04-29': 0, '2016-04-28': 0,
        '2016-04-21': 0, '2016-04-20': 0, '2016-04-23': 0, '2016-04-22': 0, '2016-04-25': 0, '2016-04-24': 0,
        '2016-04-27': 0, '2016-04-26': 0, '2016-05-08': 0, '2016-05-09': 0, '2016-05-01': 0, '2016-05-02': 0,
        '2016-05-03': 0, '2016-05-04': 0, '2016-05-05': 0, '2016-05-06': 0, '2016-05-07': 0, '2016-05-20': 2,
        '2016-04-30': 0
    }
}
```


#### PPConsole Get Service Agent Number By Range
```
POST /PPCONSOLE_GET_SERVICE_NUMBER_BY_RANGE"
```

api_level:
```
PPCONSOLE
```

Parameters:

Name                    | Type      | Description
------------------------|-----------|------------
**app_uuid**            | string    | service team' suuid

Response (example):
```
{
    'error_code': 0,
    'uri': '/PPCONSOLE_GET_SERVICE_NUMBER_BY_RANGE',
    'error_string': 'success.',
    'number': {
        '2016-05-19': 0, '2016-05-18': 0, '2016-05-17': 0, '2016-05-16': 0, '2016-05-15': 0, '2016-05-14': 0,
        '2016-05-13': 0, '2016-05-12': 0, '2016-05-11': 0, '2016-05-10': 0, '2016-04-29': 0, '2016-04-28': 0,
        '2016-04-21': 0, '2016-04-20': 0, '2016-04-23': 0, '2016-04-22': 0, '2016-04-25': 0, '2016-04-24': 0,
        '2016-04-27': 0, '2016-04-26': 0, '2016-05-08': 0, '2016-05-09': 0, '2016-05-01': 0, '2016-05-02': 0,
        '2016-05-03': 0, '2016-05-04': 0, '2016-05-05': 0, '2016-05-06': 0, '2016-05-07': 0, '2016-05-20': 2,
        '2016-04-30': 0
    }
}
```


#### PPConsole Get Message Number By Range
```
POST /PPCONSOLE_GET_MESSAGE_NUMBER_BY_RANGE"
```

api_level:
```
PPCONSOLE
```

Parameters:

Name                    | Type      | Description
------------------------|-----------|--------------------
**app_uuid**            | string    | service team's uuid

Response (example):
```
{
    'error_code': 0,
    'uri': '/PPCONSOLE_GET_MESSAGE_NUMBER_BY_RANGE',
    'error_string': 'success.',
    'number': {
        '2016-05-19': 0, '2016-05-18': 0, '2016-05-17': 0, '2016-05-16': 0, '2016-05-15': 0, '2016-05-14': 0,
        '2016-05-13': 0, '2016-05-12': 0, '2016-05-11': 0, '2016-05-10': 0, '2016-04-29': 0, '2016-04-28': 0,
        '2016-04-21': 0, '2016-04-20': 0, '2016-04-23': 0, '2016-04-22': 0, '2016-04-25': 0, '2016-04-24': 0,
        '2016-04-27': 0, '2016-04-26': 0, '2016-05-08': 0, '2016-05-09': 0, '2016-05-01': 0, '2016-05-02': 0,
        '2016-05-03': 0, '2016-05-04': 0, '2016-05-05': 0, '2016-05-06': 0, '2016-05-07': 0, '2016-05-20': 2,
        '2016-04-30': 0
    }
}
```


#### Get Third Party App Info About A Service Team

```
POST /PP_GET_API_INFO
```

api_level:
```
PPCONSOLE, THIRD_PARTY_CONSOLE
```

Parameters:

Name                    | Type      | Description
------------------------|-----------|------------
**app_uuid**            | string    | service team's uuid
**user_uuid**           | string    | user uuid

Response (example):
```
{
    'ppconsole_thirdparty': {
        'api_secret': u'NTg1YzUzMGE0MDk2ODA2MzUxOGNjMmE1YzczNGViYzg5ZjNhNmIwZg==',
        'api_key': u'ZjU4YzUzYmIzOTI0YWEwMjQ5YmE2ZGEyNzM1MWFiMWQ0OTRjOWViZQ==',
        'api_level': u'THIRD_PARTY_CONSOLE',
        'api_uuid': u'1ca75fc8-17f1-11e6-9d01-0242ac110003'
    },
    'error_code': 0,
    'uri': '/PP_GET_API_INFO',
    'error_string': 'success.',
    'ppkefu_thirdparty': {
        'api_secret': u'ZGVlNmY4NWI1MWJkMzc1NjlkZTJmNWRkYWMxZTZlMjlhOTNkNGY4Yw==',
        'api_key': u'Yzk4ZGNhNjFmYjJiNTgwM2RjNTg1YmQ4MWJkZDUxOGM0YmVmODhjNA==',
        'api_level': u'THIRD_PARTY_KEFU',
        'api_uuid': u'1ca6e7aa-17f1-11e6-9d01-0242ac110003'
    }
}
```


#### Get All service team list

```
POST /PP_GET_ALL_APP_LIST
```

api_level:
```
PPCONSOLE, THIRD_PARTY_CONSOLE
```

Parameters:

Name                    | Type      | Description
------------------------|-----------|------------
**user_uuid**           | string    | user uuid

Response (example):
```
{
    'app': [
        {
            'updatetime': '2016-05-18 09:57:22 000000',
            'uuid': '1ca35f40-17f1-11e6-9d01-0242ac110003',
            'app_secret': 'Mzg2ODliNjVlY2I2NzBlNTExMmJkMTE4YzM3MjRlMjUxN2U1MjEwMg==',
            'app_key': 'NjZlZGNiMGEzOTg4NmNjYWQ2NDIxNDZiN2ZiZTljZTA1NTFiZjdlNw==',
            'company_name': 'YOURUI',
            'api_uuid': '1ca64836-17f1-11e6-9d01-0242ac110003',
            'user_uuid': '1ca235d4-17f1-11e6-9d01-0242ac110003',
            'createtime': '2016-05-12 03:25:01 000000',
            'app_name': 'ppmessage123'
        },
        {
            'app_billing_email': 'nodejs@ppmessage.com',
            'updatetime': '2016-05-18 10:23:09 000000',
            'app_route_policy': 'BROADCAST',
            'uuid': '82baa504-1ce2-11e6-b4ca-0242ac110002',
            'app_secret': '82baa464-1ce2-11e6-b4ca-0242ac110002',
            'app_key': '82baa324-1ce2-11e6-b4ca-0242ac110002',
            'user_uuid': '82b514ea-1ce2-11e6-b4ca-0242ac110002',
            'createtime': '2016-05-18 10:23:09 000000',
            'app_name': 'nodejs'
        },
        {
            'app_billing_email': 'cordova@ppmessage.com',
            'updatetime': '2016-05-20 03:15:12 770747',
            'app_route_policy': 'BROADCAST',
            'uuid': '10f2cf8e-1e39-11e6-8cec-0242ac110002',
            'app_secret': '10f2ce12-1e39-11e6-8cec-0242ac110002',
            'app_key': '10f2c5fc-1e39-11e6-8cec-0242ac110002',
            'user_uuid': '10f23592-1e39-11e6-8cec-0242ac110002',
            'createtime': '2016-05-20 03:15:12 770747',
            'app_name': 'cordova'
        },
        {
            'app_billing_email': 'dancer@ppmessage.com',
            'updatetime': '2016-05-17 09:16:34 000000',
            'app_route_policy': 'BROADCAST',
            'uuid': '0b4693e8-1c10-11e6-b5ef-0242ac110002',
            'app_secret': '0b46933e-1c10-11e6-b5ef-0242ac110002',
            'app_key': '0b469212-1c10-11e6-b5ef-0242ac110002',
            'user_uuid': '0b4629f8-1c10-11e6-b5ef-0242ac110002',
            'createtime': '2016-05-17 09:16:34 000000',
            'app_name': 'dancer-team'
        }
    ],
    'error_code': 0,
    'uri': '/PP_GET_ALL_APP_LIST',
    'error_string': 'success.'
}
```


#### Validate Online Device

```
POST /PP_VALIDATE_ONLINE_DEVICE
```

api_level:
```
PPKEFU, THIRD_PARTY_KEFU
```

Parameters:

Name                    | Type      | Description
------------------------|-----------|-------------------------
**user_uuid**           | string    | user uuid
**device_uuid**         | string    | device uuid

Response (example):
```
{
    'valid': False,
    'error_code': 0,
    'error_string': 'success.',
    'uri': '/PP_VALIDATE_ONLINE_DEVICE'
}
```


#### Set Service Agent Status
```
POST /PPKEFU_SET_SERVICE_USER_STATUS
```

api_level:
```
PPKEFU, THIRD_PARTY_KEFU
```

Parameters:

Name                    | Type      | Description
------------------------|-----------|-------------------------
**app_uuid**            | string    | service team's uuid
**user_uuid**           | string    | user uuid
**user_status**         | string    | user status, can be 'BUSY', 'READY', 'REST'

Response (example):
```
{
    'error_code': 0,
    'error_string': 'success.',
    'uri': '/PP_SET_SERVICE_USER_STATUS',
}
```


#### Get All Predefined Script

```
POST /PP_GET_ALL_PREDEFINED_SCRIPT
```

api_level:
```
PPKEFU, PPCONSOLE, THIRD_PARTY_KEFU, THIRD_PARTY_CONSOLE
```

Parameters:

Name                    | Type      | Description
------------------------|-----------|------------
**app_uuid**            | string    | service team's uuid

Response (example):
```
{
    'error_code': 0,
    'uri': '/PP_GET_ALL_PREDEFINED_SCRIPT',
    'error_string': 'success.',
    'list': [
        '0b469212-1c10-11e6-b5ef-0242ac110002',
        '0b4629f8-1c10-11e6-b5ef-0242ac110002'
    ]
}
```


#### Get All Predefined Script Group

```
POST /PP_GET_ALL_PREDEFINED_SCRIPT_GROUP
```

api_level:
```
PPKEFU, PPCONSOLE, THIRD_PARTY_KEFU, THIRD_PARTY_CONSOLE
```

Parameters:

Name                    | Type      | Description
------------------------|-----------|------------
**app_uuid**            | string    | service team's uuid

Response (example):
```
{
    'error_code': 0,
    'uri': '/PP_GET_ALL_PREDEFINED_SCRIPT_GROUP',
    'error_string': 'success.',
    'list': [
        {
            'uuid': '10f2c5fc-1e39-11e6-8cec-0242ac110002',
            'app_uuid': '10f2cf8e-1e39-11e6-8cec-0242ac110002',
            'group_name': 'install instruction',
            'createtime': '2016-05-17 09:16:34 000000',
            'updatetime': '2016-05-17 09:16:34 000000'
        }
    ]
}
```


#### Get Predefined Script In A Group

```
POST /PP_GET_PREDEFINED_SCRIPT_WITH_GROUP
```

api_level:
```
PPKEFU, PPCONSOLE, THIRD_PARTY_KEFU, THIRD_PARTY_CONSOLE
```

Parameters:

Name                    | Type      | Description
------------------------|-----------|------------
**app_uuid**            | string    | service team's uuid
**group_uuid**          | string    | group uuid

Response (example):
```
{
    'error_code': 0,
    'uri': '/PP_GET_PREDEFINED_SCRIPT_WITH_GROUP',
    'error_string': 'success.',
    'list': [
        {
            'uuid': '1ca64836-17f1-11e6-9d01-0242ac110003',
            'app_uuid': '1ca235d4-17f1-11e6-9d01-0242ac110003',
            'group_uuid': '82baa464-1ce2-11e6-b4ca-0242ac110002',
            'script_question': 'is PPMessage an open source project ?',
            'script_answer': 'Yes, it is.'
        }
    ]
}
```


#### Add Predefined Script

```
POST /PP_ADD_PREDEFINED_SCRIPT
```

api_level:
```
PPKEFU, PPCONSOLE, THIRD_PARTY_KEFU, THIRD_PARTY_CONSOLE
```

Parameters:

Name                    | Type      | Description
------------------------|-----------|------------
**app_uuid**            | string    | service team's uuid
**script_question**     | string    | script question
**script_answer**       | string    | script answer
group_uuid              | string    | group uuid

Response (example):
```
{
    'error_code': 0,
    'uri': '/PP_ADD_PREDEFINED_SCRIPT',
    'error_string': 'success.',
    'uuid': '1ca64836-17f1-11e6-9d01-0242ac110003',
    'app_uuid': '1ca235d4-17f1-11e6-9d01-0242ac110003',
    'group_uuid': '82baa464-1ce2-11e6-b4ca-0242ac110002',
    'script_question': 'is PPMessage an open source project ?',
    'script_answer': 'Yes, it is.'
}
```


#### Remove Predefined Script

```
POST /PP_REMOVE_PREDEFINED_SCRIPT
```

api_level:
```
PPKEFU, PPCONSOLE, THIRD_PARTY_KEFU, THIRD_PARTY_CONSOLE
```

Parameters:

Name                    | Type      | Description
------------------------|-----------|------------
**app_uuid**            | string    | service team's uuid
**script_uuid**         | string    | script uuid

Response (example):
```
{
    'error_code': 0,
    'uri': '/PP_REMOVE_PREDEFINED_SCRIPT',
    'error_string': 'success.',
}
```


#### Add Predefined Script Group

```
POST /PP_ADD_PREDEFINED_SCRIPT_GROUP
```

api_level:
```
PPCONSOLE, THIRD_PARTY_CONSOLE
```

Parameters:

Name                    | Type      | Description
------------------------|-----------|-------------------
**app_uuid**            | string    | service team's uuid
**group_name**          | string    | group name


Response (example):
```
{
    'error_code': 0,
    'uri': '/PP_ADD_PREDEFINED_SCRIPT_GROUP',
    'error_string': 'success.',
    'uuid': '10f2c5fc-1e39-11e6-8cec-0242ac110002',
    'app_uuid': '10f2cf8e-1e39-11e6-8cec-0242ac110002',
    'group_name': 'install instruction',
    'createtime': '2016-05-17 09:16:34 000000',
    'updatetime': '2016-05-17 09:16:34 000000'
}
```


#### Remove Predefined Script Group

```
POST /PP_REMOVE_PREDEFINED_SCRIPT_GROUP
```

api_level:
```
PPCONSOLE, THIRD_PARTY_CONSOLE
```

Parameters:

Name                    | Type      | Description
------------------------|-----------|------------
**app_uuid**            | string    | service team's uuid
**group_uuid**          | string    | group uuid


Response (example):
```
{
    'error_code': 0,
    'uri': '/PP_REMOVE_PREDEFINED_SCRIPT_GROUP',
    'error_string': 'success.',
}
```


#### Move Predefined Script Into Group

```
POST /PP_MOVE_PREDEFINED_SCRIPT_INTO_GROUP
```

api_level:
```
PPCONSOLE, THIRD_PARTY_CONSOLE
```

Parameters:

Name                    | Type      | Description
------------------------|-----------|-------------------------
**app_uuid**            | string    | service team's uuid
**group_uuid**          | string    | group uuid
**script_uuid**         | string    | script uuid


Response (example):
```
{
    'error_code': 0,
    'uri': '/PP_MOVE_PREDEFINED_SCRIPT_INTO_GROUP',
    'error_string': 'success.',
}
```


#### PPConsole Send User Email When His Password Is Changed

```
POST /PPCONSOLE_SEND_NEW_PASSWORD
```

api_level:
```
PPCONSOLE_BEFORE_LOGIN
```

Parameters:

Name                    | Type      | Description
------------------------|-----------|------------
**user_email**          | string    | user uuid


Response (example):
```
{
    'error_code': 0,
    'uri': '/PPCONSOLE_SEND_NEW_PASSWORD',
    'error_string': 'success.',
}
```


#### Cancel Waiting Create Conversation

```
POST /PP_CANCEL_WAITING_CREATE_CONVERSATION
```

api_level:
```
PPCOM
```

Parameters:

Name                    | Type      | Description
------------------------|-----------|------------
**app_uuid**            | string    | service team's uuid
**user_uuid**           | string    | user uuid
**device_uuid**         | string    | device uuid
group_uuid              | string    | service group uuid

Response (example):
```
{
    'error_code': 0,
    'uri': '/PP_CANCEL_WAITING_CREATE_CONVERSATION',
    'error_string': 'success.',
}
```


#### PPCom Create Conversation

```
POST /PPCOM_CREATE_CONVERSATION
```

api_level:
```
PPCOM
```

Parameters:

Name                    | Type      | Description
------------------------|-----------|---------------------------------
**app_uuid**            | string    | service team's uuid
**user_uuid**           | string    | user uuid
**device_uuid**         | string    | device uuid
group_uuid              | string    | service group uuid
member_list             | list      | member list in the conversation


Response (example):
```
{
    'status': 'NEW',
    'conversation_type': 'P2S',
    'uuid': 'a3e0da04-1e69-11e6-bcf2-0242ac110002',
    'error_string': 'success.',
    'latest_task': None,
    'user_uuid': '9adb1032-1cac-11e6-bce9-0242ac110002',
    'uri': '/PPCOM_CREATE_CONVERSATION',
    'group_uuid': None,
    'conversation_icon': None,
    'app_uuid': '1ca35f40-17f1-11e6-9d01-0242ac110003',
    'conversation_name': 'right@ppmessage.com',
    'assigned_uuid': '89d63aee-1c1d-11e6-a4dd-0242ac110002',
    'error_code': 0,
    'updatetime': datetime.datetime(2016, 5, 20, 9, 2, 55, 134858),
    'createtime': datetime.datetime(2016, 5, 20, 9, 2, 55, 134858)
}
```


#### PPCom Get waiting Queue Length

```
POST /PP_GET_AMD_QUEUE_LENGTH
```

api_level:
```
PPCOM
```

Parameters:

Name                    | Type      | Description
------------------------|-----------|------------
**app_uuid**            | string    | service team's uuid


Response (example):
```
{
    'length': 10,
    'uri': '/PPCOM_CREATE_CONVERSATION',
    'error_code': 0,
    'error_string': 'success.'
}
```
