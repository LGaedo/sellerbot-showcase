flowchart LR
    subgraph External
        WhatsApp[WhatsApp Customer]
        Twilio[Twilio API]
        OpenAI[OpenAI API]
    end

    subgraph Backend[SellerBot Backend]
        Webhook[FastAPI Webhook Layer]
        OrderFlow[Order Flow Service]
        ProductValidation[Product Validation Service]
        CustomerService[Customer Service]
        AIService[AI Integration Service]
        WhatsAppProvider[WhatsApp Provider Adapter]
        I18N[i18n Message Service]
    end

    subgraph Persistence
        DB[(PostgreSQL)]
    end

    WhatsApp --> Twilio
    Twilio --> Webhook
    Webhook --> OrderFlow
    OrderFlow --> AIService
    AIService --> OpenAI
    OrderFlow --> ProductValidation
    OrderFlow --> CustomerService
    OrderFlow --> I18N
    ProductValidation --> DB
    CustomerService --> DB
    OrderFlow --> DB
    OrderFlow --> WhatsAppProvider
    WhatsAppProvider --> Twilio
