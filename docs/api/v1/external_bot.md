# External bot
To activate external bot contact suport

```

## Enable and update external_bot
make **PUT** HTTP request:
```
http://partner.omnize.com/api/v1/departments/{department_id}
```
body:

Parameter | Type | Required | Valid Attribute |
------------ | ------------- | ------------- | ------------- |
token | string | **true** | your partner token |
department | object | **true** | {"has_external_bot", "external_bot_url"} |

Example:
```
{
  "token": ".......",
  "department": {
    "external_bot_url": "http://.....",
    "has_external_bot": true
  }
}
```
Valid Response:
```
{
  "success": true,
  "status": 200,
  "data": {...}
}
```
Error Response:
```
{
    "success": false,
    "errors": "Invalid token"
}
```


## Make interaction
#### Start widget, select a department with bot and click on "Chat"
Will receive a **POST** on bot endpoint with body:

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

#### Accept
make **PUT** HTTP request:
```
 https://zchat.zenvia.io/core/api/v1/bot/{interaction_hash}/accept
```
body:

Parameter | Type | Required | Valid Attribute |
------------ | ------------- | ------------- | ------------- |
token | string | **true** | your clientSdk token |

Valid Response:
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

#### Finish
make **PUT** HTTP request:
```
 https://zchat.zenvia.io/core/api/v1/bot/{interaction_hash}/finish
```
body:

Parameter | Type | Required | Valid Attribute |
------------ | ------------- | ------------- | ------------- |
token | string | **true** | your clientSdk token |

Valid Response:
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
#### Transfer
make **PUT** HTTP request:
```
 https://zchat.zenvia.io/core/api/v1/bot/{interaction_hash}/transfer
```
body:

Parameter | Type | Required | Valid Attributes |
------------ | ------------- | ------------- | ------------- |
token | string | **true** | your clientSdk token |
department_id | integer | false | any active department_id from your account **(null will be transferred to the department that the interaction started)** |

Valid Response:
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

#### Send message
make **POST** HTTP request:
```
 https://zchat.zenvia.io/core/api/v1/bot/{interaction_hash}/message
```
body:

Parameter | Type | Required | Valid Attributes |
------------ | ------------- | ------------- | ------------- |
token | string | **true** | your clientSdk token |
content | string | **true** | any string |
content_type | string | false | text, image, video, audio, file **(null will be saved as text)** |
attachment | object | false | { "url", "size"} |


Attachment Paramenter | Type | Required | Valid Attributes |
------------ | ------------- | ------------- | ------------- |
url | string | **true** | valid url |
size | string | false | any string |

Example:
```
{
  "token": "y0urC1lientT0ken",
  "content": "your message here",
  "content_type": "image",
  "attachment": {
    "url": "https://omz-logos.s3.amazonaws.com/logo_omz.png",
    "size": "1.0MB"
  }
}
```

Valid Response:
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

#### When client send a message
Will receive a **POST** on endpoint with body:

Parameter | Type | Value |
------------ | ------------- | ------------- |
type | string | new_message |
interaction_hash | string | uuid |
content | string | any string |
content_type | string | text, image, video, audio or file |

Example:
```
{
  "type": "new_message",
  "interaction_hash": "0000a-000b-0c00-0d0e-f00d00f11111",
  "content": "Test message",
  "content_type": "text"
}
```

#### When client finishes the interaction
Will receive a **POST** on endpoint with body:

Parameter | Type | Value |
------------ | ------------- | ------------- |
type | string | finished_interaction |
interaction_hash | string | uuid |

Example:
```
{
  "type": "finished_interaction",
  "interaction_hash": "0000a-000b-0c00-0d0e-f00d00f11111"
}
```
