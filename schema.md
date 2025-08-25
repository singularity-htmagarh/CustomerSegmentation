# 1. Data Schema (Entities & Relationships)
Core Entities
1.1. Customers (Leads, Contacts, Accounts)
Customer: Holds individual customer info (person or company)
Lead: Potential customer (not yet converted)
Contact: Person associated with an Account
Account: Organization/company

1.2. Activities & Interactions
Activity/Event: Any interaction (call, email, meeting, support ticket)
Opportunity: Potential revenue event (deal, sale, application)
Case/Ticket: Support or service request

1.3. Products & Services
Product: Financial product (loan, card, insurance, etc.)
Subscription/Contract: Ongoing service or agreement

1.4. Channels & Touchpoints
Touchpoint: Specific interaction channel (web, app, call center)
Campaign: Marketing action (email, ad, event)

1.5. Segmentation & Metadata
Segment: Customer segment/group
Journey Stage: Current journey stage (Awareness, Acquisition, etc.)

1.6. Audit & History
ChangeLog: Audit trail of changes

Key Relationships:
- Customer ↔ Account (many-to-many via Contact)
- Customer ↔ Opportunity (one-to-many)
- Customer ↔ Activity (one-to-many)
- Opportunity ↔ Product (many-to-one)
- Customer ↔ Subscription (one-to-many)
- Activity ↔ Touchpoint (one-to-one or many-to-one)
- Customer ↔ Case (one-to-many)
- Customer ↔ Segment (many-to-one)

Customer (customer_id PK, first_name, last_name, dob, gender, email, phone, address, region, created_at, status, segment_id FK, ...)
Account (account_id PK, name, industry, region, created_at, ...)
Contact (contact_id PK, customer_id FK, account_id FK, role, ...)
Lead (lead_id PK, source, customer_id FK, status, created_at, ...)
Opportunity (opportunity_id PK, customer_id FK, account_id FK, product_id FK, stage, amount, expected_close, status, created_at, ...)
Product (product_id PK, name, type, description, ...)
Subscription (subscription_id PK, customer_id FK, product_id FK, start_date, end_date, status, ...)
Activity (activity_id PK, customer_id FK, contact_id FK, type, channel, datetime, notes, campaign_id FK, ...)
Case (case_id PK, customer_id FK, contact_id FK, product_id FK, type, status, opened_at, closed_at, priority, ...)
Campaign (campaign_id PK, name, type, start_date, end_date, ...)
Touchpoint (touchpoint_id PK, activity_id FK, channel, medium, details, ...)
Segment (segment_id PK, name, description, ...)
JourneyStage (journey_stage_id PK, name, description, ...)
ChangeLog (change_id PK, entity_type, entity_id, field_changed, old_value, new_value, changed_by, changed_at)

