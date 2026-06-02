# Core Entities

## Business

Represents a company using SellerBot.

Safe public fields:

- id
- name
- locale
- active status
- created timestamp

Sensitive fields excluded:

- real business phone numbers
- API credentials
- billing data
- internal configuration secrets

---

## Customer

Represents a WhatsApp customer associated with a business.

Safe public fields:

- id
- business_id
- display_name
- phone_number placeholder
- delivery_address placeholder

Sensitive fields excluded:

- real phone numbers
- real addresses
- personal identifiers

---

## Product

Represents an item available in a business catalog.

Safe public fields:

- id
- business_id
- name
- normalized_name
- price
- active status

Sensitive fields excluded:

- supplier data
- internal margins
- private catalog logic

---

## Order

Represents a customer order.

Safe public fields:

- id
- business_id
- customer_id
- status
- delivery_type
- total_amount
- created_at

Sensitive fields excluded:

- real customer references
- operational metadata
- private audit details

---

## OrderItem

Represents a product inside an order.

Safe public fields:

- id
- order_id
- product_id
- quantity
- unit_price
- subtotal
