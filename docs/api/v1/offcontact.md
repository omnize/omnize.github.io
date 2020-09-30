## Offcontact Api V1
#### Create offcontact
Make **POST** HTTP request:
```
 https://zchat.zenvia.io/core/api/v1/offcontact
```
Body

Parameter | Type | Required | Valid Attributes |
------------ | ------------- | ------------- | -------------
content | string | **true** | any string
content_type | string | false | audio, image, text, video, file, **(null will be saved as text)**
department_id | integer | **true** | any department_id from account
token | string | **true** | your clientSdk token
url | string | false | valid url
customer | object | **true** | { "phone", "cpf", "name", "email" }

Customer Parameter | Type | Required |
------------ | ------------- | -------------
phone | string | false
cpf | string | false
name | string | false
email | string | **true**

Example:
```
    {
    "content": "your offcontact content",
    "content_type": "image",
    "customer": {
        "phone": "1199900999",
        "cpf": "12345678900",
        "name": "Name Surname",
        "email": "customer@omnize.com"
    },
    "department_id": 1,
    "token": "y0ur-Client5DK-t0ken",
    "url": "https://omz-logos.s3.amazonaws.com/logo_omz.png"
    }
```
Valid Response:
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