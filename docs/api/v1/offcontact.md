# Offcontact Api
To get the access token, go to:
```
https://zchat-admin.zenvia.com
```
Then go to:
```
Menu > Settings > Integrations > API
```
Click on 'Generate Token' to obtain a new one.
## Create offcontact
Make HTTP **POST** request:
```
 https://zchat.zenvia.io/core/api/v1/offcontact
```
Body Example:
```
    {
    "content": "offcontact message",
    "content_type": "image",
    "customer": {
        "phone": "1199900999",
        "cpf": "12345678900",
        "name": "Name Surname",
        "email": "customer@email.com"
    },
    "department_id": 1,
    "token": "yourApiToken",
    "url": "https://file-address.example.com/logo.png"
    }
```

Parameter | Type | Required | Description | Default Attributes |
------------ | ------------- | ------------- | ------------- | -------------
content | string | **true** | Offcontact message content | - |
content_type | string | **false** | Type of the content | audio, image, text, video, file, **(null will be saved as text)** |
department_id | integer | **true** | Id of an active department | - |
token | string | **true** | Your API token | - |
url | string | **false** |  File URL (except for "text" type message) | - | 
customer | object | **true** | Customer's information | { "phone", "cpf", "name", "email" }
phone | string | **false** | Customer's telephone number | - |
cpf | string | **false** | Customer's document number | - |
name | string | **false** | Customer's name | - |
email | string | **true** | Customer's email | - |

<br> Success Response Example:
```
{
    "message": "Offcontact sent",
    "interaction_hash": "a126d8d3-ce3f-4448-ade0-954c6a297134",
    "status": 200
{
```
Error Response:
```
{
    "message": "Error description here",
    "status": 422
{
```