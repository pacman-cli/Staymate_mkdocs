# Amenities API

Base URL: `/api/amenities`

## 🛋 Endpoints

### List All Amenities
Get a categorized list of all available amenities for UI selection.

-   **URL**: `/`
-   **Method**: `GET`
-   **Auth**: Public

**Response**
```json
[
  {
    "id": 1,
    "name": "Wifi",
    "icon": "wifi",
    "category": "ESSENTIALS"
  },
  {
    "id": 2,
    "name": "Pool",
    "icon": "waves",
    "category": "OUTDOOR"
  }
]
```
