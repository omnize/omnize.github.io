#### Customers
Create or Update Customers
Make **POST** HTTP Request:
```
https://zchat.zenvia.io/api/external/customers
```
Body

| Parameter  | Type  | Required   | Valid Attributes  |
| ------------ | ------------ | ------------ | ------------ |
| token | string | **true** | your clientSdk token |
| customers | array | **true** | array of customers with **fields** and **agent_id** |

customers

| Parameter | Type | Required | Valid Attributes |
| ------------ | ------------ | ------------ | ------------ |
| fields | object | **true** | customer fields |
| agent_id | integer | false | valid agent_id |

**Obs**: You can see how to **GET** your customer fields on /docs/api/v1/form_fields.md

Example:
```
{
  "token": "yourClientSdkToken",
  "customers": [
    {
      "fields":{
        "main_identifier": "Customer",
        "channel_phone":  "1122334455"
      },
      "agent_id": 1
    },
    {
      "fields":{
        "main_identifier": "Another Customer",
        "channel_email": "another@customer.com"
      },
      "agent_id": 9999
    }
  ]
}
```

Valid Response:
```
{
  "status": 200,
  "customers": [
    {
      "account_id": 1,
      "fields": {
        "main_photo": "",
        "channel_email": "",
        "channel_phone": "1122334455",
        "main_identifier": "Customer"
      },
      "id": 1,
      "date_creation": "2020-01-07T00:00:00.000Z",
      "change_date": "2020-01-07T00:00:00.000Z",
      "customer_key": "uuid",
      "active": true,
      "agent_id": 1
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

