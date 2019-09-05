# External bot
To activate external bot contact suport

## For homolog environment

    Omnize platform: https://homolog.app.omnize.com.br

    Api endpoint: https://homolog.core.omnize.com.br
    
    Widget: https://omnize.github.io/wgt-homolog.html#:account_id

## Make interaction
#### Start widget, select a department with bot and click on "Chat"
Will receive a POST on endpoint with body:

    {
      "type": "new_interaction",
      "interaction_hash": ".......",
      "department_id": 0000
    }
    
#### To accept make HTTP request:

    PUT https://core.omnize.com.br/api/v1/bot/:interaction_hash/accept

With body:

    {
      "token": "j23hk4j2h3kj4h..."
    }

Response:

    {
      "message": "Message received successfully",
      "status": 200
    }
    
#### To finish make HTTP request:

    PUT https://core.omnize.com.br/api/v1/bot/:interaction_hash/finish

With body:

    {
      "token": "j23hk4j2h3kj4h..."
    }

Response:

    {
      "message": "Message received successfully",
      "status": 200
    }
    
#### To transfer to department make HTTP request:

    PUT https://core.omnize.com.br/api/v1/bot/:interaction_hash/transfer

With body:

    {
      "token": "j23hk4j2h3kj4h..."
    }

Response:

    {
      "message": "Message received successfully",
      "status": 200
    }

#### To send message make HTTP request:

    POST https://core.omnize.com.br/api/v1/bot/:interaction_hash/message

With body:

    {
      "token": "j23hk4j2h3kj4h...",
      "content": "Message",
      "content_type": "text", // "image/jpeg", "image/png", "video/mp4", "audio/ogg"
      "attachment": { // If content_type different of text
        "url": "https://images.com/image.png",
        "size": "1.0MB" //Optional
      }
    }

Response:

    {
      "message": "Message received successfully",
      "status": 200
    }

#### When client send a message
Will receive a POST on endpoint with body:

    {
      "type": "new_message",
      "interaction_hash": ".......",
      "content": "Test message",
      "content_type": "text"
    }

#### When client finishes the interaction
Will receive a POST on endpoint with body:

    {
      "type": "finished_interaction",
      "interaction_hash": "......."
    }
