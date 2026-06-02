# Prompt Strategy - Redacted Version

SellerBot uses prompt engineering to convert natural language messages into structured order intent.

The real production prompts are private and are not included in this repository.

## Public Strategy

The AI layer is instructed to extract:

- customer intent
- product names
- quantities
- delivery preference
- missing information
- possible ambiguity

## Security Boundary

The AI model does not:

- confirm orders directly
- calculate final prices
- access secrets
- bypass backend validation
- decide business rules
- persist data

All final business decisions are handled by backend services.
