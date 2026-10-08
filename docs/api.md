# API

The API is registered in Backstage as the **`auth-api`** entity. See the
**API** tab on this component for the OpenAPI definition. When the service
runs in Development, Swagger UI is also served by the service itself.

## Endpoints

| Method | Path | Purpose |
| --- | --- | --- |
| POST | `/api/Auth/Login` | Email and password → access token and refresh token |
| POST | `/api/Auth/RefreshToken` | Expired access token and refresh token → new pair |
| POST | `/api/Auth/SignOut` | Revoke the user's refresh token |
| POST | `/api/Auth/CreateUser` | Create a user with claims |

### Example: login

```http
POST http://localhost:5000/api/Auth/Login
Content-Type: application/json

{ "Email": "freddie@queen.com", "Password": "p4$$w0rd" }
```

### Calling a protected service

```http
GET http://localhost:5050/api/WeatherForecast
Authorization: Bearer <accessToken>
```

## Authentication

Login, RefreshToken and CreateUser are unauthenticated. Downstream services
validate the bearer token's RS256 signature, issuer (`http://localhost:5000/`),
audience (`http://localhost/`) and `scope` claim.

## Versioning and compatibility

The API is not versioned yet (no `/v1` prefix).
