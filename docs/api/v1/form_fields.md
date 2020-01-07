#### Form Fields

Make **GET** HTTP Request:
```
https://services.omnize.com.br/api/v1/form_fields?token={yourClientSdkToken}
```

Parameter | Type | Required | Valid Attributes |
------------ | ------------- | ------------- | -------------
token | string | **true** | your clientSdk token


Response:
Field | Type | Usage |
------------ | ------------- | -------------
id | integer | internal use
name | string | name of field
label | string | label of field that shows on screen
is_required | boolean | required field to create or update
is_unique | boolean | unique field to search
belongs_to_customer | boolean | customer field
belongs_to_collection | boolean | collection field
label_updatable | boolean | agent can edit label
value_updatable | boolean | agent can edit value
showable | boolean | field shows on screen


Response example:
```
{
  "status": 200,
  "form_fields": [
    {
      "id": 124585,
      "name": "main_identifier",
      "label": "Nome",
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
      "label": "Telefone",
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
Error Response:
```
{
  "status": 404,
  "message": "Error Message Here"
}
```

