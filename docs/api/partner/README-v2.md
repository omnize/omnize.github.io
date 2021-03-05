# Partner API

## List Agents

  Make HTTP **GET** request:
 ```
  https://zchat.zenvia.io/partner/api/agents?token={youApiTYoken}&account_id={accountId}&search={searchParamenter}&column={orderParameter}&direction={orderDirection}&page={page}&limit={limit}
  ```
| Parameter  | Required  | Description | Default Attributes |
| ------------ | ------------ | ------------ | ------------ |
| token | **true** | Your API token | - |
| account_id | **true** | Id of an account | - |
| search | **false** | Filter agents | "name" or "email" |
| column | **false** | Order agents | "id", "name"  or "email" (default: "id") |
| direction | **false** | Descending or ascending order | "desc" or "asc" (default: desc) |
| page | **false** | Number of the page  | >=1 (default:20) |
| limit | **false** | Max number of agents per page  | Any integer number (default:20) |

Success Response Example:

    {
      "status": 200,
      "success": true,
      "agents": [
        {
          "id": 1,
          "name": "Agent Name",
          "photo": "https://file-address.example.com/agent.png",
          "phone_extension": null,
          "signature": null,
          "email": "agent@example.com",
          "deleted_at": null,
          "active": true,
          "departments": [
            {
              "id": 1,
              "name": "Atendimento"
            }
          ],
          "status": "OFFLINE",
          "profile": "ADMIN",
          "created_at": "2021-03-02T19:24:32.417Z",
          "updated_at": "2021-03-02T19:24:32.417Z"
        }
      ]
    }

Error Response:

    {
      "status": 200,
      "success": false,
      "errors": "Error description here"
    }

## Show Agent
Make HTTP **GET** request:
```
https://zchat.zenvia.io/partner/api/agents/{id}?token={yourApiToken}&account_id={accountId}
```
| Parameter  | Required  | Description | Default Attributes |
| ------------ | ------------ | ------------ | ------------ |
| token | **true** | Your API token | - |
| account_id | **true** | Id of an account | - |
| id | **true** | Id of an agent from this account | - |

Success Response Example:

    {
      "status": 200,
      "success": true,
      "agent": { 
        "id": 1,
        "name": "Agent Name",
        "photo": "https://file-address.example.com/agent.png",
        "phone_extension": null,
        "signature": null,
        "email": "agent@example.com",
        "deleted_at": null,
        "active": true,
        "departments": [
          {
            "id": 1,
            "name": "Atendimento"
          }
        ],
        "status": "OFFLINE",
        "profile": "AGENT",
        "created_at": "2019-11-21T18:44:13.628Z",,
        "updated_at": "2021-02-26T14:37:35.000Z"
      }
    }

Error Response:

    {
      "status": 200,
      "success": false,
      "errors": "Error description here"
    }


## Create Agent
Make HTTP **POST** request:

    https://zchat.zenvia.io/partner/api/agents

Body Example:

    {
      "token": "yourApiToken",
      "profile": "ADMIN",
      "department_ids": [1,22,333],
      "agent": {
        "email": "test@example.com",
        "name": "Test Agent",
        "password": "03ac674216f3e15c761ee1a5e255f067953623c8b388b4459e13f978d7c846f4",
        "text_limit": 7,
        "account_id": 1111
      }
    }
Parameter | Type | Required | Description | Default Attributes |
------------ | ------------- | ------------- | ------------- | ------------- |
token | string | **true** | Your API token | - |
profile | string | **false** | Level of permission this agent will have |"ADMIN" or "AGENT" (**null will be saved as "AGENT"**) |
department_ids | array | **false** | Ids of this agent's departments (null will add to first account department) | - |
agent | object | **true** | Agent's data | { "name", "email", "password", "text_limit" } |
name | string | **true** | Agent's name | - |
email | string | **true** | Agent's email | - |
password | string | **true** | Agent's password signed as SHA256 hash | - |
text_limit | string | **false** | Text limit | - |
account_id | integer | **true** | Id of this agent's account | - |

Success Response Example:

    {
      "status": 200,
      "success": true,
      "agent": {
        "id": 1,
        "name": "Agent Name",
        "photo": null,
        "phone_extension": null,
        "signature": null,
        "email": "agent@example.com",
        "deleted_at": null,
        "active": true,
        "departments": [
          {
            "id": 1,
            "name": "Atendimento"
          }
        ],
        "status": "OFFLINE",
        "profile": "ADMIN",
        "created_at": "2020-10-21T12:46:12.648Z",
        "updated_at": "2020-10-21T12:46:12.648Z"
      }
    }

Error Response:

    {
      "status": 200,
      "success": false,
      "errors": "Error description here"
    }

## Update Agent
Make a HTTP **PUT** request:

    https://zchat.zenvia.io/partner/api/agents/{id}

| Parameter  | Required  | Description | Default Attributes |
| ------------ | ------------ | ------------ | ------------ |
| id | **true** | Id of the agent that will be updated | - |

Body Example:

    {
      "token: 'YourApiToken',
      "profile": 'ADMIN',
      "agent": {
        "account_id": 1111,
        "email": "update@example.com",
        "name": "New Name",
        "text_limit": 7,
        "password": "03ac674216f3e15c761ee1a5e255f067953623c8b388b4459e13f978d7c846f4",
        "active": true  
      }
    }

Parameter | Type | Required | Description | Default Attributes |
------------ | ------------- | ------------- | ------------- | ------------- |
token | string | **true** | Your API token | - |
profile | string | **false** | Level of permission this agent will have |"ADMIN" or "AGENT" (**null will be saved as "AGENT"**) |
department_ids | array | **false** | Ids of this agent's departments (null will add to first account department) | - |
agent | object | **true** | Agent's data | { "name", "email", "password", "text_limit" } |
name | string | **true** | Agent's name | - |
email | string | **true** | Agent's email | - |
password | string | **true** | Agent's password signed as SHA256 hash | - |
text_limit | string | **false** | Text limit | - |
account_id | integer | **true** | Id of this agent's account | - |

Success Response Example:

    {
      "status": 200,
      "success": true,
      "agent": {
        "id": 1,
        "name": "Agent Name",
        "photo": null,
        "phone_extension": null,
        "signature": null,
        "email": "agent@example.com",
        "deleted_at": null,
        "active": true,
        "departments": [
          {
            "id": 1,
            "name": "Atendimento"
          }
        ],
        "status": "OFFLINE",
        "profile": "ADMIN",
        "created_at": "2020-10-21T12:46:12.648Z",
        "updated_at": "2020-10-21T12:46:12.648Z"
      }
    }

Error Response:

    {
      "status": 200,
      "success": false,
      "errors": "Error description here"
    }
    

## Delete Agent
Make HTTP **DELETE** request:

    https://zchat.zenvia.io/partner/api/agents/{id}

With body:

    {
      "token": "YourApiToken",
      "agent": {
        "account_id": 1111
      }
    }

Success Response:

    {
      "status": 200,
      "success": true,
      "message": "Agent deleted successfully"
    }

Error Response:

    {
      "status": 200,
      "success": false,
      "errors": "Error description here"
    }

## List Departments

Make HTTP **GET** request:

    https://zchat.zenvia.io/partner/api/departments?token={yourApiToken}&account_id={accountId}&search={searchParamenter}&column={orderParameter}&direction={orderDirection}&page={page}&limit={limit}

| Parameter  | Required  | Description | Default Attributes |
| ------------ | ------------ | ------------ | ------------ |
| token | **true** | Your API token | - |
| account_id | **true** | Id of an account | - |
| search | **false** | Filter departments | "name" or "id" |
| column | **false** | Order departments | "name" or "id"  (default: "id") |
| direction | **false** | Descending or ascending order | "desc" or "asc" (default: desc) |
| page | **false** | Number of the page  | >=1 (default:20) |
| limit | **false** | Max number of departments per page  | Any integer number (default:20) |

<br> Success Response Example:

    {
      "status": 200
      "departments": [
        {
          "active": true,
          "description": "Atendimento",
          "id": 1,
          "name": "Atendimento",
          "queue": true,
          "queued_max_time": 120,
          "ringing_max_time": 20,
          "queue_position_time": null,
          "deleted_at": null,
          "agents": 2,
          "created_at": "2018-01-02T19:28:41.000Z",
          "updated_at": "2018-01-04T19:28:41.000Z",
          "channels": [
            {
              "id": 3,
              "name": "VOICE",
              "state": 1
            },
            {
              "id": 2,
              "name": "VIDEO",
              "state": 1
            },
            {
              "id": 1,
              "name": "CHAT",
              "state": 1
            }
          ]
        }
      ]
    }

Error Response:

    {
      "status": 200,
      "success": false,
      "errors": "Error description here"
    }


## Create Department
Make HTTP **POST** request:

    https://zchat.zenvia.io/partner/api/departments

Body Example:

    {
      "token": "yourApiToken",
      "agent_ids": [1,22,33],
      "channels": ["chat"],
      "department": {
        "account_id": 1,
        "name": "New Department",
        "description": "A new created department"
      }
    }
Parameter | Type | Required | Description | Default Attributes |
------------ | ------------- | ------------- | ------------- | ------------- |
token | string | **true** | Your API token | - |
agent_ids | array | **false** | List of agent's id for this department | - |
channels | array | **false** | List of channels for this department | "chat", "video", "audio" |
department | object | **true** | The department data | { "account_id", "name", "description" } |
account_id | integer | **true** | Account id for this department | - |
name | string | **false** | Name of the department | - |
description | string | **false** | Description of the department | - |

<br> Success Response Example:

    {
      "status": 200,
      "success": true,
      "department": {
        "active": true,
        "description": "Department description",
        "id": 1,
        "name": "Atendimento",
        "queue": true,
        "queued_max_time": 120,
        "ringing_max_time": 20,
        "queue_position_time": null,
        "deleted_at": null,
        "agents": 0,
        "created_at": "2020-08-21T12:51:10.672Z",
        "updated_at": "2020-10-21T12:56:09.672Z",
        "channels": []
      }
    }

Error Response:

    {
      "status": 200,
      "success": false,
      "errors": "Error description here"
    }

## Update Department
Make HTTP **PUT** request:

    https://zchat.zenvia.io/partner/api/departments/{id}

| Parameter  | Required  | Description | Default Attributes |
| ------------ | ------------ | ------------ | ------------ |
| id | **true** | Id of the department to update | - |

<br> Body Example:

    {
      "token": 'YourApiToken',
      "agent_ids": [1,22,33],
      "channels": ["chat"],
      "department": {
        "account_id": 1,
        "name": "New Name",
        "description": "A new description"
      }
    }
Parameter | Type | Required | Description | Default Attributes |
------------ | ------------- | ------------- | ------------- | ------------- |
token | string | **true** | Your API token | - |
agent_ids | array | **false** | List of agent's id for this department | - |
channels | array | **false** | List of channels for this department | "chat", "video", "voice" |
department | object | **true** | The department data | { "account_id", "name", "description" } |
account_id | integer | **true** | Account id for this department | - |
name | string | **false** | Name of the department | - |
description | string | **false** | Description of the department | - |
<br> Success Response Example:

    {
      "status": 200,
      "success": true,
      "department": {
        "active": true,
        "description": "New description",
        "id": 1,
        "name": "New Name",
        "queue": true,
        "queued_max_time": 120,
        "ringing_max_time": 20,
        "queue_position_time": null,
        "deleted_at": null,
        "agents": 0,
        "created_at": "2020-08-21T12:51:10.672Z",
        "updated_at": "2020-10-21T12:56:09.672Z",
        "channels": []
      }
    }

Error Response:

    {
      "status": 200,
      "success": false,
      "errors": "Error description here"
    }