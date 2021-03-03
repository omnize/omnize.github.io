## ClientApi V1
To get the access token and set a webhook URL, access:
```
https://zchat-admin.zenvia.com
```
Go to:
```
Menu > Settings > Integrations > API
```
Click on 'Generate Token' to obtain a new one. Add your URL at 'Webhook URL' to receive the trigger events.


#### Start interaction
Make HTTP **POST** request:
```
https://zchat.zenvia.io/core/api/v1/interactions
```
Body:
```
{
  "token": "yourAPIToken",
  "media_type": "TEXT",
  "department_id": 1,
  "customer": {
    "name": "Name Surname",
    "email": "name@example.com",
    "phone": "11991417777",
    "cpf": "12345678900"
  },
  "extra" : {
    "clientId": "any",
    "botId": "any"
  },
  "external_history": "https://test.com"
}
```
Parameter | Type | Required | Description | Default Attributes |
------------ | ------------- | ------------- | ------------- | ------------- |
token | string | **true** | Your API token | - |
department_id | integer | **true** | Id of an active department from your account | - |
media_type | string | false | Type of media | TEXT, SMS, WHATSAPP  **(null will be saved as TEXT)** |
extra | object | false | Any parameters **(will be returned on webhook)** | - |
customer | object | false | Your customer information | { "phone", "cpf", "name", "email" } |
external_history | string | false | URL that can GET a JSON | - |

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

#### External History
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
messages | array of objects | **true** | Array of message objects | - |
time | datetime | **true** | When the message was recorded | - |
direction | string | **true** | Who sent the mesage | "CLIENT" or "AGENT" |
content | string | **true** | Content of the message | - |

#### Update interaction
Make HTTP **PUT** request:
```
https://zchat.zenvia.io/core/api/v1/interactions/{interaction_hash}
```
| Parameter | Required  | Description | Default Attributes |
| ------------ | ------------ | ------------ | ------------ |
| interaction_hash | **true** | Unique identification for the interaction (UUID format) | - |
Body:
```
{
  "token": "y0UrCl1EntSdk",
  "mood": "POSITIVE",
  "tag_ids": ["1", "999"],
  "customer_key": "0010-abcd-efgh-ijkd-1c422e49fdff",
  "note": "any note here"
}
```
Parameter | Type | Required | Valid Attributes |
------------ | ------------- | ------------- | ------------- |
token | string | **true** | your clientSdk token
mood | string | false | "POSITIVE", "NEGATIVE"
tag_ids | array | false | your tag_ids
customer_key | string | false | your existing customer
note | string | false | any string

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

#### Send message
Make HTTP **POST** request:
```
https://zchat.zenvia.io/core/api/v1/interactions/{interactionHash}/messages
```
| Parameter | Required  | Description | Default Attributes |
| ------------ | ------------ | ------------ | ------------ |
| interaction_hash | **true** | Unique identification for the interaction (UUID format) | - |
Body:
```
{
  "token": "yourAPIToken",
  "content": "your message",
  "type": "image",
  "url": "https://omz-logos.s3.amazonaws.com/logo_omz.png"
}
```
Parameter | Type | Required | Description | Default Attributes |
------------ | ------------- | ------------- | ------------- | ------------- |
token | string | **true** | Your API token | - |
content | string | **true** | Your message | - |
type | string | false | Type of the content |text, image, video, audio, file **(null will be saved as text)** |
url | string | **false** | File URL (except for "text" type) | - |
Success Response:
```
{
    "data": {
        "interaction_hash": "interaction_hash"
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

#### Notify when client typing
Make HTTP **PUT** request:
```
https://zchat.zenvia.io/core/api/v1/interactions/{interactionHash}/typing
```
| Parameter | Required  | Description | Default Attributes |
| ------------ | ------------ | ------------ | ------------ |
| interaction_hash | **true** | Unique identification for the interaction (UUID format) | - |

Body:
```
{
  "token": "YourApiToken"
}
```
Parameter | Type | Required | Description |Default Attributes |
------------ | ------------- | ------------- | ------------- | ------------- |
token | string | **true** | Your API token | - |

#### Notify when client stop typing
Make **PUT** HTTP request:
```
https://zchat.zenvia.io/core/api/v1/interactions/{interactionHash}/cleared
```
| Parameter | Required  | Description | Default Attributes |
| ------------ | ------------ | ------------ | ------------ |
| interaction_hash | **true** | Unique identification for the interaction (UUID format) | - |

Body:
```
{
  "token": "YourApiToken"
}
```
Parameter | Type | Required | Description |Default Attributes |
------------ | ------------- | ------------- | ------------- | ------------- |
token | string | **true** | Your API token | - |


#### Finish interaction
Make **PUT** HTTP request:
```
https://zchat.zenvia.io/core/api/v1/interactions/{interactionHash}/finish
```
| Parameter | Required  | Description | Default Attributes |
| ------------ | ------------ | ------------ | ------------ |
| interaction_hash | **true** | Unique identification for the interaction (UUID format) | - |

Body:
```
{
  "token": "YourApiToken"
}
```
Parameter | Type | Required | Description |Default Attributes |
------------ | ------------- | ------------- | ------------- | ------------- |
token | string | **true** | Your API token | - |


## Triggers

#### Interaction added to queue

    {
      "interaction_hash": "322e458c-540c-4c11-ab5c-d38d39f57213",
      "state": "queued",
      "position": 1,
      "extra": {}
    }

#### Agent accepts interaction

    {
      "interaction_hash": "322e458c-540c-4c11-ab5c-d38d39f57213",
      "state": "accepted",
      "extra": {}
    }

#### In case of unavailable agents:

    {
      "interaction_hash": "322e458c-540c-4c11-ab5c-d38d39f57213",
      "state": "unavailable",
      "extra": {}
    }

####  Agent finish interaction:

    {
      "interaction_hash": "322e458c-540c-4c11-ab5c-d38d39f57213",
      "state": "finished",
      "extra": {}
    }

####  Agent typing:

    {
      "interaction_hash": "322e458c-540c-4c11-ab5c-d38d39f57213",
      "state": "typing",
      "extra": {}
    }

####  Agent stop typing:

    {
      "interaction_hash": "322e458c-540c-4c11-ab5c-d38d39f57213",
      "state": "cleared",
      "extra": {}
    }

#### Agent new message:

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
