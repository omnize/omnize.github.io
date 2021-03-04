# Form Fields API
To get the access token, go to:
```
https://zchat-admin.zenvia.com
```
Then go to:
```
Menu > Settings > Integrations > API
```
Click on 'Generate Token' to obtain a new one.
## List Form Fields
Make HTTP **GET** Request:
```
https://zchat.zenvia.io/api/external/form_fields?token={yourAPIToken}
```

| Parameter  | Required  | Description | Default Attributes |
| ------------ | ------------ | ------------ | ------------ |
| token | **true** | Your API token | - |

Success Response Example:
```
{
  "status": 200,
  "form_fields": [
    {
      "id": 9999,
      "name": "main_identifier",
      "label": "Name",
      "is_required": true,
      "is_unique": false,
      "type": "string",
      "is_multiple": false,
      "belongs_to_customer": true,
      "belongs_to_collection": false,
      "label_updatable": true,
      "value_updatable": true,
      "showable": true
    },
    {
      "id": 8888,
      "name": "channel_phone",
      "label": "Telephone",
      "is_required": true,
      "is_unique": true,
      "type": "phone",
      "is_multiple": true,
      "belongs_to_customer": true,
      "belongs_to_collection": false,
      "label_updatable": true,
      "value_updatable": true,
      "showable": true
    }
  ]
}
```
| Response Parameter   |  Description |
| ------------ | ------------ |
| id | Unique id |
| name | Name of the field |
| label | Name of the field that shows on screen |
| is_required | Required field for creating or updating |
| is_unique | Unique field, can be used for searching |
| type | Field data type |
| is_multiple | Allows more than one |
| belongs_to_customer | Customer field |
| belongs_to_collection | Collection field |
| label_updatable | Agent can edit label |
| value_updatable | Agent can edit value |
| showable | Field shows on screen |

<br> Error Response:
```
{
  "status": 404,
  "message": "Error Message Here"
}
```

