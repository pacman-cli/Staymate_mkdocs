# User API

Base URL: `/api/users`

## Endpoints

### Get Current Profile
Retrieve the profile of the currently logged-in user.

-   **URL**: `/profile`
-   **Method**: `GET`
-   **Auth**: Bearer Token (Any Role)

### Update Profile
Update personal information.

-   **URL**: `/profile`
-   **Method**: `PUT`
-   **Auth**: Bearer Token (Any Role)

### Delete Account (Self)
Initiate account deletion (Grace Period of 3 days).

-   **URL**: `/profile`
-   **Method**: `DELETE`
-   **Auth**: Bearer Token (Any Role)
-   **Response**: `200 OK`
    ```json
    {
      "message": "Account scheduled for deletion..."
    }
    ```

### Delete User (Admin)
Immediately delete a user account.

-   **URL**: `/{id}`
-   **Method**: `DELETE`
-   **Auth**: Bearer Token (Admin Only)
-   **Response**: `204 No Content`
