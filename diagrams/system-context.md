flowchart TD
    Customer[Customer]
    Business[Business Owner / Operator]
    SellerBot[SellerBot Platform]
    Twilio[Twilio WhatsApp API]
    OpenAI[OpenAI GPT API]
    PostgreSQL[(PostgreSQL Database)]
    AWS[AWS Infrastructure]

    Customer -->|Sends orders via WhatsApp| Twilio
    Twilio -->|Webhook events| SellerBot
    SellerBot -->|AI-assisted interpretation| OpenAI
    SellerBot -->|Stores orders, customers, products| PostgreSQL
    SellerBot -->|Sends replies| Twilio
    Business -->|Manages catalog and receives orders| SellerBot
    SellerBot -->|Deployable on| AWS
