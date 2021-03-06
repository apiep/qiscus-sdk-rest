# REST API

> BASE_URL : [APP_ID].qiscus.com
> example : if your APP_ID is `domino-prod` means the base_url will be `domino-prod.qiscus.com`

## Postman Collections

You can see Postman collections of Qiscus REST APIs here :

[Qiscus REST API Postman's Collections](https://documenter.getpostman.com/view/484596/qiscus-sdk-postman-collection/6tXb66L#07399c07-4283-3140-ec89-55aea88fe7ac)

## Authentication

Add `SECRET KEY` on every header's request as 'QISCUS_SDK_SECRET', you can get the value from www.qiscus.com/dashboard

so for example if your `SECRET KEY` value is `8355105e6171795fca176366e0c16f22`, your header request will be :

```bash
headers :

QISCUS_SDK_SECRET: 8355105e6171795fca176366e0c16f22

```

## Login or Register

You can use this endpoint to create new user if it does not exist yet, or you can use this endpoint to update data of the user if they already exists

verb :
`POST /api/v2/rest/login_or_register`

request :

```bash
email [string]
password [string password, optional] # password will be updated if user already exist
username [string]
avatar_url [string url, optional]
device_token [string, optional]
device_platform ["ios" or "android", optional]
```


Note : `password` is optional, it will generate random string on the backend if you dont pass it during `User` creation through this API. However, please note for those users already created you can not use this API `login_or_register` without passing password value

response :
```json
{
    "status": 200,
    "results": {
        "user": {
            "id": 1,
            "email": "email@qiscus.com",
            "username": "Johnny Cage",
            "avatar_url": "https://myimagebucket.com/image.jpg",
            "token": "abcde1234defgh"
        },
    }
}
```

## Get User Profile

You can use this endpoint to check user profile

verb :

`GET /api/v2/rest/user_profile?user_email={{user_id}}`

request :

```bash
user_email [string]
```

response :
```json
{
    "status": 200,
    "results": {
        "user": {
            "id": 1,
            "email": "email@qiscus.com",
            "username": "Johnny Cage",
            "avatar_url": "https://myimagebucket.com/image.jpg",
            "token": "abcde1234defgh"
        },
    }
}
```


## Reset User Authentication Token

In case your user token is compromised, you can reset their token at any time. This make previous token no longer valid.

verb:

`POST /api/v2/rest/reset_user_token`

request:
```bash
user_email [string] user email to reset
```

response:
```json
{
    "results": {
        "user": {
            "avatar": {
                "url": "https://res.cloudinary.com/qiscus/image/upload/v1492579000/kiwari-prod_user_id_108/m9lvv1ykfrgw3lte0ojb.jpg"
            },
            "avatar_url": "https://res.cloudinary.com/qiscus/image/upload/v1492579000/kiwari-prod_user_id_108/m9lvv1ykfrgw3lte0ojb.jpg",
            "email": "userid_108_6285868231412@kiwari-prod.com",
            "id": 144,
            "last_comment_id": 443376,
            "pn_android_configured": true,
            "pn_ios_configured": true,
            "rtKey": "somestring",
            "token": "kj2oLfL9CwzKZXxkHfHE",
            "username": "Yusuf"
        }
    },
    "status": 200
}
```

## Get User Room List

Will show maximum 20 data per page. If page parameter empty, this API will return all conversations (max 100)

Verb:
`GET /api/v2/rest/get_user_rooms`

request:
```bash
user_email [string] required
page [int, optional] number of page
show_participants [bool, optional] "true" or "false" default will be false
room_type [string, optional] filter by room type ("single" or "group") default will be return all type
```


response when **show_participants** is false:
```json
{
    "results": {
        "meta": {
            "current_page": 1,
            "total_room": 39
        },
        "rooms_info": [
            {
                "last_comment_id": 443375,
                "last_comment_message": "Yusuf added Heru S",
                "last_comment_timestamp": "2017-08-04T15:45:07Z",
                "room_avatar_url": "",
                "room_id": 1339,
                "room_name": "Heru S",
                "room_type": "single",
                "unread_count": 19
            },
            {
                "last_comment_id": 430237,
                "last_comment_message": "Haha",
                "last_comment_timestamp": "2017-07-14T09:19:40Z",
                "room_avatar_url": "https://res.cloudinary.com/qiscus/image/upload/v1493780549/group_avatar_kiwari-prod_user_id_74/chbflw5rqfdlj0orsfzj.jpg",
                "room_id": 1325,
                "room_name": "qiscus AI",
                "room_type": "group",
                "unread_count": 56
            }
        ]
    },
    "status": 200
}
```

response when **show_participants** is true:
```json
{
    "results": {
        "meta": {
            "current_page": 1,
            "total_room": 39
        },
        "rooms_info": [
            {
                "last_comment_id": 443376,
                "last_comment_message": "halo",
                "last_comment_timestamp": "2017-08-07T11:10:59Z",
                "participants": [
                    {
                        "avatar_url": "https://res.cloudinary.com/qiscus/image/upload/v1492579000/kiwari-prod_user_id_108/m9lvv1ykfrgw3lte0ojb.jpg",
                        "email": "userid_108_6285868231412@kiwari-prod.com",
                        "id": 144,
                        "last_comment_read_id": 443376,
                        "last_comment_received_id": 426622,
                        "username": "Yusuf"
                    },
                    {
                        "avatar_url": "https://res.cloudinary.com/qiscus/image/upload/v1486119595/kiwari-prod_user_id_72/tcqbyg6adc6e9mymb9nr.jpg",
                        "email": "userid_72_6281226612018@kiwari.com",
                        "id": 101,
                        "last_comment_read_id": 428889,
                        "last_comment_received_id": 426622,
                        "username": "Delta"
                    },
                    {
                        "avatar_url": "https://res.cloudinary.com/qiscus/image/upload/v1490343786/kiwari-prod_user_id_201/sa6r61reovri6dtrajly.jpg",
                        "email": "userid_201_6285877700050@kiwari-prod.com",
                        "id": 326,
                        "last_comment_read_id": 425609,
                        "last_comment_received_id": 411931,
                        "username": "A. Athaullah"
                    }
                ],
                "room_avatar_url": "https://res.cloudinary.com/qiscus/image/upload/v1493173118/group_avatar_kiwari-prod_user_id_93/c7tankz1i4yi6620btby.jpg",
                "room_id": 1275,
                "room_name": "Qiscus SDK clients",
                "room_type": "group",
                "unread_count": 0
            }
        ]
    },
    "status": 200
}
```


## Create room

verb:
`POST /api/v2/rest/create_room`

request:
```bash
name [string]
participants[] [array of string email]
creator [string email]
avatar_url [string] optional
```
response:
```json
{
  "results": {
    "creator": "abc@outlook.com",
    "participants": [
      "abc@outlook.com",
      "kotak@outlook.com"
    ],
    "room_id": 16,
    "room_name": "gege",
    "room_type": "group"
  },
  "status": 200
}
```

## Update Room

verb:
`POST /api/v2/rest/update_room`

request:
```bash
user_email [string required] must one of user participant
room_id [string required] must be group room
room_name [string optional]
room_avatar_url [string optional]
options [string optional]
```

response:
```json
{
  "results": {
    "changed": true,
    "room": {
      "chat_type": "group", // always group
      "id": 18,
      "last_comment_id": 0,
      "last_comment_message": "",
      "last_topic_id": 0,
      "avatar_url": "http://avatar.jpg",
      "options": "",
      "participants": [
        {
          "avatar_url": "https://qiscuss3.s3.amazonaws.com/uploads/55c0c6ee486be6b686d52e5b9bbedbbf/2.png",
          "email": "asasmoyo@outlook.com",
          "username": "asasmoyo",
          "last_comment_read_id": 0,
          "last_comment_received_id": 0
        },
        {
          "avatar_url": "https://qiscuss3.s3.amazonaws.com/uploads/55c0c6ee486be6b686d52e5b9bbedbbf/2.png",
          "email": "kotak@outlook.com",
          "username": "kotak",
          "last_comment_read_id": 0,
          "last_comment_received_id": 0
        }
      ],
      "room_name": "uwooo"
    },
    "comments": [
        {
        "id": 985,
        "comment_before_id": 984,
        "message": "Hello Post 2",
        "type": "text"
        "payload": {},
        "disable_link_preview": false,
        "email": "f1@gmail.com",
        "username": "f1",
        "user_avatar": {
            "avatar": {
                "url": "http://imagebucket.com/image.jpg"
            }
        },
        "user_avatar_url": "http://imagebucket.com/image.jpg",
        "timestamp": "2016-09-06T16:18:50+00:00",
        "unix_timestamp": 1489999170,
        "unique_temp_id": "CanBeAnything1234321"
      },
      {
        "id": 985,
        "comment_before_id": 984,
        "message": "Hello Post 2",
        "type": "text"
        "payload": {},
        "disable_link_preview": false,
        "username": "f1",
        "email": "f1@gmail.com",
        "user_avatar": {
            "avatar": {
                "url": "http://imagebucket.com/image.jpg"
            }
        },
        "user_avatar_url": "http://imagebucket.com/image.jpg",
        "timestamp": "2016-09-06T16:18:50+00:00",
        "unix_timestamp": 1489999170,
        "unique_temp_id": "CanBeAnything1234321"
      }
    ]
  },
  "status": 200
}
```

## Get or create room with target

verb:
`GET /api/v2/rest/get_or_create_room_with_target`

request:
```bash
emails[] [array of string] # must contains 2 emails
```
response:
```json
{
  "results": {
    "comments": [
      {
        "comment_before_id": 124973,
        "disable_link_preview": false,
        "email": "abc@outlook.com",
        "id": 124974,
        "message": "testingasdad asdas dasd",
        "timestamp": "2017-02-07T19:01:00Z",
        "unique_temp_id": "pyRIKY4reRXlU4Sp6r97",
        "user_avatar_url": "https://res.cloudinary.com/drbmkdgd2/image/fetch/http://res.cloudinary.com/qiscus/image/upload/v1486117460/kiwari-prod_user_id_95/vqgq5pwx1y3mafxsezmb.jpg",
        "username": "abc"
      },
      {
        "comment_before_id": 124972,
        "disable_link_preview": false,
        "email": "abc@outlook.com",
        "id": 124973,
        "message": "testingasdad asdas dasd",
        "timestamp": "2017-02-07T19:00:58Z",
        "unique_temp_id": "K5E6HmKQJQwSovEkFhHf",
        "user_avatar_url": "https://res.cloudinary.com/drbmkdgd2/image/fetch/http://res.cloudinary.com/qiscus/image/upload/v1486117460/kiwari-prod_user_id_95/vqgq5pwx1y3mafxsezmb.jpg",
        "username": "abc"
      }
    ],
    "room": {
      "avatar_url": "",
      "chat_type": "single",
      "id": 234,
      "last_comment_id": 124974,
      "last_comment_message": "testingasdad asdas dasd",
      "last_topic_id": 234,
      "options": null,
      "participants": [
        {
          "avatar_url": "https://res.cloudinary.com/drbmkdgd2/image/fetch/http://res.cloudinary.com/qiscus/image/upload/v1486117460/kiwari-prod_user_id_95/vqgq5pwx1y3mafxsezmb.jpg",
          "email": "abc@outlook.com",
          "username": "abc"
        },
        {
          "avatar_url": "https://qiscuss3.s3.amazonaws.com/uploads/55c0c6ee486be6b686d52e5b9bbedbbf/2.png",
          "email": "kotak@outlook.com",
          "username": "kotak"
        }
      ],
      "room_name": "abc@outlook.com kotak@outlook.com"
    }
  },
  "status": 200
}
```

## Get rooms info

verb:
`POST /api/v2/rest/get_rooms_info`

request:
```bash
room_id[] [array of string]
user_email [string email]
show_participants [boolean true or false, default is false]
```
response:
```json
{
  "results": {
    "rooms_info": [
      {
        "last_comment_id": 0,
        "last_comment_message": "",
        "last_comment_timestamp": "0001-01-01T00:00:00Z",
        "room_id": 13,
        "room_name": "abc@outlook.com kotak1@outlook.com",
        "room_type": "single",
        "unread_count": 123
      },
      {
        "last_comment_id": 0,
        "last_comment_message": "",
        "last_comment_timestamp": "0001-01-01T00:00:00Z",
        "room_id": 14,
        "room_name": "abc@outlook.com kotak2@outlook.com",
        "room_type": "single",
        "unread_count": 123
      }
    ]
  },
  "status": 200
}
```

## Add room participants

verb:
`post /api/v2/rest/add_room_participants`

request:
```bash
room_id [string]
emails[] [array of string emails]
```
response:
```json
{
  "results": {
    "creator": "abc@outlook.com",
    # updated participants
    "participants": [
      "abc@outlook.com",
      "kotak@outlook.com"
    ],
    "room_id": 16,
    "room_name": "gege",
    "room_type": "group"
  },
  "status": 200
}
```

## Remove room participants

verb:
`post /api/v2/rest/remove_room_participants`

request:
```bash
room_id [string]
emails [array of string emails]
```
response:
```json
{
  "results": {
    "creator": "abc@outlook.com",
    # updated participants
    "participants": [
      "abc@outlook.com",
      "kotak@outlook.com"
    ],
    "room_id": 16,
    "room_name": "gege",
    "room_type": "group"
  },
  "status": 200
}
```

## Post comment

verb:
`post /api/v2/rest/post_comment`

request:
```bash
sender_email [string]
room_id [string], it can be room_id or channel id specified by client or auto generated by server
message [string]
type [string, default=text]
payload [string json, see payload definitions bellow]
unique_temp_id [string, optional, default=generated by backend]
disable_link_preview [bool, optional, default=false]
```
response, is same as response in `/sdk` post comment:
```json
{
  "results": {
    "comment": {
      "comment_before_id": 2,
      "disable_link_preview": false,
      "email": "asasmoyo@outlook.com",
      "id": 3,
      "message": "Account linking",
      "payload": {
        "url": "http://google.com",
        "redirect_url": "http://google.com/redirect",
        "text": "silahkan login",
        "params": {
          "user_id": 1,
          "topic_id": 1
        }
      },
      "room_id": 1,
      "timestamp": "2017-02-27T17:30:09+07:00",
      "unix_timestamp": 1489999170,
      "topic_id": 1,
      "type": "account_linking",
      "unique_temp_id": "8I4NUxHkMCut7c1ijJLt",
      "user_avatar": {
        "avatar": {
          "url": "https://qiscuss3.s3.amazonaws.com/uploads/55c0c6ee486be6b686d52e5b9bbedbbf/2.png"
        }
      },
      "user_avatar_url": "https://qiscuss3.s3.amazonaws.com/uploads/55c0c6ee486be6b686d52e5b9bbedbbf/2.png",
      "username": "asasmoyo"
    }
  },
  "status": 200
}
```

There are several type of comment (message) that you can post to a room. Each comment has different payload format:
** type account_linking **
example payload structure:
```json
{
    "text": "silahkan login",
    "url": "http://google.com",
    "redirect_url": "http://google.com/redirect",
    "params": {
        "user_id": 1,
        "topic_id": 1,
        "button_text": "ini button",
        "view_title": "title",
        "success_message": "sip!"
    }
}
```
** type buttons **
example payload structure:
```json
{
    "text": "silahkan pencet",
    "buttons": [
        {
            "label": "button1",
            "type": "postback",
            "payload": {
                "url": "http://somewhere.com/button1",
                "method": "get",
                "payload": null
            }
        },
        {
            "label": "button2",
            "type": "link",
            "payload": {
                "url": "http://somewhere.com/button2?id=123"
            }
        }
    ]
}
```
** type system_event **

you cannot post comment using this end-point, nor SDK client post comment
end-point. To post comment with type **system_event** only can be
done using `POST /api/v2/rest/post_system_event_message` endpoint.

For each sub-type of system_event, there are different payload
structure. This is example of payload response:

**sub type: create_room**

example response payload:
```json
...
message: "Ucup created room 'Qiscus'",
payload: {
    "type": "create_room",
    "subject_username": "Ucup",
    "subject_email": "ucup@qiscus.com",
    "room_name": "Qiscus"
},
...
```

**sub type add_member**
example response payload:
```json
...
message: "Ucup added Ani",
payload: {
    "type": "add_member",
    "subject_username": "Ucup",
    "subject_email": "ucup@qiscus.com",
    "object_username": "Ani",
    "object_email": "ani@qiscus.com",
}
...
```

**sub type join_room**
example response payload:
```json
...
message: "Ucup joined room",
payload: {
    "type": "join_room",
    "subject_username": "Ucup",
    "subject_email": "ucup@qiscus.com",
    "room_name": "Qiscus"
}
...
```

**sub type remove_member**
example response payload:
```json
...
message: "Ucup removed Ani",
payload: {
    "type": "remove_member",
    "subject_username": "Ucup",
    "subject_email": "ucup@qiscus.com",
    "object_username": "Ani",
    "object_email": "ani@qiscus.com",
}
...
```
**sub type left_room**
example response payload:
```json
...
message: "Ucup left room",
payload: {
    "type": "left_room",
    "subject_username": "Ucup",
    "subject_email": "ucup@qiscus.com",
    "room_name": "Qiscus"
}
...
```

**sub type change_room_name**
example response payload:
```json
...
message: "Ucup changed room name to 'Qiscus Super Family'",
payload: {
    "type": "change_room_name",
    "subject_username": "Ucup",
    "subject_email": "ucup@qiscus.com",
    "room_name": "Qiscus Super Family"
}
...
```

**sub type change_room_avatar**
example response payload:
```json
...
message: "Ucup changed room avatar",
payload: {
    "type": "change_room_avatar",
    "subject_username": "Ucup",
    "subject_email": "ucup@qiscus.com"
}
...
```
**sub type custom**
will post message to room with System User as a sender and payload is defined
by you as a client. Example, if you post payload as:
```json
{
    "type": "add_admin",
    "admin_email": "admin@email.com"
}
```

So, the response payload string will be the same as you have inputted:
```json
{
    "type": "add_admin",
    "admin_email": "admin@email.com"
}
```


** type card **

request payload structure:
```json
{
    "text": "Special deal buat sista nih..",
    "image_url": "http://url.com/gambar.jpg",
    "title": "Atasan Blouse Tunik Wanita Baju Muslim Worie Longtop",
    "description": "Oleh sippnshop\n96% (666 feedback)\nRp 49.000.00,-\nBUY 2 GET 1 FREE!!!",
    "url": "http://url.com/baju?id=123&track_from_chat_room=123",
    "buttons": [
        {
            "label": "button1",
            "type": "postback",
            "payload": {
                "url": "http://somewhere.com/button1",
                "method": "get",
                "payload": null
            }
        },
        {
            "label": "button2",
            "type": "link",
            "payload": {
                "url": "http://somewhere.com/button2?id=123"
            }
        }
    ]
}
```
response payload example:
```json
{
    "text": "Special deal buat sista nih..",
    "image": "http://url.com/gambar.jpg",
    "title": "Atasan Blouse Tunik Wanita Baju Muslim Worie Longtop",
    "description": "Oleh sippnshop\n96% (666 feedback)\nRp 49.000.00,-\nBUY 2 GET 1 FREE!!!",
    "url": "http://url.com/baju?id=123&track_from_chat_room=123",
    "buttons": [
        {
            "label": "button1",
            "type": "postback",
            "payload": {
                "url": "http://somewhere.com/button1",
                "method": "get",
                "payload": null
            }
        },
        {
            "label": "button2",
            "type": "link",
            "payload": {
                "url": "http://somewhere.com/button2?id=123"
            }
        }
    ]
}
```

** type custom **
Request payload must be valid json string object, and it will return as what
you have inputted. The json payload must have an type and content object.
Type must be string, for example if you want to create promo payload, it can
be “promo”. The content can be anything, such as object, array, number or
string in JSON. By this, you can input, let say XML string in
payload.content object value and later you can parse it by yourself
by overriding SDK client chat view.

example request payload:
```json
{
    "type": "promo", // sub type of custom payload
    "content": {
        "date": "2017-09-09"
    } // can be anything: object, array, string, number in JSON
}
```

The response payload will be:
```json
{
    "type": "promo",
    "content": {
        "date": "2017-09-09"
    }
}
```

** type location **
The message text will be `name + address + map_url`. Example request payload:
```json
{
   "name": "Mirota Kampus 2 Simanjuntak",
   "address": "Jalan C Simanjuntak No.70, Terban, Gondokusuman, Kota Yogyakarta, Daerah Istimewa Yogyakarta 55223",
   "latitude": 1213.2323,
   "longitude": 1223223.1212,
   "map_url": "https://goo.gl/maps/nkY2DBF1quM2"
}

```

** type contact_person **
message text will be `name - value`
```json
{
  "name": "Evan",
  "value": "e@qiscus.com",
  "type": "email" //optional, default is phone. Must be "email" or "phone" or empty string.
}
```

## Load comments

verb:
`get /api/v2/rest/load_comments`

request:
```bash
room_id [string]
page [int optional]
limit [int optional default=20]
```
response:
```json
{
  "results": {
    "comments": [
      {
        "comment_before_id": 124973,
        "disable_link_preview": false,
        "email": "abc@outlook.com",
        "id": 124974,
        "message": "testing",
        "room_id": 234,
        "room_name": "abc@outlook.com kotak@outlook.com",
        "timestamp": "2017-02-07T19:01:00Z",
        "unique_temp_id": "pyRIKY4reRXlU4Sp6r97",
        "user_avatar_url": "https://res.cloudinary.com/drbmkdgd2/image/fetch/http://res.cloudinary.com/qiscus/image/upload/v1486117460/kiwari-prod_user_id_95/vqgq5pwx1y3mafxsezmb.jpg",
        "username": "abc"
      },
      {
        "comment_before_id": 124972,
        "disable_link_preview": false,
        "email": "abc@outlook.com",
        "id": 124973,
        "message": "here is the message that I sent",
        "room_id": 234,
        "room_name": "abc@outlook.com kotak@outlook.com",
        "timestamp": "2017-02-07T19:00:58Z",
        "unique_temp_id": "K5E6HmKQJQwSovEkFhHf",
        "user_avatar_url": "https://res.cloudinary.com/drbmkdgd2/image/fetch/http://res.cloudinary.com/qiscus/image/upload/v1486117460/kiwari-prod_user_id_95/vqgq5pwx1y3mafxsezmb.jpg",
        "username": "abc"
      }
    ]
  },
  "status": 200
}
```

## Post System Event Message
To send event system message such as creating group, join room, remove member, etc
verb:
`POST /api/v2/rest/post_system_event_message`


request:
```bash
system_event_type [string] valid value is: "create_room", "add_member", "join_room", "remove_member", "left_room", "change_room_name", "change_room_avatar"
room_id [string] required, room id to post
subject_email [string] required, person who create a room, add member to room, join room, remove member from room, left from room, change room name and/or room avatar
object_email[] [array of string] optional, only required when system event type is add_member or remove_member
updated_room_name [string] optional, only required when system event message type is change_room_name or create_room
```
response:
Will return last inserted comment and object id when type is add_member or remove_member.
```json
{
    "results": {
        "comment": {
            "comment_before_id": 17974,
            "disable_link_preview": false,
            "email": "system@dragongo.qiscus.com",
            "id": 17975,
            "message": "Yusuf joined room",
            "payload": {
                "object_email": "",
                "object_username": "",
                "room_name": "Test Group",
                "subject_email": "userid_846_6285868233422@dragongo.com",
                "subject_username": "Yusuf",
                "type": "join_room"
            },
            "room_id": 2427,
            "timestamp": "2017-06-22T02:10:29Z",
            "topic_id": 2427,
            "type": "system_event",
            "unique_temp_id": "AOpM0LdZULDb8gw82ui3",
            "unix_timestamp": 1498097429,
            "user_avatar": {
                "avatar": {
                    "url": "https://qiscuss3.s3.amazonaws.com/uploads/55c0c6ee486be6b686d52e5b9bbedbbf/2.png"
                }
            },
            "user_avatar_url": "https://qiscuss3.s3.amazonaws.com/uploads/55c0c6ee486be6b686d52e5b9bbedbbf/2.png",
            "user_id": 2905,
            "username": "System"
        }
    },
    "status": 200
}
```
## Search Messages
Search results will get last 100 messages on the query keyword.
verb:
`POST /api/v2/rest/search_messages`
request:
```bash
user_email [string] required, user email
query [string] required, keyword to search
room_id [string] optional, send this param if you want search message in specific room
```

response:
```json
{
    "results": {
        "comments": [
            {
                "chat_type": "group",
                "comment_before_id": 155913,
                "disable_link_preview": false,
                "email": "userid_74_6281212962110@kiwari.com",
                "id": 156028,
                "message": "Support integration",
                "payload": null,
                "room_id": 1275,
                "room_name": "Qiscus SDK clients",
                "timestamp": "2017-04-25T05:20:48Z",
                "topic_id": 1275,
                "type": "text",
                "unique_temp_id": "bq1493097648433",
                "unix_timestamp": 1493097648,
                "user_avatar": {
                    "avatar": {
                        "url": "https://res.cloudinary.com/qiscus/image/upload/v1493460995/kiwari-prod_user_id_74/fsx7ueheeavclilc5djl.jpg"
                    }
                },
                "user_avatar_url": "https://res.cloudinary.com/qiscus/image/upload/v1493460995/kiwari-prod_user_id_74/fsx7ueheeavclilc5djl.jpg",
                "user_id": 103,
                "username": "Evan"
            }
        ]
    },
    "status": 200
}
```

# Data Backup and Import

## Create or Request Backup

description: will request a backup as json
verb:
`POST /api/v2/rest/exports`

request:
```bash
type [string] type of resource which will be exported, permitted value are: "users", "rooms", "comments"
start_date [string] using format "YYYY-MM-DD"
end_date [string] using format "YYYY-MM-DD"
```
response:
```json
{
    "results": {
        "created_at": "2017-07-17T10:19:44+07:00",
        "download_url": "",
        "error_message": "",
        "original_filename": "2017-07-17T10:19:44+07:00_exported_comments.json",
        "percentage": 0,
        "resource_name": "comments",
        "size": 0,
        "status": "started",
        "total_rows": 0,
        "unique_id": "dd2c46a8-0921-4b75-837c-cee1b9804787"
    },
    "status": 200
}
```

## Get List of Backup
verb:
`GET /api/v2/rest/exports`

request:
```bash
page [int] page number, optional
```

response:
will return maximum 20 rows of recent backup
```json
{
    "results": {
        "backup_histories": [
            {
                "created_at": "2017-07-17T10:10:57+07:00",
                "download_url": "https://res.cloudinary.com/dscpwwumu/raw/upload/2017-07-17T10:10:57+07:00_exported_comments.json",
                "error_message": "",
                "original_filename": "2017-07-17T10:10:57+07:00_exported_comments.json",
                "percentage": 100,
                "resource_name": "comments",
                "size": 43044263,
                "status": "finished",
                "total_rows": 119963,
                "unique_id": "c44c4168-0b45-4ac2-8942-a4f1af987a13"
            }
        ]
    },
    "status": 200
}
```

## Get Backup By Id
verb:
`GET /api/v2/rest/exports/:backup_unique_id`
where `:backup_unique_id` is unique id of backup
response:
```json
{
    "results": {
        "backup_history": {
            "created_at": "2017-07-17T10:10:57+07:00",
            "download_url": "https://res.cloudinary.com/dscpwwumu/raw/upload/2017-07-17T10:10:57+07:00_exported_comments.json",
            "error_message": "",
            "original_filename": "2017-07-17T10:10:57+07:00_exported_comments.json",
            "percentage": 100,
            "resource_name": "comments",
            "size": 43044263,
            "status": "finished",
            "total_rows": 119963,
            "unique_id": "c44c4168-0b45-4ac2-8942-a4f1af987a13"
        }
    },
    "status": 200
}
```


## Delete Backup By Id

verb:
`DELETE /api/v2/rest/exports/:backup_unique_id`

where `:backup_unique_id` is unique id of backup

response:
```json
{
    "results": {
        "backup_history": {
            "created_at": "2017-07-17T10:10:57+07:00",
            "download_url": "https://res.cloudinary.com/dscpwwumu/raw/upload/2017-07-17T10:10:57+07:00_exported_comments.json",
            "error_message": "",
            "original_filename": "2017-07-17T10:10:57+07:00_exported_comments.json",
            "percentage": 100,
            "resource_name": "comments",
            "size": 43044263,
            "status": "finished",
            "total_rows": 119963,
            "unique_id": "c44c4168-0b45-4ac2-8942-a4f1af987a13"
        }
    },
    "status": 200
}
```
## Make an Import
verb:
`POST /api/v2/rest/imports`

request:
```bash
type [string] type of resource which will be exported, permitted value are: "users", "rooms", "comments"
file [file] json file, limit 4 MB each import
```
response:
```json
{
    "results": {
        "backup_history": {
            "created_at": "2017-07-24T16:38:14+07:00",
            "errors": {
                "Message": "",
                "Data": null
            },
            "original_filename": "comment_single.json",
            "resource_name": "comments",
            "size": 926,
            "status": "started",
            "total_rows": 0,
            "unique_id": "13c4952f-4b77-4705-9523-7ddca9c45967"
        }
    },
    "status": 200
}
```

> Note: for each type, it must follows required format as specified below:

** Users **
Email and authentication token must be unique, and you must have no same
data (both email or unique id)in your database right now (you can check it
by export it first).. Password in this json is plain password and system
will encrypted it when save to db. We encourage you to use https version
of avatar url. Another key will discarded when import.

```json
[
  {
    "Email": "mymail@mymail.com",
    "Name": "Nama",
    "AvatarUrl": "https://placehold.it/20x20",
    "AuthenticationToken": "randomstring",
    "Password": "password",
    "CreateAt": "2017-05-10T11:46:30Z"
  }
]
```

** Rooms **
* Unique id must be unique at application level (you cannot insert a new
data with same unique id AND application id), and you must have no same
unique id in your database right now (you can check it by export it first).
* Avatar URL should be https.
* If room type is single, the name inserted into db will be
changed by logic using template “partcicipant1_email <<space>>
participant2_email“, so please to make sure that if your room type is single,
your participant must contains exactly 2 participant AND one of that
participant is specified at CreatorEmail. Otherwise, if room type is group,
Name will be the name of group.
* CreatorEmail and all of ParticipantEmails must be exists in database
(check by make an export users first).
```json
[
  {
    "Name": "demo1@linkdokter.com 4992614d-9d32-4cc4-ae8e-310a7a0fdbb9",
    "Type": "single",
    "Options": "",
    "CreatorEmail": "user@mymail.com",
    "CreatedAt": "2017-05-11T06:35:27Z",
    "AvatarUrl": "",
    "UniqueId": "f82e5262-e9c4-4b7b-867a-ea890ba64f43",
    "ParticipantEmails": [
      "user@mymail.com",
      "mymail@mymail.com"
    ]
  },
  {
    "Name": "Qiscus Family Super",
    "Type": "group",
    "Options": "",
    "CreatorEmail": "user@mymail.com",
    "CreatedAt": "2017-05-11T06:35:27Z",
    "AvatarUrl": "",
    "UniqueId": "f82e5262-e9c4-4b7b-867a-ea890ba64f43",
    "ParticipantEmails": [
      "user@mymail.com",
      "mymail@mymail.com",
      "newuser@mymail.com"
    ]
  }
]
```

** Comments **

* UniqueId must be unique, and you must have no same unique id in your database
right now (you can check it by export it first).
* RoomUniqueId must be exists in database (check by export it first).
* CreatorEmail must be exists in database.
* We remind you to only import comment using type **text **or **reply** only,
since custom format may not fully supported.


Since comment has multiple type with different payload (and it must passes an
validator for each type), you must specify a correct payload. You may notice
that for some type, you need to pass an exact value, for example is
replied_comment_id in type reply, it can be tricky since we cannot get exact
value to get which comment id should be referred (because payload is saved
in **JSON** data type and it **cannot be related to any foreign key**). But,
thanks to RDBMS which can handle this problem. For type **reply **you must
specify a value ParentCommentUniqueId, it can be related to comment unique
id that already exist in database or UniqueId that you are specify before
current object data.

> You can refer payload format in post comment section.

Tips for import comment:
Type: reply
**text**: same as message
**replied_comment_id**: 1, you must type literally integer 1 number, since it is means true when it came to validator service.

```json
{
    "text": "ini comment",
    "replied_comment_id": 1
}
```

Example data to import:
```json
[
    {
        "Message": "Halo doc",
        "DisableLinkPreview": false,
        "Type": "text",
        "UniqueId": "android_14945300625232b81ffc0520f961",
        "CreatorEmail": "userid_844_6285868233422@kiwari-stag.com",
        "RoomUniqueId": "4e6c208b-3436-46a0-a6d7-add9b90dfc77",
        "CreatedAt": "2017-05-11T19:14:24Z",
        "Payload": null,
        "ParentCommentUniqueId": ""
    },
    {
        "Message": "Maaf mau tanya..",
        "DisableLinkPreview": false,
        "Type": "reply",
        "UniqueId": "android_14945300625232b81ffc0520f962",
        "CreatorEmail": "userid_844_6285868233422@kiwari-stag.com",
        "RoomUniqueId": "4e6c208b-3436-46a0-a6d7-add9b90dfc77",
        "CreatedAt": "2017-05-11T19:14:24Z",
        "Payload": {
            "text": "Maaf mau tanya..",
            "replied_comment_id": 1
        },
        "ParentCommentUniqueId": "android_14945300625232b81ffc0520f961"
      }
]
```

## Get Imported List
verb:
`GET /api/v2/rest/imports`
request:
```bash
page [int] page number, optional
```
response:
```json
{
    "results": {
        "backup_histories": [
            {
                "created_at": "2017-07-24T16:34:57+07:00",
                "errors": {},
                "original_filename": "comment_single.json",
                "resource_name": "comments",
                "size": 926,
                "status": "finished",
                "total_rows": 1,
                "unique_id": "85cfa162-f8ac-4e91-a6a4-a2e4ab25e150"
            }
        ]
    },
    "status": 200
}
```

# Webhooks
Webhooks make it super easy to build on top of Qiscus SDK. They are
user-defined callbacks. They are triggered by events -- in this case, messages
from customers and businesses. When the event occurs, the webhook will
make a http(s) call to the URI it’s configured to.

## on post message
Webhooks on post message being triggered either from sdk client side or
from REST API

PROTOCOL : HTTPS
VERB : POST

payload being send to your endpoint is below
```json
{
    "type": "post_comment_mobile", // either type "post_comment_mobile" if from client side or "post_comment_rest" if from REST API
    "payload": {
        "from": {
            "id": 1,
            "email": "user1@gmail.com",
            "name": "User1",
        },
        "room": {
            "id": 1,
            "topic_id": 1,
            "type": "group", # can also be single
            "name": "ini grup",
            "participants": [
                {
                    "id": 1,
                    "email": "user1@gmail.com",
                    "username": "User1",
                    "avatar_url": "http://avatar1.jpg"
                },
                {
                    "id": 2,
                    "email": "user2@gmail.com",
                    "username": "User2",
                    "avatar_url": "http://avatar2.jpg"
                }
            ]
        },
        "message": {
            "type": "text",
            "text": "ini pesan",
            "payload": {
                # comment type specific payload
            }
        }
    }
}
```