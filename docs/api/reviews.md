# Reviews API

Base URL: `/api/reviews`

## ⭐ Endpoints

### Create Review
Leave a review for a property after a completed stay.

-   **URL**: `/`
-   **Method**: `POST`
-   **Auth**: `ROLE_USER` (Must have completed booking)

**Request Body**
```json
{
  "propertyId": 12,
  "bookingId": 45,
  "rating": 5,
  "comment": "Amazing stay, very clean!"
}
```

### Get Property Reviews
Fetch all reviews for a specific property.

-   **URL**: `/property/{propertyId}`
-   **Method**: `GET`
-   **Auth**: Public
