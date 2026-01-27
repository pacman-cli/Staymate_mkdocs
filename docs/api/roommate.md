# Roommate API

Base URL: `/api/roommates`

## Endpoints

### Create Roommate Post
Create a new roommate finder profile.

-   **URL**: `/`
-   **Method**: `POST`
-   **Auth**: Bearer Token

**Request Body**
```json
{
  "location": "Dhaka",
  "budgetMin": 5000,
  "budgetMax": 10000,
  "moveInDate": "2024-02-01",
  "genderPreference": "MALE",
  "smoking": false,
  "alcohol": false,
  "pets": true,
  "bio": "Software engineer looking for a quiet place."
}
```

### Get Matches
Get AI-scored roommate matches.

-   **URL**: `/matches`
-   **Method**: `GET`
-   **Auth**: Bearer Token

**Response (200 OK)**
```json
[
  {
    "id": 102,
    "matchScore": 85,
    "matchExplanation": "High compatibility due to similar sleep schedule and budget.",
    "user": { "firstName": "Alice" },
    ...
  }
]
```

### Search Posts
Filter posts by criteria.

-   **URL**: `/search`
-   **Method**: `GET`
-   **Params**: `location`, `minBudget`, `maxBudget`, `genderPreference`
