# Properties API

Base URL: `/api/properties`

## 🏠 Endpoints

### Create Property
List a new property for rent.

-   **URL**: `/`
-   **Method**: `POST`
-   **Auth**: `ROLE_HOUSE_OWNER`

**Request Body**
```json
{
  "title": "Luxury Apartment in Gulshan",
  "description": "3 Bedroom, fully furnished...",
  "price": 25000,
  "location": "Gulshan 2, Dhaka",
  "beds": 3,
  "baths": 2,
  "amenityIds": [1, 4, 8]
}
```

### Search Properties
Filter listings by various criteria.

-   **URL**: `/search`
-   **Method**: `GET`
-   **Auth**: Public

**Query Parameters**
-   `location`: (string) City or area
-   `minPrice`: (number) Minimum rent
-   `maxPrice`: (number) Maximum rent
-   `beds`: (number) Minimum beds

### Get Property Details
Retrieve full details including reviews and owner info.

-   **URL**: `/{id}`
-   **Method**: `GET`
-   **Auth**: Public
