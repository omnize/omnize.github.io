## Partner API V2

### Retrieve agents
  Accepted params:
  ```
  token: partner_token (required)
  account_id: account_id (required)
  column: order by column (id name email) default: id
  direction: order by (desc asc) default: desc
  page: pagination of agents (>=1) default: 1
  limit: limit number of return agents default: 20
  search: search by (id name or email)
  ```
  Make HTTP request:
 ```
    GET https://zchat.zenvia.io/partner/api/agents?token=hj4h2k3h4k23&account_id=1&search=test@gmail&column=name&direction=asc&page=1&limit=10
```

Response, success:

    {
      "status": 200,
      "success": true,
      "agents": [
        {
          "id": 1,
          "name": "Agent Name",
          "photo": null, // Url
          "phone_extension": null,
          "signature": null,
          "email": "agent@example.com",
          "deleted_at": null,
          "active": true,
          "departments": [
            {
              "id": 1,
              "name": "Atendimento"
            }
          ],
          "status": "OFFLINE",
          "profile": "ADMIN",
          "created_at": null,
          "updated_at": null
        }
      ]
    }

In case of errors:

    {
      status: 200,
      success: false,
      errors: "Invalid token"
    }

### Show agent
  Accepted params:
  ```
  token: partner_token (required)
  account_id: account_id (required)
  ```
  Make HTTP request:
 ```
    GET https://zchat.zenvia.io/partner/api/agents/:id?token=hj4h2k3h4k23&account_id=1
```

Response, success:

    {
      status: 200,
      success: true,
      agent: { 
        "id": 1,
        "name": "Agent Name",
        "photo": null, // Url
        "phone_extension": null,
        "signature": null,
        "email": "agent@example.com",
        "deleted_at": null,
        "active": true,
        "departments": [
          {
            "id": 1,
            "name": "Atendimento"
          }
        ],
        "status": "OFFLINE",
        "profile": "ADMIN",
        "created_at": null,
        "updated_at": null
      }
    }

In case of errors:

    {
      status: 200,
      success: false,
      errors: "Invalid token"
    }


### Create Agent
Make HTTP request:

    POST https://zchat.zenvia.io/partner/api/agents

With body:

    {
      token: 'j423j42jn3kj4n',
      profile: 'ADMIN', // 'ADMIN' or 'AGENT'
      department_ids: [1,22,333]
      agent: {
        email: 'test@example.com', // Email used to login
        name: 'Test Agent',
        password: 'j2hk2j3h4kj23h4kjh2k34', // Plain text signed as SHA256 hash
        text_limit: 7, // optional 
        account_id: 1111
      }
    }

Without parameter profile, will create a AGENT profile
Without parameter department_ids, will add agent to first account department

Response, success:

    {
      status: 200,
      success: true,
      agent: {
        "id": 1,
        "name": "Agent Name",
        "photo": null,
        "phone_extension": null,
        "signature": null,
        "email": "agent@example.com",
        "deleted_at": null,
        "active": true,
        "departments": [
          {
            "id": 1,
            "name": "Atendimento"
          }
        ],
        "status": "OFFLINE",
        "profile": "ADMIN",
        "created_at": "2020-10-21T12:46:12.648Z",
        "updated_at": "2020-10-21T12:46:12.648Z"
      }
    }

In case of errors:

    {
      status: 200,
      success: false,
      errors: "Invalid token"
    }

### Update Agent
Make a HTTP request:

    PUT https://zchat.zenvia.io/partner/api/agents/:id

With body:

    {
      token: 'j423j42jn3kj4n',
      profile: 'ADMIN', // 'ADMIN' or 'AGENT'
      agent: {
        account_id: 1111,
        email: 'update@example.com',
        name: 'New Name',
        text_limit: 7, // optional 
        password: 'j2hk2j3h4kj23h4kjh2k34' // Plain text signed as SHA256 hash,
        active: true  
      }
    }

Response, success:

    {
      status: 200,
      success: true,
      agent: {
        "id": 1,
        "name": "Agent Name",
        "photo": null,
        "phone_extension": null,
        "signature": null,
        "email": "agent@example.com",
        "deleted_at": null,
        "active": true,
        "departments": [
          {
            "id": 1,
            "name": "Atendimento"
          }
        ],
        "status": "OFFLINE",
        "profile": "ADMIN",
        "created_at": "2020-10-21T12:46:12.648Z",
        "updated_at": "2020-10-21T12:46:12.648Z"
      }
    }

In case of errors:

    {
      status: 200,
      success: false,
      errors: "E-mail can be blank"
    }
    

### Delete Agent
Make HTTP request:

    DELETE https://zchat.zenvia.io/partner/api/agents/:id

With body:

    {
      token: 'hj4h2k3h4k23'
    }

Response, success:

    {
      status: 200,
      success: true,
      message: "Agent deleted successfully"
    }

In case of errors:

    {
      status: 200,
      success: false,
      errors: "Invalid token"
    }

## Manage Departments

### Retrieve all

  Accepted params:
  ```
  token: partner_token (required)
  account_id: account_id (required)
  column: order by column (id name email) default: id
  direction: order by (desc asc) default: desc
  page: pagination of agents (>=1) default: 1
  limit: limit number of return agents default: 20
  search: search by (id or name)
  ```

Make HTTP request:

    GET https://zchat.zenvia.io/partner/api/departments?token=hj4h2k3h4k23&account_id=1

Response, success:

    {
      status: 200
      departments: [
        {
          "active": true,
          "description": "Atendimento",
          "id": 1,
          "name": "Atendimento",
          "queue": true,
          "queued_max_time": 120,
          "ringing_max_time": 20,
          "queue_position_time": null,
          "deleted_at": null,
          "agents": 2,
          "created_at": null,
          "updated_at": "2018-01-04T19:28:41.000Z",
          "channels": [
            {
              "id": 3,
              "name": "VOICE",
              "state": 1
            },
            {
              "id": 2,
              "name": "VIDEO",
              "state": 1
            },
            {
              "id": 1,
              "name": "CHAT",
              "state": 1
            }
          ]
        }
      ]
    }

In case of errors:

    {
      status: 200,
      success: false,
      errors: "Invalid token"
    }


### Create
Make HTTP request:

    POST https://zchat.zenvia.io/partner/api/departments

With body:

    {
      token: 'hj4h2k3h4k23',
      agent_ids: [1,22,33],
      channels: ["chat"],
      department: {
        account_id: 1,
        name: "New Department",
        description: "A new created department"
      }
    }

Response, success:

    {
      "status": 200,
      "success": true,
      "department": {
        "active": true,
        "description": "Department description",
        "id": 1,
        "name": "Atendimento",
        "queue": true,
        "queued_max_time": 120,
        "ringing_max_time": 20,
        "queue_position_time": null,
        "deleted_at": null,
        "agents": 0,
        "created_at": "2020-10-21T12:56:09.672Z",
        "updated_at": "2020-10-21T12:56:09.672Z",
        "channels": []
      }
    }

In case of errors:

    {
      status: 200,
      success: false,
      errors: "Invalid token"
    }

### Update
Make HTTP request:

    PUT https://zchat.zenvia.io/partner/api/departments/:id

With body:

    {
      token: 'hj4h2k3h4k23',
      agent_ids: [1,22,33],
      channels: ["chat"],
      department: {
        account_id: 1,
        name: "New Name",
        description: "A new description"
      }
    }

Response, success:

    {
      status: 200,
      success: true,
      department: {
        "active": true,
        "description": "A new description",
        "id": 1,
        "name": "New Name",
        "queue": true,
        "queued_max_time": 120,
        "ringing_max_time": 20,
        "queue_position_time": null,
        "deleted_at": null,
        "agents": 0,
        "created_at": "2020-10-21T12:56:09.672Z",
        "updated_at": "2020-10-21T12:56:09.672Z",
        "channels": []
      }
    }

In case of errors:

    {
      status: 200,
      success: false,
      errors: "Invalid token"
    }

