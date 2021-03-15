# Whatsapp Api
To get the access token, go to:
```
https://zchat-admin.zenvia.com
```
Then go to:
```
Menu > Settings > Integrations > API
```
Click on 'Generate Token' to obtain a new one.

## Send message
Make HTTP **POST** request:

    https://zchat.zenvia.io/core/api/v1/whatsapp

Body Example:

    {
      "token": "yourAPIToken",
      "content": "Message",
      "content_type": "image/png",
      "url": "https://file-address.example.com/logo.png",
      "department_id": 1,
      "customer": {
        "name": "Name Surname",
        "email": "customer@email.com",
        "phone": "123456789",
        "cpf": "123456789",
        "external_id": "123456",
      },
      "extra" : {
        "clientId": "1",
        "botId": "1111"
      },
	  "external_history": "https://chat-history.example.com"
    }
Parameter | Type | Required | Description | Default Attributes |
------------ | ------------- | ------------- | ------------- | ------------- |
token | string | **true** | Your API token | - |
content | string | **false** | Message content | - |
content_type | string | **false** | Type of the content | audio, image, text, video, file, **(null will be saved as text)** |
url | string | **false** |  File URL (except for "text" type message) | - | 
department_id | integer | **true** | Id of an active department from your account | - |
customer | object | **true** | Your customer information | { "phone", "cpf", "name", "email", "external_id" } |
name | string | **false** | Customer's name | - |
email | string | **false** | Customer's email | - |
phone | string | **false** | Customer's phone | - |
cpf | string | **false** | Customer's document | - |
external_id | string | **true** | Customer's id in an external system | - |
extra | object | **false** | Any parameters **(will be returned on webhook)** | - |
external_history | string | **false** | URL that can GET a JSON | - |
<br>Success Response:

    {
      "message": "Message sent successfully",
    }


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

###  Agent finish interaction:

    {
      "external_id": "abcd1234",
      "interaction_hash": "322e458c-540c-4c11-ab5c-d38d39f57213",
      "state": "finished"
    }

###  Agent typing:

    {
      "external_id": "abcd1234",
      "interaction_hash": "322e458c-540c-4c11-ab5c-d38d39f57213",
      "state": "typing"
    }

###  Agent stop typing:

    {
      "external_id": "abcd1234",
      "interaction_hash": "322e458c-540c-4c11-ab5c-d38d39f57213",
      "state": "cleared"
    }

### Agent new message:

    {
      "external_id": "abcd1234",
      "interaction_hash": "322e458c-540c-4c11-ab5c-d38d39f57213",
      "message": {
        "content": "Message",
        "type": "text"
      },
      "agent": {
        "id": 123,
        "name": "Agent"
      }
    }

### Agent transfer interaction to department

    {
      "external_id": "abcd1234",
      "interaction_hash": "322e458c-540c-4c11-ab5c-d38d39f57213",
      "state": "transferred",
      "department_id": "1545"
    }
