# Departments API
To get the access token, go to:
```
https://zchat-admin.zenvia.com
```
Then go to:
```
Menu > Settings > Integrations > API
```
Click on 'Generate Token' to obtain a new one.
## Get Departments
Make HTTP **GET** request:
```
https://zchat.zenvia.io/api/external/departments?token={yourAPIToken}
```
| Parameter  | Required  | Description | Default Attributes |
| ------------ | ------------ | ------------ | ------------ |
| token | **true** | Your API token | - |

<br> Success Response Example:
```
[
  {
    "id": 99999,
    "name": "Atendimento",
    "ringing_max_time": 20,
    "queued_max_time": 120,
    "queue": true,
    "bot_id": null,
    "queue_position_time": null,
    "date_creation": "2020-08-03T20:25:32.684Z",
    "change_date": null,
    "state": 1,
    "agents": [
      {
        "id": 9999,
        "name": "Agent Name",
        "photo": "https://file-address.example.com.com/agent.png"
      }
    ],
    "channels": [
      {
        "id": 9999,
        "name": "CHAT",
        "state": 1
      }
    ]
  }
]
```
Response Parameter  | Description |
------------  | -------------
id | Department id
name | Department Name 
ringing_max_time | Max time an interaction can ring for an agent
queued_max_time | Max time an interaction can ring in a department queue
queue | Department Name 
bot_id | Department Name 
queue_position_time | Department Name 
date_creation | When was the department created 
change_date | When was the department last changed
state | 1 - Active, 0 - Inactive
agents | List of agents from this department
channels | List of channels registered for this department

<br> Error Response:
```
{
  "status": 404,
  "message": "Error Message Here"
}
```