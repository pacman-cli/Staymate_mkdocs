# Finance & Earnings

StayMate includes a ledger-based finance system to handle rent collection, payouts, and platform revenue.

## 💸 Financial Flow

```mermaid
sequenceDiagram
    participant Tenant
    participant Gateway
    participant System
    participant Landlord
    participant Admin

    Tenant->>Gateway: Pay Rent (Credit Card/MFS)
    Gateway-->>System: Webhook (Payment Success)
    System->>System: Ledger: Credit 'Escrow Wallet'
    System->>System: Booking -> CONFIRMED

    Note over System: Money held until Check-in

    System->>System: Ledger: Debit 'Escrow', Credit 'Landlord Wallet'
    System->>System: Ledger: Credit 'Platform Revenue' (Fee)

    Landlord->>System: Request Payout (Bank Transfer)
    System->>Admin: Create Payout Request
    Admin->>System: Approve Request
    System->>Landlord: Mark Payout as SENT
```

## 📊 Landlord Earnings
Landlords can track:
-   **Total Revenue**: Gross earnings before fees.
-   **Pending Payouts**: Funds eligible for withdrawal.
-   **Withdrawn**: Funds already sent to bank.

### Payout Methods
Supported withdrawal channels:
-   **Bank Transfer**: Directly to local bank account.
-   **Mobile Wallet**: bKash, Nagad (BDT).

## 👮 Admin Oversight
Admins have a dedicated **Finance Dashboard** to:
-   View total platform ecosystem value (GMV).
-   Track net platform revenue (Commissions).
-   Approve/Reject landlord payout requests.
-   Process refunds for cancelled bookings.

## 🛠 API Reference
See [Earnings API](../api/earnings.md) for endpoint details.
