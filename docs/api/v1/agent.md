# Agent Api
To get the access token, go to:
```
https://zchat-admin.zenvia.com
```
Then go to:
```
Menu > Settings > Integrations > API
```
Click on 'Generate Token' to obtain a new one.
## Get Online Agents
 Make HTTP **GET** request:
```
 https://zchat.zenvia.io/core/api/v1/agents/online?token={yourAPIToken}&department_id={departmentId}
```
| Parameter  | Required  | Description | Default Attributes |
| ------------ | ------------ | ------------ | ------------ |
| token | **true** | Your API token | - |
| department_id | **false** | Id of an active department | - |

<br> Success Response Example:
```
{
    "agents": [
        {
            "id": 9999,
            "name": "Agent Name",
            "photo": "https://file-address.example.com/agent.png"
        }
    ],
    "averageService": 60,
    "count": 10,
    "status": 200
}
```
Response Parameter  | Description |
------------  | -------------
agents | List of online agents - returns **max** of 3 **random** agents
averageService | Average agent answering time of the last 100 interactions (in **seconds**)
count | **Total** of agents online

<br> Error Response:
```
{
    "message": "Error description here",
    "status": 422
{
```

## List Agents
 Make HTTP **GET** request:
```
https://zchat.zenvia.io/api/external/agents?token={yourAPIToken}
```
| Parameter  | Required  | Description | Default Attributes |
| ------------ | ------------ | ------------ | ------------ |
| token | **true** | Your API token | - |

<br> Success Response Example:
```
[
    {
        "id": 99999,
        "name": "Agent Name",
        "photo": "https://file-address.example.com/agent.png",
        "phone_extension": null,
        "signature": null,
        "email": "agent@company.com",
        "deleted_at": null,
        "ativo": 1,
        "active": true,
        "new_status": "OFFLINE",
        "department": {
            "name": "Atendimento",
            "id": 99999
        }
    }
]
```
<br> Error Response:
```
{
  "status": 404,
  "message": "Error Message Here"
}
```

## Get Agent
 Make HTTP **GET** request:
```
https://zchat.zenvia.io/api/external/agents/{agentId}?token={yourAPIToken}
```
| Parameter  | Required  | Description | Default Attributes |
| ------------ | ------------ | ------------ | ------------ |
| token | **true** | Your API token | - |
| agent_id | **true** | Id of an agent | - |

<br> Success Response Example:
```
{
    "id": 9999,
    "name": "Agent Name",
    "photo": "https://file-address.example.com/agent.png",
    "phone_extension": null,
    "signature": null,
    "email": "agent@company.com",
    "deleted_at": null,
    "ativo": 1,
    "active": true,
    "new_status": "OFFLINE",
    "department": {
        "name": "Atendimento",
        "id": 9999
    }
}
```
<br> Error Response:
```
{
  "status": 404,
  "message": "Error Message Here"
}
```

## Create Agent
 Make HTTP **POST**  request:
```
https://zchat.zenvia.io/api/external/agents
```
Body Example:
```
{
	"token": "YourApiToken",
	"name": "Agent Name",
	"email": "agent@company.com",
	"password": "123456",
	"profile": "AGENT",
    "text_limit": "10"
}
```
Parameter | Type | Required | Description | Default Attributes |
------------ | ------------- | ------------- | ------------- | ------------- |
token | string | **true** | Your API token | - |
name | string | **true** | Agent's name | - |
email | string | **true** | Agent's email | - |
password | string | **true** | Agent's password | - |
profile | string | **true** | Level of permission this agent will have |"ADMIN" or "AGENT"
text_limit | string | **false** | Text limit | - |


Success Response Example:
```
{
    "id": 9999,
    "name": "Agent Name",
    "photo": "https://file-address.example.com/agent.png",
    "phone_extension": null,
    "signature": null,
    "email": "agent@company.com",
    "deleted_at": null,
    "ativo": 1,
    "active": true,
    "new_status": "OFFLINE",
    "department": {
        "name": "Atendimento",
        "id": 9999
    }
}
```
Error Response:
```
{
  "status": 200,
  "success": false,
  "errors": [
    "Error description here"
  ]
}
```

## Update Agent
 Make HTTP **PUT** request:
```
https://zchat.zenvia.io/api/external/agents/{agentId}
```
| Parameter  | Required  | Description | Default Attributes |
| ------------ | ------------ | ------------ | ------------ |
| agent_id | **true** | Id of an agent | - |
<br> Body Example:
```
{
	"token": "YourApiToken",
	"name": "Agent Name",
	"email": "agent@company.com",
	"password": "123456",
	"profile": "AGENT",
    "text_limit": "10"
}
```
Parameter | Type | Required | Description | Default Attributes |
------------ | ------------- | ------------- | ------------- | ------------- |
token | string | **true** | Your API token | - |
name | string | **false** | Agent's name | - |
email | string | **false** | Agent's email | - |
password | string | **false** | Agent's password | - |
profile | string | **false** | Level of permission this agent will have |"ADMIN" or "AGENT"
text_limit | string | **false** | Text limit | - |

<br> Success Response Example:
```
{
    "id": 9999,
    "name": "Agent Name",
    "photo": "https://file-address.example.com/agent.png",
    "phone_extension": null,
    "signature": null,
    "email": "agent@company.com",
    "deleted_at": null,
    "ativo": 1,
    "active": true,
    "new_status": "OFFLINE",
    "department": {
        "name": "Atendimento",
        "id": 9999
    }
}
```
<br> Error Response:
```
{
  "status": 404,
  "message": "Error Message Here"
}
```