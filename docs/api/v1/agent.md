## Agent Api V1

#### Get Online Agents
 Make **GET** HTTP request:
```
https://core.omnize.com.br/api/v1/agents/online?token={yourClientSdkToken}&department_id={yourDepartmentId}
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