# Security Roles & Permissions

StayMate uses **Role-Based Access Control (RBAC)** enforced by Spring Security.

## 🎭 User Roles

| Role | Database Value | Description |
|------|----------------|-------------|
| **Guest** | `ROLE_GUEST` | Unauthenticated users. Can search but not view details. |
| **Tenant** | `ROLE_USER` | Standard user seeking rentals. Can book and message. |
| **Landlord** | `ROLE_HOUSE_OWNER` | Property owner. Can list properties and view earnings. |
| **Admin** | `ROLE_ADMIN` | Platform administrator. Can ban users and verify IDs. |

## 🔐 Implementation Details

-   **Annotations**: We use `@PreAuthorize("hasRole('ADMIN')")` on Controllers.
-   **Database**: Roles are stored in the `roles` table and linked via `user_roles`.
-   **JWT Claims**: The `roles` claim in the Access Token determines access.

## 🛡 Protected Resources

-   **Admin Only**:
    -   `/api/admin/**`
    -   `/api/users/ban/**`
    -   `/api/properties/verify/**`
-   **Landlord Only**:
    -   `/api/properties` (POST/PUT/DELETE)
    -   `/api/dashboard/landlord`
-   **Authenticated**:
    -   `/api/users/me`
    -   `/api/bookings`
