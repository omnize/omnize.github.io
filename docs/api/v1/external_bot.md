# External bot
To activate external bot, please, contact suport.

## Create an Interaction
### Start widget, select a department with an enabled bot and click on "Chat"
It will receive a HTTP **POST** request at the bot endpoint with body:

Parameter | Type | Value |
------------ | ------------- | ------------- |
type | string | new_interaction |
interaction_hash | string | uuid |
department_id | integer | your department_id |

Example:
```
{
  "type": "new_interaction",
  "interaction_hash": "0000a-000b-0c00-0d0e-f00d00f11111",
  "department_id": 1
}
```

## Accept
Make HTTP **PUT** request:
```
 https://zchat.zenvia.io/core/api/v1/bot/{interaction_hash}/accept
```
| Parameter | Required  | Description | Default Attributes |
| ------------ | ------------ | ------------ | ------------ |
| interaction_hash | **true** | Unique identification for the interaction (UUID) | - |

<br> Body Example: 
```
{
  "token": "YourApiToken"
}
```

Parameter | Type | Required | description | Default Attribute |
------------ | ------------- | ------------- | ------------- | ------------- |
token | string | **true** | Your API token | -|

Success Response:
```
{
  "message": "Message received successfully",
  "status": 200
}
```
Error Response:
```
{
    "message": "Error description here",
    "status": 422
}
```

### Finish
Make HTTP **PUT** request:
```
 https://zchat.zenvia.io/core/api/v1/bot/{interaction_hash}/finish
```
| Parameter | Required  | Description | Default Attributes |
| ------------ | ------------ | ------------ | ------------ |
| interaction_hash | **true** | Unique identification for the interaction (UUID) | - |

<br> Body Example: 
```
{
  "token": "YourApiToken"
}
```

Parameter | Type | Required | description | Default Attribute |
------------ | ------------- | ------------- | ------------- | ------------- |
token | string | **true** | Your API token | -|

Success Response:
```
{
  "message": "Message received successfully",
  "status": 200
}
```
Error Response:
```
{
  "message": "Error description here",
  "status": 422
}

```
### Transfer
Make HTTP **PUT** request:
```
 https://zchat.zenvia.io/core/api/v1/bot/{interaction_hash}/transfer
```
| Parameter | Required  | Description | Default Attributes |
| ------------ | ------------ | ------------ | ------------ |
| interaction_hash | **true** | Unique identification for the interaction (UUID) | - |

<br> Body Example: 
```
{
  "token": "YourApiToken",
  "department_id": 9999
}
```

Parameter | Type | Required | Description | Default Attribute |
------------ | ------------- | ------------- | ------------- | ------------- |
token | string | **true** | Your API token | - |
department_id | integer | **false** | Id of an active department **(null will be transferred to the department that the interaction started)** | - |

Success Response:
```
{
  "message": "Message received successfully",
  "status": 200
}
````
Error Response:
```
{
  "message": "Error description here",
  "status": 422
}
```

### Send message
Make HTTP **POST** request:
```
 https://zchat.zenvia.io/core/api/v1/bot/{interaction_hash}/message
```
| Parameter | Required  | Description | Default Attributes |
| ------------ | ------------ | ------------ | ------------ |
| interaction_hash | **true** | Unique identification for the interaction (UUID) | - |

<br> Body Example: 
```
{
  "token": "YourAPIToken",
  "content": "your message",
  "content_type": "image",
  "attachment": {
    "url": "https://file-address.example.com/logo.png",
    "size": "1.0MB"
  }
}
```

Parameter | Type | Required | Description | Default Attribute |
------------ | ------------- | ------------- | ------------- | ------------- |
token | string | **true** | Your API token | - |
content | string | **true** | Message content | - |
content_type | string | **false** | Type of the content | audio, image, text, video, file, **(null will be saved as text)** |
attachment | object | **false**  | Information about the file attachment | { "url", "size"} |
url | string | **false** |  File URL (except for "text" type message) | - | 
size | string | **false**  | File size | - |

Success Response:
```
{
  "message": "Message received successfully",
  "status": 200
}
```
Error Response:
```
{
  "message": "Error description here",
  "status": 422
}
```

### When client send a message
It will receive a HTTP **POST** request at the bot endpoint with body:

Parameter | Description | Default Value
------------ | ------------- | ------------- |
type | Type of request | new_message
interaction_hash | Unique id for the interaction (uuid) |
content | Content of the message |
content_type | Message content type | text, image, video, audio or file |

Body Example:
```
{
  "type": "new_message",
  "interaction_hash": "0000a-000b-0c00-0d0e-f00d00f11111",
  "content": "Test message",
  "content_type": "text"
}
```

### When client finishes the interaction
It will receive a HTTP **POST** request at the bot endpoint with body:

Parameter | Description | Default Value |
------------ | ------------- | ------------- |
type | Type of request | finished_interaction |
interaction_hash | Unique id for the interaction (uuid) |

Body Example:
```
{
  "type": "finished_interaction",
  "interaction_hash": "0000a-000b-0c00-0d0e-f00d00f11111"
}
```
