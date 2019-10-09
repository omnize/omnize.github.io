## Omnize Agent SDK V1
To get access token access:

    https://app.omnize.com.br

Go to:

    Menu > Settings > Integrations > ClientSDK

Click on 'Generate Token' to obtain a new one.

#### Authenticate user
Make HTTP request:

    POST https://services.omnize.com.br/authentication/login

With body:

    {
      "username": "test@example.org",
      "password": "password12345"
    }

Response:

    {
      "status": "200",
      "token": "......."
    }

## Getting start
#### Import SDK:

    <script src="https://omnizeagentsdk.omnize.com.br/sdk.min.js" type="text/javascript"></script>

####  Insantiate sdk passing agent token:

    const sdk = new OmnizeAgentSDK(token)

## Handlers
#### Register agent success (Online):

    sdk.on('registered', () => {})

#### Register agent failed:

    sdk.on('unauthorized', () => {})

#### Unregister agent success (Offline):

    sdk.on('unregistered', () => {})

#### New message from customer:

    sdk.on('newMessage', ({createdAt, content, interactionHash, contentType, messageId, url}) => {})

#### Agent message received on server:

    sdk.on('receivedMessage', ({messageId, interactionHash, tempId}) => {})

#### Agent message delivered to customer:

    sdk.on('deliveredMessage', ({messageId, interactionHash}) => {})

#### Customer typing:

    sdk.on('typing', (interactionHash) => {})

#### Accepted interaction:

    sdk.on('acceptedInteraction', (interactionHash) => {})

#### Customer cleared input:

    sdk.on('cleared', (interactionHash) => {})

#### Customer finished interaction:

    sdk.on('finishedInteraction', (interactionHash, reason) => {})

#### Cancel interaction to agent (Stop ringing):

    sdk.on('canceled', (interactionHash) => {})

#### Interaction was transferred successfully:

    sdk.on('transferred', (interactionHash) => {})

#### Interaction wasn't transferred:

    sdk.on('transferFailed', (interactionHash, reason = '') => {})

#### Email response sent by agent was delivered:

    sdk.on('mailDelivered', ({messageId, interactionHash, tempId}) => {})

#### Email response sent by agent fail:

    sdk.on('mailFailed', ({messageId, interactionHash, tempId}) => {})

#### New interaction received:

    sdk.on('newInteraction', ({interactionHash, id, customer, department.id, interactionType, externalHistory, currentState, createdAt}) => {})

#### Interaction update:

    sdk.on('updateInteraction', (interaction) => {})

#### When agent register in another session:

    sdk.on('kill', () => {})


## Methods
#### Connect agent to server:

    sdk.connect()

#### Register agent (Online):

    sdk.register()

#### Unregister agent (Offline):

    sdk.unregister()

#### Accept new interaction (Answer), wait for acceptedInteraction to confirm:

    sdk.acceptInteraction(interactionHash)

#### Send agent typing to customer:

    sdk.typing(interactionHash)

#### Send agent cleared to customer:

    sdk.cleared(interactionHash)

#### Send message to customer:

    tempId = sdk.newMessage(content, interactionHash, contentType)

#### Send email message to customer:

    tempId = sdk.sendMailMessage({content, interactionHash, attachments, cc, subject})

#### Transfer interaction to agent:

    sdk.transferToAgent(toAgentId, toDepartmentId, interactionHash)

#### Transfer interaction to department:

    sdk.transferToDepartment(toDepartmentId, interactionHash)

#### Send finish interaction:

    sdk.finishInteraction(interactionHash)

#### Transfer phone interaction to agent:

    sdk.transferPhoneToAgent(interactionHash)
