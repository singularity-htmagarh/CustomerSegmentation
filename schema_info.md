# 1. Data Schema (Entities & Relationships)
Core Entities

Customers (Leads, Contacts, Accounts)
Customer: Holds individual customer info (person or company)
Lead: Potential customer (not yet converted)
Contact: Person associated with an Account
Account: Organization/company

Activities & Interactions
Activity/Event: Any interaction (call, email, meeting, support ticket)
Opportunity: Potential revenue event (deal, sale, application)
Case/Ticket: Support or service request

Products & Services
Product: Financial product (loan, card, insurance, etc.)
Subscription/Contract: Ongoing service or agreement

Channels & Touchpoints
Touchpoint: Specific interaction channel (web, app, call center)
Campaign: Marketing action (email, ad, event)

1.5. Segmentation & Metadata
Segment: Customer segment/group
Journey Stage: Current journey stage (Awareness, Acquisition, etc.)

1.6. Audit & History
ChangeLog: Audit trail of changes

Key Relationships:
- Customer ↔ Account (many-to-many via Contact)
   - Customer (customer_id PK, first_name, last_name, dob, gender, email, phone, address, region, created_at, status, segment_id FK, ...)
   - Account (account_id PK, name, industry, region, created_at, ...)
   - Contact (contact_id PK, customer_id FK, account_id FK, role, ...)
   - Lead (lead_id PK, source, customer_id FK, status, created_at, ...)

- Customer ↔ Opportunity (one-to-many)
   - Opportunity (opportunity_id PK, customer_id FK, account_id FK, product_id FK, stage, amount, expected_close, status, created_at, ...)

- Customer ↔ Activity (one-to-many)
   - Activity (activity_id PK, customer_id FK, contact_id FK, type, channel, datetime, notes, campaign_id FK, ...)

- Opportunity ↔ Product (many-to-one)
   - Product (product_id PK, name, type, description, ...)
   - ChangeLog (change_id PK, entity_type, entity_id, field_changed, old_value, new_value, changed_by, changed_at)

- Customer ↔ Subscription (one-to-many)
  - Subscription (subscription_id PK, customer_id FK, product_id FK, start_date, end_date, status, ...)

- Activity ↔ Touchpoint (one-to-one or many-to-one)
  - Campaign (campaign_id PK, name, type, start_date, end_date, ...)
  - JourneyStage (journey_stage_id PK, name, description, ...)
  - Touchpoint (touchpoint_id PK, activity_id FK, channel, medium, details, ...)

- Customer ↔ Case (one-to-many)
  - Case (case_id PK, customer_id FK, contact_id FK, product_id FK, type, status, opened_at, closed_at, priority, ...)

- Customer ↔ Segment (many-to-one)
  - Segment (segment_id PK, name, description, ...)


