# Auth Microservice

Authentication and authorization microservice built with .NET and Clean
Architecture. It authenticates users, issues **RS256-signed JWT access tokens**
with **refresh tokens**, and lets other services authorize requests by
validating those tokens with the public key.

| | |
| --- | --- |
| **Owner** | `group:platform-engineering` |
| **System** | `infrastructure` |
| **Lifecycle** | `experimental` |
| **Repository** | [MinaEmadMF/dotnet-auth-microservice](https://github.com/MinaEmadMF/dotnet-auth-microservice) |
| **Design article** | [Auth microservice with Clean Architecture](https://veglos.github.io/posts/dotnet-auth-microservice-with-clean-architecture/) |

## What it does

- **Login**: validates email and password and returns an access token and a
  refresh token.
- **Refresh token**: exchanges an expired access token plus a valid refresh
  token for a new pair.
- **Sign out**: revokes the user's refresh token.
- **Create user**: registers a user with a set of claims (scopes).

The repo also contains **External.API**, a sample "weather" service that shows
how a downstream service authorizes calls using the access token's `scope`
claim.

## Key facts

- **Runtime**: .NET 5 (`net5.0`), ASP.NET Core Web API, Swagger (Swashbuckle)
- **Datastore**: MongoDB, database `auth_database`
- **Tokens**: RS256 JWT, 300-second lifetime. Refresh tokens are 64 bytes and
  last 60 minutes.
- **Ports (docker-compose)**: Auth API `5000`, External API `5050`,
  MongoDB `27017`

## Contacts

<!-- Slack channel, on-call rotation, escalation path. -->
