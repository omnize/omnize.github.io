# Interactions API
To get the access token, go to:
```
https://zchat-admin.zenvia.com
```
Then go to:
```
Menu > Settings > Integrations > API
```
Click on 'Generate Token' to obtain a new one.

## Start interaction
Make HTTP **POST** request:
```
https://zchat.zenvia.io/core/api/v1/interactions
```
Body Example:
```
{
  "token": "YourApiToken",
  "media_type": "TEXT",
  "department_id": 9999,
  "customer": {
    "name": "Name Surname",
    "email": "name@example.com",
    "phone": "11991417777",
    "cpf": "12345678900"
  },
  "extra" : {
    "clientId": "1",
    "botId": "1111"
  },
  "external_history": "https://chat-history.example.com"
}
```
Parameter | Type | Required | Description | Default Attributes |
------------ | ------------- | ------------- | ------------- | ------------- |
token | string | **true** | Your API token | - |
department_id | integer | **true** | Id of an active department from your account | - |
media_type | string | **false** | Type of media | TEXT, SMS, WHATSAPP  **(null will be saved as TEXT)** |
extra | object | **false** | Any parameters **(will be returned on webhook)** | - |
customer | object | **false** | Your customer information | { "phone", "cpf", "name", "email" } |
name | string | **false** | Customer's name | - |
email | string | **false** | Customer's email | - |
phone | string | **false** | Customer's phone | - |
cpf | string | **false** | Customer's document | - |
external_history | string | **false** | URL that can GET a JSON | - |

Success Response:
```
{
  "message": "Interaction created successfully",
  "data": {
    "interaction_hash": "0000a-000b-0c00-0d0e-f00d00f11111"
  }
}
```

Error Response:
```
{
    "message": "Error description here",
    "status": 422
}
```
## Update interaction
Make HTTP **PUT** request:
```
https://zchat.zenvia.io/core/api/v1/interactions/{interactionHash}
```
| Parameter | Required  | Description | Default Attributes |
| ------------ | ------------ | ------------ | ------------ |
| interaction_hash | **true** | Unique id for the interaction (UUID) | - |
<br> Body Example:
```
{
  "token": "YourApiToken",
  "mood": "POSITIVE",
  "tag_ids": ["1", "999"],
  "customer_key": "0010-abcd-efgh-ijkd-1c422e49fdff",
  "note": "Any note here"
}
```
Parameter | Type | Required | Description | Default Attributes |
------------ | ------------- | ------------- | ------------- | ------------- |
token | string | **true** | Your API token | - |
mood | string | **false** | Service evaluation | "POSITIVE" or "NEGATIVE" |
tag_ids | array | **false** | Ids of the tags used in this interaction 
customer_key | string | **false** | Id of a customer (UUID) | - |
note | string | **false** | any string

Success Response:
```
{
    "message": "Interaction updated successfully",
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

## Send message
Make HTTP **POST** request:
```
https://zchat.zenvia.io/core/api/v1/interactions/{interactionHash}/messages
```
| Parameter | Required  | Description | Default Attributes |
| ------------ | ------------ | ------------ | ------------ |
| interaction_hash | **true** | Unique identification for the interaction (UUID) | - |
<br> Body Example: 
```
{
  "token": "yourAPIToken",
  "content": "your message",
  "type": "image",
  "url": "https://file-address.example.com/logo.png"
}
```
Parameter | Type | Required | Description | Default Attributes |
------------ | ------------- | ------------- | ------------- | ------------- |
token | string | **true** | Your API token | - |
content | string | **true** | Your message | - |
type | string | **false** | Type of the content |text, image, video, audio, file **(null will be saved as text)** |
url | string | **false** | File URL (except for "text" type message) | - |
<br> Success Response Example:
```
{
    "data": {
        "interaction_hash": "0010-abcd-efgh-ijkd-1c422e49fdff"
    },
    "message": "Message created successfully",
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

## Notify when client typing
Make HTTP **PUT** request:
```
https://zchat.zenvia.io/core/api/v1/interactions/{interactionHash}/typing
```
| Parameter | Required  | Description | Default Attributes |
| ------------ | ------------ | ------------ | ------------ |
| interaction_hash | **true** | Unique identification for the interaction (UUID format) | - |

Body Example:
```
{
  "token": "YourApiToken"
}
```
Parameter | Type | Required | Description |Default Attributes |
------------ | ------------- | ------------- | ------------- | ------------- |
token | string | **true** | Your API token | - |
<br> Success Response:
```
{
  "message": "Typing sent successfully",
  "status": 200
}
```

## Notify when client stop typing
Make HTTP **PUT** request:
```
https://zchat.zenvia.io/core/api/v1/interactions/{interactionHash}/cleared
```
| Parameter | Required  | Description | Default Attributes |
| ------------ | ------------ | ------------ | ------------ |
| interaction_hash | **true** | Unique identification for the interaction (UUID format) | - |

Body Example:
```
{
  "token": "YourApiToken"
}
```
Parameter | Type | Required | Description |Default Attributes |
------------ | ------------- | ------------- | ------------- | ------------- |
token | string | **true** | Your API token | - |
<br> Success Response:
```
{
  "message": "Cleared sent successfully",
  "status": 200
}
```

## Finish Interaction
Make HTTP **PUT** request:
```
https://zchat.zenvia.io/core/api/v1/interactions/{interactionHash}/finish
```
| Parameter | Required  | Description | Default Attributes |
| ------------ | ------------ | ------------ | ------------ |
| interaction_hash | **true** | Unique identification for the interaction (UUID) | - |

Body Example:
```
{
  "token": "YourApiToken"
}
```
Parameter | Type | Required | Description |Default Attributes |
------------ | ------------- | ------------- | ------------- | ------------- |
token | string | **true** | Your API token | - |
<br> Success Response:
```
{
  "message": "Finish sent successfully",
  "status": 200
}
```

## External History
Endpoint that **GET** a JSON:

Response:
```
{
  "messages":[
    {
      "time":"2019-03-14 00:00:01",
      "direction":"CLIENT",
      "content":"client message here"
    },
    {
      "time":"2019-03-14 00:00:10",
      "direction":"AGENT",
      "content":"agent answer here"
    }
  ]
}
```
Parameter | Type | Required | Description | Default Attributes |
------------ | ------------- | ------------- | ------------- | ------------- |
messages | array | **true** | Array of message objects | - |
time | datetime | **true** | When the message was recorded | - |
direction | string | **true** | Who sent the mesage | "CLIENT" or "AGENT" |
content | string | **true** | Content of the message | - |
<br>

## Triggers

To set up a webhook URL, access:
```
https://zchat-admin.zenvia.com
```
Go to:
```
Menu > Settings > Integrations > Weebhooks
```
Add your URL to receive the trigger events.

### Interaction added to queue

    {
      "interaction_hash": "322e458c-540c-4c11-ab5c-d38d39f57213",
      "state": "queued",
      "position": 1,
      "extra": {}
    }

### Agent accepts interaction

    {
      "interaction_hash": "322e458c-540c-4c11-ab5c-d38d39f57213",
      "state": "accepted",
      "extra": {}
    }

### In case of unavailable agents:

    {
      "interaction_hash": "322e458c-540c-4c11-ab5c-d38d39f57213",
      "state": "unavailable",
      "extra": {}
    }

###  Agent finish interaction:

    {
      "interaction_hash": "322e458c-540c-4c11-ab5c-d38d39f57213",
      "state": "finished",
      "extra": {}
    }

###  Agent typing:

    {
      "interaction_hash": "322e458c-540c-4c11-ab5c-d38d39f57213",
      "state": "typing",
      "extra": {}
    }

###  Agent stop typing:

    {
      "interaction_hash": "322e458c-540c-4c11-ab5c-d38d39f57213",
      "state": "cleared",
      "extra": {}
    }

### Agent new message:

    {
      "interaction_hash": "322e458c-540c-4c11-ab5c-d38d39f57213",
      "message": {
        "hash": "3110a5da-87c7-4f6d-a4ab-2b1ed5edfd46",
        "content": "Message",
        "type": "text",
        "url": "http://..."
      },
      "agent": {
        "id": 111,
        "name": "Atendente"
      },
      "extra": {}
    }
