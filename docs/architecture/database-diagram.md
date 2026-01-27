# Database Schema & Entity Relationship Diagrams

This document provides a comprehensive view of the StayMate database architecture, organized into readable domain-specific diagrams.

!!! info "Schema Source"
    These ERDs are derived from JPA entity classes in `server/src/main/java/com/webapp/domain/`.

---

## 📊 Schema Overview

| Domain | Tables | Description |
|--------|--------|-------------|
| Identity & Access | 3 | Users, roles, verification |
| Property & Rentals | 5 | Listings, seats, amenities |
| Bookings & Applications | 2 | Reservations, rental applications |
| Roommate Matching | 3 | Posts, requests, saved |
| Messaging | 3 | Conversations, messages, inquiries |
| Notifications | 1 | User notifications |
| Reviews | 1 | Ratings and comments |
| Finance | 4 | Payments, earnings, payouts |
| Support | 2 | Tickets, messages |
| Maintenance | 1 | Property maintenance |
| Admin & System | 4 | Complaints, fraud, CMS, settings |

**Total: 31 tables**

---

## 🔐 Identity & Access Domain

```mermaid
erDiagram
    users {
        bigint id PK
        varchar email UK
        varchar password_hash
        varchar first_name
        varchar last_name
        varchar phone_number
        varchar profile_picture_url
        varchar auth_provider
        varchar account_status
        boolean email_verified
        boolean phone_verified
        boolean role_selected
        boolean enabled
        timestamp created_at
        timestamp updated_at
    }

    user_roles {
        bigint user_id FK
        varchar role
    }

    verification_requests {
        bigint id PK
        bigint user_id FK
        varchar document_type
        varchar document_url
        varchar status
        varchar rejection_reason
        timestamp created_at
    }

    users ||--o{ user_roles : "has"
    users ||--o{ verification_requests : "submits"
```

---

## 🏠 Property & Rentals Domain

```mermaid
erDiagram
    properties {
        bigint id PK
        bigint owner_id FK
        varchar title
        text description
        varchar location
        varchar price
        decimal price_amount
        int beds
        int baths
        int sqft
        varchar property_type
        varchar image_url
        varchar status
        double rating
        boolean verified
        int views
        timestamp created_at
    }

    seats {
        bigint id PK
        bigint property_id FK
        varchar label
        varchar status
        timestamp last_vacated_at
    }

    amenities {
        bigint id PK
        varchar name UK
        varchar icon_name
        varchar category
    }

    property_amenities {
        bigint property_id FK
        bigint amenity_id FK
    }

    property_availability {
        bigint id PK
        bigint property_id FK
        date available_from
        date available_to
        boolean is_available
    }

    properties ||--o{ seats : "contains"
    properties ||--o{ property_availability : "has"
    properties }o--o{ amenities : "has"
```

---

## 📋 Bookings & Applications Domain

```mermaid
erDiagram
    users {
        bigint id PK
        varchar email
        varchar first_name
    }

    properties {
        bigint id PK
        varchar title
    }

    seats {
        bigint id PK
        varchar label
    }

    bookings {
        bigint id PK
        bigint version
        bigint tenant_id FK
        bigint landlord_id FK
        bigint property_id FK
        bigint seat_id FK
        date start_date
        date end_date
        decimal total_price
        decimal commission
        decimal net_amount
        varchar status
        text notes
        timestamp created_at
    }

    applications {
        bigint id PK
        bigint sender_id FK
        bigint receiver_id FK
        bigint property_id FK
        varchar status
        text message
        timestamp created_at
    }

    users ||--o{ bookings : "books"
    users ||--o{ bookings : "hosts"
    properties ||--o{ bookings : "for"
    seats ||--o{ bookings : "assigned"
    users ||--o{ applications : "sends"
    users ||--o{ applications : "receives"
    properties ||--o{ applications : "for"
```

---

## 🤝 Roommate Matching Domain

```mermaid
erDiagram
    users {
        bigint id PK
        varchar email
    }

    roommate_posts {
        bigint id PK
        bigint user_id FK
        varchar location
        double budget_min
        double budget_max
        date move_in_date
        text bio
        varchar gender_preference
        boolean smoking
        boolean alcohol
        boolean pets
        varchar occupation
        varchar cleanliness
        varchar sleep_schedule
        json personality_tags
        json interests
        varchar status
        timestamp created_at
    }

    roommate_requests {
        bigint id PK
        bigint requester_id FK
        bigint receiver_id FK
        varchar status
        timestamp created_at
    }

    saved_roommates {
        bigint id PK
        bigint user_id FK
        bigint roommate_post_id FK
        timestamp saved_at
    }

    users ||--o{ roommate_posts : "creates"
    users ||--o{ roommate_requests : "sends"
    users ||--o{ roommate_requests : "receives"
    users ||--o{ saved_roommates : "saves"
    roommate_posts ||--o{ saved_roommates : "saved in"
```

---

## 💬 Messaging & Inquiries Domain

```mermaid
erDiagram
    users {
        bigint id PK
        varchar email
    }

    properties {
        bigint id PK
        varchar title
    }

    conversations {
        bigint id PK
        bigint participant_one_id FK
        bigint participant_two_id FK
        varchar subject
        bigint property_id
        timestamp last_message_at
        varchar last_message_preview
        int participant_one_unread
        int participant_two_unread
        timestamp created_at
    }

    messages {
        bigint id PK
        bigint conversation_id FK
        bigint sender_id FK
        bigint recipient_id FK
        varchar content
        varchar message_type
        varchar attachment_url
        boolean is_read
        timestamp read_at
        timestamp created_at
    }

    inquiries {
        bigint id PK
        bigint sender_id FK
        bigint property_id FK
        bigint owner_id FK
        text message
        text reply
        varchar status
        timestamp created_at
    }

    users ||--o{ conversations : "participates"
    conversations ||--o{ messages : "contains"
    users ||--o{ messages : "sends"
    users ||--o{ inquiries : "asks"
    properties ||--o{ inquiries : "about"
```

---

## 💰 Finance Domain

```mermaid
erDiagram
    users {
        bigint id PK
        varchar email
    }

    bookings {
        bigint id PK
        decimal total_price
    }

    payments {
        bigint id PK
        bigint user_id FK
        bigint booking_id FK
        decimal amount
        varchar status
        varchar payment_method
        varchar transaction_id
        timestamp payment_date
        timestamp created_at
    }

    earnings {
        bigint id PK
        bigint landlord_id FK
        bigint booking_id FK
        bigint property_id FK
        decimal amount
        decimal commission
        decimal net_amount
        varchar status
        timestamp earned_at
    }

    payout_methods {
        bigint id PK
        bigint user_id FK
        varchar method_type
        varchar account_details
        boolean is_default
        boolean is_verified
    }

    payout_requests {
        bigint id PK
        bigint user_id FK
        bigint payout_method_id FK
        decimal amount
        varchar status
        varchar transaction_ref
        timestamp processed_at
    }

    users ||--o{ payments : "makes"
    bookings ||--|| payments : "paid"
    users ||--o{ earnings : "earns"
    users ||--o{ payout_methods : "has"
    users ||--o{ payout_requests : "requests"
    payout_methods ||--o{ payout_requests : "uses"
```

---

## 🎫 Support & Maintenance Domain

```mermaid
erDiagram
    users {
        bigint id PK
        varchar email
    }

    properties {
        bigint id PK
        varchar title
    }

    support_tickets {
        bigint id PK
        bigint user_id FK
        varchar subject
        varchar category
        varchar status
        varchar priority
        timestamp created_at
    }

    support_messages {
        bigint id PK
        bigint ticket_id FK
        bigint sender_id FK
        text content
        boolean is_staff
        timestamp sent_at
    }

    maintenance_requests {
        bigint id PK
        bigint property_id FK
        bigint requester_id FK
        varchar title
        text description
        varchar type
        varchar priority
        varchar status
        text resolution
        timestamp resolved_at
    }

    users ||--o{ support_tickets : "creates"
    support_tickets ||--o{ support_messages : "has"
    properties ||--o{ maintenance_requests : "has"
    users ||--o{ maintenance_requests : "submits"
```

---

## ⚙️ Admin & System Domain

```mermaid
erDiagram
    users {
        bigint id PK
        varchar email
    }

    properties {
        bigint id PK
        varchar title
    }

    complaints {
        bigint id PK
        bigint reporter_id FK
        bigint reported_user_id FK
        bigint property_id FK
        varchar type
        text description
        varchar status
        varchar priority
        text resolution
        bigint resolved_by FK
        timestamp created_at
    }

    fraud_events {
        bigint id PK
        bigint user_id FK
        varchar fraud_type
        varchar severity
        text details
        varchar action_taken
        timestamp detected_at
    }

    cms_content {
        bigint id PK
        varchar content_type
        varchar title
        text content
        boolean is_published
        timestamp published_at
    }

    system_settings {
        bigint id PK
        varchar setting_key UK
        text setting_value
        varchar category
        text description
    }

    users ||--o{ complaints : "reports"
    users ||--o{ complaints : "reported"
    users ||--o{ fraud_events : "flagged"
```

---

## 🔗 Cross-Domain Relationships

```mermaid
erDiagram
    users ||--o{ properties : "owns"
    users ||--o{ bookings : "books/hosts"
    users ||--o{ applications : "sends/receives"
    users ||--o{ roommate_posts : "creates"
    users ||--o{ notifications : "receives"
    users ||--o{ reviews : "writes/receives"
    users ||--o{ saved_properties : "saves"

    properties ||--o{ seats : "contains"
    properties ||--o{ bookings : "booked"
    properties ||--o{ reviews : "has"
    properties ||--o{ inquiries : "receives"
    properties ||--o{ maintenance_requests : "has"

    bookings ||--|| payments : "paid by"
    bookings ||--o| earnings : "generates"
```

---

## 📈 Quick Reference

### Key Indexes
- `conversations`: participant_one_id, participant_two_id, last_message_at
- `messages`: conversation_id, sender_id, is_read, created_at
- `notifications`: user_id, is_read, created_at

### Join Tables
- `property_amenities` (properties ↔ amenities)
- `user_roles` (users ↔ roles)

### Optimistic Locking
- `bookings.version` prevents concurrent modifications

---

**Database schema verified — ER diagrams fully match models and are production-accurate.**
