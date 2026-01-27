# 🌍 Environment Variables Reference

This document provides a complete reference of all environment variables used by StayMate.

---

## Overview

StayMate uses environment variables for configuration across all services. Variables can be set:

1. **Root `.env` file** — Used by Docker Compose
2. **Backend `application.properties`** — Spring Boot configuration
3. **Frontend `.env.local`** — Next.js configuration

---

## Database Configuration

| Variable | Default | Required | Description |
|----------|---------|----------|-------------|
| `DB_HOST` | localhost | ✅ | MySQL server hostname |
| `DB_PORT` | 3306 | ✅ | MySQL server port |
| `DB_NAME` | staymate | ✅ | Database name |
| `DB_USERNAME` | root | ✅ | Database username |
| `DB_PASSWORD` | — | ✅ | Database password |

```bash
# Example
DB_HOST=localhost
DB_PORT=3306
DB_NAME=staymate
DB_USERNAME=root
DB_PASSWORD=your_secure_password
```

---

## JWT / Authentication

| Variable | Default | Required | Description |
|----------|---------|----------|-------------|
| `JWT_SECRET` | (dev key) | ✅ Prod | Base64-encoded 256-bit secret |
| `JWT_EXPIRATION_MS` | 3600000 | ❌ | Access token expiry (1 hour) |
| `JWT_REFRESH_EXPIRATION_MS` | 604800000 | ❌ | Refresh token expiry (7 days) |

!!! warning "Generate Secure Secret"
    ```bash
    openssl rand -base64 64
    ```

---

## OAuth2 (Google Login)

| Variable | Default | Required | Description |
|----------|---------|----------|-------------|
| `GOOGLE_CLIENT_ID` | — | ❌ | Google OAuth2 Client ID |
| `GOOGLE_CLIENT_SECRET` | — | ❌ | Google OAuth2 Client Secret |
| `OAUTH2_REDIRECT_URI` | http://localhost:3000/oauth2/redirect | ❌ | Post-login redirect |

Get credentials from [Google Cloud Console](https://console.cloud.google.com/).

---

## MinIO (Object Storage)

| Variable | Default | Required | Description |
|----------|---------|----------|-------------|
| `MINIO_URL` | http://localhost:9005 | ✅ | MinIO API endpoint |
| `MINIO_ACCESS_KEY` | minioadmin | ✅ | MinIO access key |
| `MINIO_SECRET_KEY` | minioadmin | ✅ | MinIO secret key |
| `MINIO_BUCKET_NAME` | staymate-uploads | ✅ | Default bucket name |
| `MINIO_PUBLIC_URL` | http://localhost:9005 | ✅ | Public URL for file access |

---

## Admin Configuration

| Variable | Default | Required | Description |
|----------|---------|----------|-------------|
| `ADMIN_EMAIL` | admin@gmail.com | ❌ | Default admin email |
| `ADMIN_PASSWORD` | admin123 | ❌ | Default admin password |
| `ADMIN_SECRET_KEY` | dev-admin-secret-key | ✅ Prod | Secret for admin endpoints |

!!! danger "Change in Production"
    Always change default admin credentials in production!

---

## CORS Configuration

| Variable | Default | Required | Description |
|----------|---------|----------|-------------|
| `CORS_ALLOWED_ORIGINS` | http://localhost:3000,http://localhost:8080 | ✅ | Comma-separated origins |

---

## Rate Limiting

| Variable | Default | Required | Description |
|----------|---------|----------|-------------|
| `RATE_LIMIT_ENABLED` | false | ❌ | Enable rate limiting |
| `RATE_LIMIT_REQUESTS_PER_MINUTE` | 100 | ❌ | Max requests per minute |

---

## AI Service (Ollama)

| Variable | Default | Required | Description |
|----------|---------|----------|-------------|
| `ai.ollama.url` | http://localhost:11434 | ❌ | Ollama API URL |
| `ai.ollama.model` | llama3.2 | ❌ | Model for AI matching |

---

## Frontend Variables

| Variable | Default | Required | Description |
|----------|---------|----------|-------------|
| `NEXT_PUBLIC_API_URL` | http://localhost:8080 | ✅ | Backend API URL (browser) |
| `BACKEND_URL` | http://localhost:8080 | ✅ | Backend URL (server-side) |

!!! note "NEXT_PUBLIC_ Prefix"
    Variables prefixed with `NEXT_PUBLIC_` are exposed to the browser.

---

## SMS Notifications (Twilio)

| Variable | Default | Required | Description |
|----------|---------|----------|-------------|
| `sms.provider` | console | ❌ | `console` or `twilio` |
| `TWILIO_ACCOUNT_SID` | — | ❌ | Twilio Account SID |
| `TWILIO_AUTH_TOKEN` | — | ❌ | Twilio Auth Token |
| `TWILIO_PHONE_NUMBER` | — | ❌ | Twilio phone number |

---

## Server Configuration

| Variable | Default | Required | Description |
|----------|---------|----------|-------------|
| `SERVER_PORT` | 8080 | ❌ | Backend server port |
| `SPRING_PROFILES_ACTIVE` | — | ❌ | Active Spring profile |

---

## Complete `.env` Template

```bash
# =============================================
# DATABASE
# =============================================
DB_HOST=localhost
DB_PORT=3306
DB_NAME=staymate
DB_USERNAME=root
DB_PASSWORD=your_secure_password

# =============================================
# MINIO (Object Storage)
# =============================================
MINIO_ROOT_USER=minioadmin
MINIO_ROOT_PASSWORD=minioadmin
MINIO_URL=http://localhost:9005
MINIO_PUBLIC_URL=http://localhost:9005
MINIO_BUCKET_NAME=staymate-uploads

# =============================================
# JWT
# =============================================
JWT_SECRET=your_base64_encoded_secret

# =============================================
# OAUTH2 (Optional)
# =============================================
GOOGLE_CLIENT_ID=your_client_id
GOOGLE_CLIENT_SECRET=your_client_secret
OAUTH2_REDIRECT_URI=http://localhost:3000/oauth2/redirect

# =============================================
# ADMIN
# =============================================
ADMIN_EMAIL=admin@gmail.com
ADMIN_PASSWORD=admin123
ADMIN_SECRET_KEY=your_admin_secret

# =============================================
# CORS
# =============================================
CORS_ALLOWED_ORIGINS=http://localhost:3000,http://localhost:8080

# =============================================
# FRONTEND
# =============================================
NEXT_PUBLIC_API_URL=http://localhost:8080
BACKEND_URL=http://localhost:8080

# =============================================
# RATE LIMITING
# =============================================
RATE_LIMIT_ENABLED=false
RATE_LIMIT_REQUESTS_PER_MINUTE=100
```

---

## See Also

- [Local Setup Guide](local-setup.md)
- [Docker Deployment](docker.md)
