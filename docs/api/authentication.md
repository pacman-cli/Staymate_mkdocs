# Authentication API

Base URL: `/api/auth`

## 🔐 Auth Flow

```mermaid
sequenceDiagram
    participant User
    participant Frontend
    participant AuthController
    participant SecurityFilter
    participant DB

    User->>Frontend: Enter Credentials
    Frontend->>AuthController: POST /login
    AuthController->>DB: Validate Email/Pass
    DB-->>AuthController: Valid User
    AuthController->>AuthController: Generate JWT (Access + Refresh)
    AuthController-->>Frontend: Return { tokens, user }

    Note over Frontend: Store Tokens in Cookie/LocalStorage

    User->>Frontend: Navigate to Dashboard
    Frontend->>SecurityFilter: GET /api/users/me (Bearer Token)
    SecurityFilter->>SecurityFilter: Validate JWT Signature
    SecurityFilter->>AuthController: Set SecurityContext
    AuthController-->>Frontend: Return Protected Data
```

## Endpoints

### Register User
Create a new user account.

-   **URL**: `/register`
-   **Method**: `POST`
-   **Auth**: Public

**Request Body**
```json
{
  "email": "user@example.com",
  "password": "strongpassword123",
  "firstName": "John",
  "lastName": "Doe"
}
```

**Response (201 Created)**
```json
{
  "accessToken": "eyJhbG...",
  "refreshToken": "eyJhbG...",
  "user": { ... }
}
```

### Login
Authenticate headers and receive tokens.

-   **URL**: `/login`
-   **Method**: `POST`
-   **Auth**: Public

**Request Body**
```json
{
  "email": "user@example.com",
  "password": "password"
}
```

### Get Current User
Retrieve the profile of the currently logged-in user.

-   **URL**: `/me`
-   **Method**: `GET`
-   **Auth**: Bearer Token
