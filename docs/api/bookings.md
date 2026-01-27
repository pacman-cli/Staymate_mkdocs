# Bookings API

Base URL: `/api/bookings`

## 📅 Endpoints

### Create Booking Request
Tenant requests to book a property.

-   **URL**: `/`
-   **Method**: `POST`
-   **Auth**: `ROLE_USER`

**Request Body**
```json
{
  "propertyId": 12,
  "startDate": "2024-01-01",
  "endDate": "2024-12-31",
  "guests": 2
}
```

### Update Status (Landlord)
Approve or reject a booking request.

-   **URL**: `/{id}/status`
-   **Method**: `PATCH`
-   **Auth**: `ROLE_HOUSE_OWNER`

**Request Body**
```json
{
  "status": "APPROVED" // or REJECTED
}
```

### Get My Bookings
Retrieve booking history for the current user (Tenant or Landlord).

-   **URL**: `/my-bookings`
-   **Method**: `GET`
-   **Auth**: Secured
