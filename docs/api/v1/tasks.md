## Import Tasks

Make **POST** HTTP Request:
```
https://zchat.zenvia.io/api/external/tasks
```
#### Body parameters
Parameter  | Required | Description
------------  | ------------  | -------------
token | **true** | Account ClientSDK token
tasks | **true** | List of tasks

#### Tasks parameters
Parameter  | Required | Description
------------  | ------------  | -------------
task | **true** | Task data
customer | **true** | Customer data
agents | **true** | List of emails

#### Task parameters
Parameter  | Required | Description
------------  | ------------  | -------------
id | **true** | 
name | **true** | 
description |  | 
expires_at | | Date of expiration, utc, format: '2020-01-01 00:00:00'

#### Customer parameters
Parameter  | Required | Description
------------  | ------------  | -------------
id | **true** | Id from external system, used to create/update.
name | | 
emails | | List of emails
phones | | List of phones
document |  | 

Request body example:
```
{
    "token": "account_token",
    "tasks": [
        {
            "task": {
                "name": "Task 123",
                "description": "Task description",
                "id": "xpto123",
                "expires_at": "2020-03-01 10:00:00"
            },
            "customer": {
                "id": "xpto123",
                "name": "Test User",
                "emails": [
                    "test_user@example.com"
                ],
                "phones": [
                    "5511988776655"
                ],
                "document": "12345678900"
            },
            "agents": [
                "test_user@example.com"
            ]
        }
    ]
}
```


Valid Response:
```
{
    "status": 200
}
```

Invalid agents response:
```
{
    "status": 500,
    "errors": [
        "Agents not found with email = '[\"test_user@example.com\", \"test_user2@example.com\"]'"
    ]
}
```
