# Customers API
To get the access token, go to:
```
https://zchat-admin.zenvia.com
```
Then go to:
```
Menu > Settings > Integrations > API
```
Click on 'Generate Token' to obtain a new one.
## Create or Update Customers
Make HTTP **POST** Request:
```
https://zchat.zenvia.io/api/external/customers
```
Body Example:

```
{
  "token": "yourApiToken",
  "customers": [
    {
      "fields":{
        "main_identifier": "Customer 1 Name",
        "channel_phone":  "1122334455"
      },
      "agent_id": 1
    },
    {
      "fields":{
        "main_identifier": "Customer 2 Name",
        "channel_email": "customer@email.com"
      },
      "agent_id": 9999
    }
  ]
}
```
| Parameter  | Type  | Required | Description  | Default Attributes  |
| ------------ | ------------ | ------------ | ------------ | ------------ |
| token | string | **true** | Your API token | - |
| customers | array | **true** |  List of customers to create/update | - |
| fields | object | **true** | Customer fields* | - |
| agent_id | integer | **false** | A valid agent id | - |

***Obs**: You can see how to **GET** your customer fields on /docs/api/v1/form_fields.md

Success Response Example:
```
{
  "status": 200,
  "customers": [
    {
      "account_id": 9999,
      "fields": {
        "main_photo": "",
        "channel_email": "",
        "channel_phone": "1122334455",
        "main_identifier": "Customer"
      },
      "id": 1,
      "date_creation": "2020-01-07T00:00:00.000Z",
      "change_date": "2020-01-07T00:00:00.000Z",
      "customer_key": "0000-abcd-efgh-ijkl-1c422e49fdff",
      "active": true,
      "agent_id": 9999
    }
  ],
  "errors": [
    {
      "fields": {
        "main_identifier": "Another Customer",
        "channel_email": "another@customer.com"
      },
      "agent_id": 9999,
      "errors": [
        "field: channel_phone is required",
        "agent_id: 9999 not found"
      ]
    }
  ]
}
```
Response Parameter  | Description |
------------  | -------------
customers | List of customers created/updated
account_id | Your account id
fields | list of fields with the customers' info
id | Customer's id
date_creation | When was the customer created
change_date | When was the customer last changed
customer_key | Customer's unique identification (UUID)
active | Active customer
agent_id | Agent related to that customer
errors | List of customers that had a response error when trying to create/update

