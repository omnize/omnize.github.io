## Partner API

#### Create Agent
Make HTTP request:

    POST https://zchat.zenvia.io/api/partner/agents

With body:

    {
      token: 'j423j42jn3kj4n',
      profile: 'ADMIN', // 'ADMIN' or 'AGENT'
      agent: {
        email: 'test@example.com', // Email used to login
        name: 'Test Agent',
        password: 'j2hk2j3h4kj23h4kjh2k34', // Plain text signed as SHA256 hash
        text_limit: 7, // optional 
        account_id: 1111
      }
    }

Without parameter profile, will create a AGENT profile

Response, success:

    {
      status: 200,
      success: true,
      data: {
        id: 12153,
        name: "New Agent",
        password: nil,
        administrator: "NAO",
        email: "agent@example.com",
        ativo: 1,
        photo: nil,
        subscriber_id: nil,
        account_id: 3373,
        date_creation: "2017-06-20 20:24:51",
        change_date: "2017-06-20 20:24:51",
        user_creation: nil,
        user_change: nil,
        version_register: 0,
        register_mobile_id: nil,
        photo_expired_date: nil,
        bucket_conf: nil
      }
    }

In case of errors:

    {
      status: 200,
      success: false,
      errors: "Invalid token"
    }

#### Update Agent
Make a HTTP request:

    PUT https://zchat.zenvia.io/api/partner/agents/:id

With body:

    {
      token: 'j423j42jn3kj4n',
      agent: {
        email: 'update@example.com',
        name: 'New Name',
        text_limit: 7, // optional 
        password: 'j2hk2j3h4kj23h4kjh2k34' // Plain text signed as SHA256 hash
      }
    }

Response, success:

    {
      status: 200,
      success: true
    }

In case of errors:

    {
      status: 200,
      success: false,
      errors: "E-mail can be blank"
    }
    

#### Delete Agent
Make HTTP request:

    DELETE https://zchat.zenvia.io/api/partner/agents/:id

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


#### Update Agent Profile
Make a HTTP request:

    PUT https://zchat.zenvia.io/api/partner/agents/:id/profile

With body:

    {
      token: 'j423j42jn3kj4n',
      profile: 'AGENT'
    }

Response, success:

    {
      status: 200,
      success: true
    }

#### Retrieve agents
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
    GET https://zchat.zenvia.io/api/partner/agents?token=hj4h2k3h4k23&account_id=1&search=test@gmail&column=name&direction=asc&page=1&limit=10
```

Response, success:

    {
      status: 200,
      success: true,
      data: [listOfAgents]
    }

In case of errors:

    {
      status: 200,
      success: false,
      errors: "Invalid token"
    }

#### Retrieve accounts
  Accepted params:
  ```
  token: partner_token (required)
  column: order by column (id name email main_contact) default: id
  direction: order by (desc asc) default: desc
  page: pagination of agents (>=1) default: 1
  limit: limit number of return agents default: 20
  search: search by (id name or email)
  ```
  Make HTTP request:
  ```
    GET https://zchat.zenvia.io/api/partner/accounts?token=hj4h2k3h4k23&search=test@gmail&column=name&direction=asc&page=1&limit=10
```
Response, success:

    {
      status: 200,
      success: true,
      data: [{
            "id": 9949,
            "name": "example",
            "email": "example@omnize.com.br",
            "main_contact": "omnize",
            "url": "https://omnize.com.br",
            "user_last_access": "someone",
            "date_creation": "2018-07-30T13:46:16.652Z",
            "change_date": "2018-07-30T13:46:16.652Z",
            "webhook_url": "https://omnize.com.br/webhooks",
            "deleted_at": null,
            "phone": "0000-0000",
            "ativo": 1, // It will be discontinued in future
            "active": true // Boolean
        }, ...]
    }

In case of errors:

    {
      status: 200,
      success: false,
      errors: "Error Message"
    }


#### Create Account
Make HTTP request:

    POST https://zchat.zenvia.io/api/partner/accounts

With body:

    {
      token: 'hj4h2k3h4k23',
      license_quantity: 10,
      password: 'j2hk2j3h4kj23h4kjh2k34', (Optional) // SHA256
      account: {
        email: 'test@example.com',
        main_contact: 'Account Owner Namer',
        telefone: '(11) 9345-0987',
        url: 'testwebpage.com.br'
      }
    }

Response, success:

    {
      status: 200,
      success: true,
      data: {
        id: 4931,
        name: nil,
        razao_social: nil,
        inscricao_estadual: nil,
        cpfcnpj: nil,
        endereco: nil,
        bairro: nil,
        cidade: nil,
        estado: nil,
        telefone: "(11) 98877-6655",
        telefone1: nil,
        email: "test@example.org",
        main_contact: "Test Account",
        iugu_id: nil,
        validate_hash: true,
        subscriber_id: nil,
        domain_id: 4926,
        ativo: 1,
        version_register: 0,
        user_creation: nil,
        date_creation: "2017-06-02 19:24:00",
        user_change: nil,
        change_date: "2017-06-02 19:24:00",
        cep: nil,
        user_last_access: nil,
        date_last_access: nil,
        region_id: 36,
        segment_id: 1,
        url: "www.test.com",
        whatsapp: nil,
        token: nil,
        partner_id: 1,
        facelift: true
      }
    }

In case of errors:

    {
      status: 200,
      success: false,
      errors: "Invalid token"
    }
    
#### Update Account
Make HTTP request:

    PUT https://zchat.zenvia.io/api/partner/accounts/:id

With body:

    {
      token: 'hj4h2k3h4k23',
      account: {
        email: 'test@example.com',
        main_contact: 'Account Owner Namer',
        telefone: '(11) 9345-0987',
        url: 'testwebpage.com.br',
        ativo: 1
      }
    }

Response, success:

    {
      status: 200,
      success: true
    }

In case of errors:

    {
      status: 200,
      success: false,
      errors: "Invalid token"
    }
    

#### Inactive Account
Make HTTP request:

    PUT https://zchat.zenvia.io/api/partner/accounts/:id

With body:

    {
      token: 'hj4h2k3h4k23',
      account: {
        ativo: 0
      }
    }

Response, success:

    {
      status: 200,
      success: true
    }

In case of errors:

    {
      status: 200,
      success: false,
      errors: "Invalid token"
    }

#### Active Account
Make HTTP request:

    PUT https://zchat.zenvia.io/api/partner/accounts/:id

With body:

    {
      token: 'hj4h2k3h4k23',
      account: {
        ativo: 1
      }
    }

Response, success:

    {
      status: 200,
      success: true
    }

In case of errors:

    {
      status: 200,
      success: false,
      errors: "Invalid token"
    }


#### Delete Account
Make HTTP request:

    DELETE https://zchat.zenvia.io/api/partner/accounts/:id

With body:

    {
      token: 'hj4h2k3h4k23'
    }

Response, success:

    {
      status: 200,
      success: true,
      message: "Account deleted successfully"
    }

In case of errors:

    {
      status: 200,
      success: false,
      errors: "Invalid token"
    }

#### Update account licenses
Make HTTP request:

    PUT https://zchat.zenvia.io/api/partner/accounts/:id

With body:

    {
      token: 'hj4h2k3h4k23',
      license_quantity: 5
    }

Response, success:

    {
      status: 200,
      success: true
    }

In case of errors:

    {
      status: 200,
      success: false,
      errors: "Invalid token"
    }

#### Update account licenses code
Make HTTP request:

    PUT https://zchat.zenvia.io/api/partner/accounts/:id

With body:

    {
      token: 'hj4h2k3h4k23',
      license_code: 'PARTNER_X'
    }

Response, success:

    {
      status: 200,
      success: true
    }

In case of errors:

    {
      status: 200,
      success: false,
      errors: "Invalid token"
    }

#### Widget
Widget-code, set proper account_id at 'wOmz.init({id:#{id}})':

    <!-- Início do script Omnize -->
      <script>
        document.addEventListener('DOMContentLoaded',function(){
          var JSLink=location.protocol+'//widget.omnize.com',JSElement=document.createElement('script');
          JSElement.async=!0;
          JSElement.src=JSLink;
          JSElement.onload=OnceLoaded;
          document.getElementsByTagName('body')[0].appendChild(JSElement);
          function OnceLoaded(){
            wOmz.init({id:#{id}});
          }
        },false);
      </script>
    <!-- Fim do script Omnize -->


#### Url login
Make a http request to generate auth_token:

    POST https://ca1vsqktff.execute-api.us-east-1.amazonaws.com/prod/authentication

Body:

    {
      "action": "loginPartner",
      "username":"user@example.org", // Agent email
      "token":"B4cPxMMVteyoqCk6UUsK" // Partner token
    }

Response:

    {
      "message": "",
      "token": "eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVaRp5D0e3",
      "status": 200
    }

Link to login, with returned token:

    https://login.omnize.com.br?token=eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVaRp5D0e3


## Manage Departments
#### Create
Make HTTP request:

    POST https://zchat.zenvia.io/api/partner/departments

With body:

    {
      token: 'hj4h2k3h4k23',
      department: {
        account_id: 1,
        name: "New Department",
        description: "A new created department",
        ativo: 1,
        channels: ["chat","video","audio"]
      }
    }

Response, success:

    {
      status: 200,
      success: true,
      data: [createdObject]
    }

In case of errors:

    {
      status: 200,
      success: false,
      errors: "Invalid token"
    }

#### Update
Make HTTP request:

    PUT https://zchat.zenvia.io/api/partner/departments/:id

With body:

    {
      token: 'hj4h2k3h4k23',
      department: {
        name: "New Department Name",
        description: "New department description",
        ativo: 0
      }
    }

Response, success:

    {
      status: 200,
      success: true,
      data: [updatedObject]
    }

In case of errors:

    {
      status: 200,
      success: false,
      errors: "Invalid token"
    }

#### Retrieve all
Make HTTP request:

    GET https://zchat.zenvia.io/api/partner/departments?token=hj4h2k3h4k23&account_id=1

Response, success:

    {
      status: 200,
      success: true,
      data: [listOfDepartments]
    }

In case of errors:

    {
      status: 200,
      success: false,
      errors: "Invalid token"
    }

#### Retrieve all channels
Make HTTP request:

    GET https://zchat.zenvia.io/api/partner/departments/:id/channels?token=hj4h2k3h4k23

Response, success:

    {
      status: 200,
      success: true,
      data: [listOfChannels]
    }

In case of errors:

    {
      status: 200,
      success: false,
      errors: "Invalid token"
    }

#### Retrieve all agents on a department
Make HTTP request:

    GET https://zchat.zenvia.io/api/partner/departments/:id/agents?token=hj4h2k3h4k23

Response, success:

    {
      status: 200,
      success: true,
      data: [listOfAgents]
    }

In case of errors:

    {
      status: 200,
      success: false,
      errors: "Invalid token"
    }

#### Add agents
Make HTTP request:

    POST https://zchat.zenvia.io/api/partner/departments/:id/add_agents

With body:

    {
      token: "B4cPxMMVteyoqCk6UUsK",
      agents: ["123","456"]
    }

Response, success:

    {
      status: 200,
      success: true,
      data: [listOfAgents]
    }

In case of errors:

    {
      status: 200,
      success: false,
      errors: "Invalid token"
    }

#### Remove agents
Make HTTP request:

    POST https://zchat.zenvia.io/api/partner/departments/:id/remove_agents

With body:

    {
      token: "B4cPxMMVteyoqCk6UUsK",
      agents: ["123","456"]
    }

Response, success:

    {
      status: 200,
      success: true,
      data: [listOfAgents]
    }

In case of errors:

    {
      status: 200,
      success: false,
      errors: "Invalid token"
    }

#### Add channels
Make HTTP request:

    POST https://zchat.zenvia.io/api/partner/departments/:id/add_channels

With body:

    {
      token: "B4cPxMMVteyoqCk6UUsK",
      channels: ["audio"]
    }

Response, success:

    {
      status: 200,
      success: true,
      data: [listOfChannels]
    }

In case of errors:

    {
      status: 200,
      success: false,
      errors: "Invalid token"
    }

#### Remove channels
Make HTTP request:

    POST https://zchat.zenvia.io/api/partner/departments/:id/remove_channels

With body:

    {
      token: "B4cPxMMVteyoqCk6UUsK",
      channels: ["video"]
    }

Response, success:

    {
      status: 200,
      success: true,
      data: [listOfChannels]
    }

In case of errors:

    {
      status: 200,
      success: false,
      errors: "Invalid token"
    }

