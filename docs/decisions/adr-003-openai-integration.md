# ADR-003: OpenAI Integration as an Interpretation Layer

## Status

Accepted

## Context

SellerBot needs to understand natural language messages from WhatsApp customers. Traditional rule-based parsing becomes difficult when users write informal, incomplete, or multilingual messages.

## Decision

OpenAI GPT is used as an interpretation layer to extract structured order intent from customer messages.

The AI output is not treated as final business truth. It must be validated by backend services before any order is created or confirmed.

## Consequences

### Benefits

- Better natural language understanding.
- Support for informal messages.
- Easier multilingual support.
- Reduced complexity in handcrafted parsing rules.

### Trade-offs

- External API dependency.
- Token cost.
- Latency considerations.
- Need for prompt versioning.
- Need for deterministic backend validation.

## Security Controls

- No API keys are stored in the repository.
- Prompts are not publicly exposed.
- AI responses are validated before use.
- Product catalog data remains controlled by the backend.
- Final pricing and persistence are deterministic.
