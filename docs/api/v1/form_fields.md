#### Form Fields

Make **GET** HTTP Request:
```
https://zchat.zenvia.io/api/external/form_fields?token={yourAPIToken}
```

| Parameter  | Required  | Description | Default Attributes |
| ------------ | ------------ | ------------ | ------------ |
| token | **true** | Your API token | -|


Response
```
{
  "status": 200,
  "form_fields": [
    {
      "id": 124585,
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
      "id": 124580,
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
    },
    {
      "id": 124586,
      "name": "channel_email",
      "label": "Email",
      "is_required": false,
      "is_unique": true,
      "type": "email",
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
| Field  | Type  |  Description |
| ------------ | ------------ | ------------ |
| id | integer | Unique id |
| name | string | Name of the field |
| label | string | Name of the field that shows on screen |
| is_required | boolean | Required field for creating or updating |
| is_unique | boolean | Unique field, can be used for searching |
| type | string | Field data type |
| is_multiple | boolean | Allows more than one |
| belongs_to_customer | boolean | Customer field |
| belongs_to_collection | boolean | Collection field |
| label_updatable | boolean | Agent can edit label |
| value_updatable | boolean | Agent can edit value |
| showable | boolean | Field shows on screen |

Error Response:
```
{
  "status": 404,
  "message": "Error Message Here"
}
```

