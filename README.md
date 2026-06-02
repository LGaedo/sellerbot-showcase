# sellerbot-showcase
AI-powered WhatsApp ordering assistant — architecture, backend design, cloud readiness and system documentation.


This repository is a documentation and architecture showcase only. It does not include production source code, private prompts, credentials, customer data, or proprietary business logic.



# SellerBot Showcase

## AI-Powered WhatsApp Ordering Assistant

SellerBot is a conversational commerce assistant designed to automate product ordering workflows through WhatsApp.

This repository is a public architecture and documentation showcase. It does not contain production source code, private prompts, credentials, tokens, customer data, or proprietary business logic.

The goal of this project is to demonstrate backend engineering, cloud-oriented architecture, AI integration, database modeling, and technical leadership applied to a real-world commerce automation use case.

---

## Project Overview

SellerBot helps small and medium businesses receive, validate, and manage customer orders through WhatsApp.

The system interprets natural language messages, validates requested products against a business catalog, prepares an order preview, asks for missing delivery information when required, and persists confirmed orders in PostgreSQL.

The productive implementation is private. This repository documents the architecture, functional flows, design decisions, integration strategy, and scalability model.

---

## Business Problem

Many small businesses receive customer orders through WhatsApp manually. This creates operational problems:

- Slow response times.
- Human errors when interpreting orders.
- Missed messages during peak hours.
- Lack of structured order history.
- No standardized validation against the product catalog.
- Difficulty scaling operations across multiple businesses.

SellerBot addresses this by turning WhatsApp conversations into structured, validated, and traceable orders.

---

## Core Capabilities

- WhatsApp-based order intake.
- Natural language order understanding.
- Product validation against a business catalog.
- Suggested products for ambiguous or invalid requests.
- Order preview before confirmation.
- Delivery or pickup flow handling.
- Address reuse when customer data already exists.
- Multi-business support.
- Internationalization support.
- PostgreSQL persistence.
- AI-assisted parsing and reasoning.
- Cloud-ready deployment architecture.

---

## Technology Stack

| Area | Technology |
|---|---|
| Backend | Python, FastAPI |
| ORM | SQLAlchemy |
| Database | PostgreSQL |
| Messaging | Twilio WhatsApp API |
| AI Integration | OpenAI GPT |
| Infrastructure Target | AWS EC2, Aurora PostgreSQL |
| Containerization | Docker |
| Architecture Style | Modular backend, service-oriented application layer |
| Internationalization | Centralized i18n message system |

---

## High-Level Architecture

mermaid flowchart LR     Customer[Customer on WhatsApp]     Twilio[Twilio WhatsApp API]     API[FastAPI Webhook API]     Orchestrator[Order Flow Orchestrator]     AI[OpenAI GPT Integration]     Catalog[Product Catalog Service]     Orders[Order Management Service]     DB[(PostgreSQL)]     Business[Business Operator]      Customer --> Twilio     Twilio --> API     API --> Orchestrator     Orchestrator --> AI     Orchestrator --> Catalog     Orchestrator --> Orders     Catalog --> DB     Orders --> DB     Orders --> Business     API --> Twilio     Twilio --> Customer 

---

## Functional Flow

mermaid sequenceDiagram     participant Customer     participant WhatsApp as WhatsApp / Twilio     participant API as FastAPI Webhook     participant Flow as Order Flow Service     participant AI as OpenAI Integration     participant Catalog as Product Catalog     participant DB as PostgreSQL      Customer->>WhatsApp: Sends natural language order     WhatsApp->>API: Delivers webhook event     API->>Flow: Starts order analysis     Flow->>AI: Extracts structured order intent     AI-->>Flow: Returns parsed products and metadata     Flow->>Catalog: Validates products     Catalog->>DB: Queries business catalog     DB-->>Catalog: Returns matching products     Catalog-->>Flow: Valid, invalid and suggested products     Flow-->>Customer: Sends order preview     Customer->>WhatsApp: Confirms order     WhatsApp->>API: Sends confirmation webhook     API->>Flow: Confirms order     Flow->>DB: Persists order     Flow-->>Customer: Sends confirmation message 

---

## Data Model Overview

mermaid erDiagram     BUSINESS ||--o{ CUSTOMER : owns     BUSINESS ||--o{ PRODUCT : offers     BUSINESS ||--o{ ORDER : receives     CUSTOMER ||--o{ ORDER : places     ORDER ||--o{ ORDER_ITEM : contains     PRODUCT ||--o{ ORDER_ITEM : references      BUSINESS {         uuid id         string name         string locale         boolean active     }      CUSTOMER {         uuid id         uuid business_id         string phone_number         string display_name         string delivery_address     }      PRODUCT {         uuid id         uuid business_id         string name         string normalized_name         decimal price         boolean active     }      ORDER {         uuid id         uuid business_id         uuid customer_id         string status         string delivery_type         decimal total_amount         datetime created_at     }      ORDER_ITEM {         uuid id         uuid order_id         uuid product_id         integer quantity         decimal unit_price         decimal subtotal     } 

---

## Example Use Case

### Customer Message

text Hi, I want 2 cheesecakes, 1 coffee and delivery please. 

### System Interpretation

json {   "intent": "create_order",   "delivery_type": "delivery",   "products": [     {       "name": "cheesecake",       "quantity": 2     },     {       "name": "coffee",       "quantity": 1     }   ] } 

### Order Preview

text Here is your order preview:  - 2x Cheesecake - 1x Coffee  Delivery type: Delivery Delivery address: We will use your saved address.  Please confirm if everything is correct. 

---

## AI Integration Strategy

SellerBot uses AI as an interpretation layer, not as the source of truth.

The AI model helps extract structured intent from natural language messages. However, product validation, pricing, business rules, customer data, and order persistence are handled by deterministic backend services.

This design prevents the AI layer from making unauthorized business decisions.

### Responsibilities of the AI Layer

- Interpret customer intent.
- Extract product names and quantities.
- Detect missing information.
- Assist with natural language understanding.
- Support multilingual conversations.

### Responsibilities of the Backend

- Validate products.
- Apply catalog rules.
- Calculate prices.
- Manage order state.
- Persist data.
- Enforce tenant isolation.
- Handle security boundaries.
- Send official customer-facing responses.

---

## WhatsApp Integration Strategy

SellerBot integrates with WhatsApp through Twilio.

Twilio receives customer messages and forwards them to a FastAPI webhook. The backend processes the message, updates the order flow, and sends a response back through the WhatsApp provider abstraction.

This design allows the messaging provider to be replaced in the future without rewriting the business logic.

---

## Multi-Business Design

SellerBot is designed to support multiple businesses from the same backend.

Each business can have:

- Its own product catalog.
- Its own customers.
- Its own orders.
- Its own language configuration.
- Its own WhatsApp configuration.
- Its own message templates.

Tenant isolation is enforced at the application and database query level through the business identifier.

---

## Security and Privacy

This public repository intentionally excludes:

- Production source code.
- Private prompts.
- API keys.
- OpenAI tokens.
- Twilio credentials.
- Database credentials.
- Customer phone numbers.
- Business-sensitive data.
- Internal deployment scripts.
- Proprietary matching logic.

All examples are synthetic and designed for demonstration purposes only.

---

## Architecture Decisions

Key technical decisions documented in this repository:

- FastAPI was selected for Python-based API development.
- SQLAlchemy was selected to maintain ORM-based persistence and database portability.
- PostgreSQL was selected as the primary relational database.
- OpenAI GPT was integrated as a controlled AI interpretation layer.
- Twilio was used as the initial WhatsApp provider.
- AWS EC2 and Aurora PostgreSQL were selected as the initial production-ready cloud target.
- Docker was used to improve local reproducibility and deployment consistency.

---

## Scalability Considerations

The architecture is designed to evolve from a simple MVP deployment into a scalable production system.

### Initial MVP

- Single FastAPI backend.
- PostgreSQL database.
- Twilio WhatsApp integration.
- OpenAI integration.
- Docker-based deployment.
- AWS EC2 hosting.

### Growth Stage

- Aurora PostgreSQL.
- Background workers for async processing.
- Redis for caching and temporary flow state.
- Centralized observability.
- Queue-based message processing.
- Horizontal backend scaling.

### Advanced Stage

- Multi-tenant administration panel.
- Provider-agnostic WhatsApp integration.
- Event-driven order processing.
- Analytics dashboard.
- Business onboarding automation.
- AI evaluation and prompt versioning.

---

## Engineering Highlights

This project demonstrates:

- Backend service design.
- Domain-oriented modeling.
- API webhook processing.
- AI integration with deterministic validation.
- SQLAlchemy ORM modeling.
- PostgreSQL persistence.
- Multi-tenant architecture.
- WhatsApp automation.
- Cloud deployment planning.
- Security-aware public documentation.
- Technical communication for stakeholders.

---

## Target Roles

This project is relevant for:

- Backend Developer roles.
- Python Developer roles.
- Cloud Engineer roles.
- AI Integration Engineer roles.
- Solution Architect roles.
- Technical Lead roles.
- Conversational Commerce roles.
- Automation Engineer roles.

---

## Repository Scope

This repository is not intended to be executed as a production system.

It is a public technical showcase that documents how the system works, why the architecture was designed this way, and how it can scale.

The private production repository contains the actual implementation.
