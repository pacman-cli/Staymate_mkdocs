# Earnings API

Base URL: `/api/finance`

## 💰 Endpoints

### Get Earnings Overview
Retrieve total revenue, pending payouts, and monthly breakdown.

-   **URL**: `/stats`
-   **Method**: `GET`
-   **Auth**: `ROLE_HOUSE_OWNER`

**Response**
```json
{
  "totalRevenue": 150000.00,
  "pendingPayout": 25000.00,
  "monthlyStats": [
    { "month": "JAN", "amount": 50000 },
    { "month": "FEB", "amount": 52000 }
  ]
}
```

### Request Payout
Withdraw available balance to bank account.

-   **URL**: `/payout`
-   **Method**: `POST`
-   **Auth**: `ROLE_HOUSE_OWNER`

**Request Body**
```json
{
  "amount": 25000,
  "bankAccountId": 99
}
```
