## Agent Api V1

#### Get Online Agents
 Make **GET** HTTP request:
```
 https://zchat.zenvia.io/core/api/v1/agents/online?token={yourClientSdkToken}&department_id={yourDepartmentId}
```
Parameter  | Required |
------------  | -------------
token | **true**
 department_id | false

Valid Response:
```
{
    "agents": [
        {
            "id": id,
            "name": "Agent Name",
            "photo": "https://omz-photo.s3.amazonaws.com/agent.png"
        }
    ],
    "averageService": 60,
    "count": 10,
    "status": 200
}
```
Response Parameter  | Description |
------------  | -------------
agents | list of online agents - returns **max** of 3 **random** agents
averageService | average time to answer last 100 interactions in **seconds**
count | **total** of agents online

Error Response:
```
{
    "message": "Error description here",
    "status": 422
{
```

#### List Agents
 Make **GET** HTTP request:
```
https://services.omnize.com.br/api/v1/agents?token={yourClientSdkToken}
```
Parameter  | Required |
------------  | -------------
token | **true**

Valid Response:
```
[
    {
        "id": id,
        "name": "Agent Name",
        "photo": "Agent photo url",
        "phone_extension": null,
        "signature": null,
        "new_status": "OFFLINE",
        "department": {
            "name": "Atendimento",
            "id": department_id
        }
    }
]
```

#### Get Agent
 Make **GET** HTTP request:
```
https://services.omnize.com.br/api/v1/agents/{agent_id}?token={yourClientSdkToken}
```
Parameter  | Required |
------------  | -------------
token | **true**
agent_id | **true**

Valid Response:
```
{
    "id": id,
    "name": "Agent Name",
    "photo": "Agent photo url",
    "phone_extension": null,
    "signature": null,
    "new_status": "OFFLINE",
    "department": {
        "name": "Atendimento",
        "id": department_id
    }
}
```

#### Create Agent
 Make **POST** HTTP request:
```
https://services.omnize.com.br/api/v1/agents
```
Parameter  | Required |
------------  | -------------
token | **true**
name | **true**
email | **true**
password | **true**
profile | ["ADMIN","AGENT"]
text_limit | false


Valid Response:
```
{
    "id": id,
    "name": "Agent Name",
    "photo": "Agent photo url",
    "phone_extension": null,
    "signature": null,
    "new_status": "OFFLINE",
    "department": {
        "name": "Atendimento",
        "id": department_id
    }
}
```


#### Update Agent
 Make **PUT** HTTP request:
```
https://services.omnize.com.br/api/v1/agents/{agent_id}
```
Parameter  | Required |
------------  | -------------
token | **true**
agent_id | **true**
name | false
email | false
password | false
profile | false
text_limit | false


Valid Response:
```
{
    "id": id,
    "name": "Agent Name",
    "photo": "Agent photo url",
    "phone_extension": null,
    "signature": null,
    "new_status": "OFFLINE",
    "department": {
        "name": "Atendimento",
        "id": department_id
    }
}
```
