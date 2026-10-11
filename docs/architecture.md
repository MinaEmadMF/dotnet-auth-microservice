# Architecture

## Context

```text
 Client app ── 1. POST /api/Auth/Login ─────────▶ Auth.API ──▶ MongoDB
     ▲                                               │        (users, refresh tokens)
     └──────── 2. access token + refresh token ◀─────┘

 Client app ── 3. Authorization: Bearer <token> ─▶ External.API
                                                   (verifies the RS256 signature
                                                    with the public key and
                                                    checks the scope claim)
```

Downstream services never call the Auth service to validate a token. They
verify the JWT signature locally with the RSA **public key** and authorize on
the `scope` claim.

![Auth sequence](https://veglos.github.io/assets/img/2021-11-08-dotnet-auth-microservice-with-clean-architecture/auth-sequence.jpg)

## Components (Clean Architecture layers)

| Project | Layer | Responsibility |
| --- | --- | --- |
| `Auth.Domain` | Domain | Entities: `User`, `Claim`, `RefreshToken` |
| `Auth.Application` | Application | Use cases (`Login`, `RefreshToken`, `SignOut`, `CreateUser`), and the ports `IAuthRepository`, `IAuthTokenService` and `ICryptographyService` |
| `Auth.Infrastructure` | Infrastructure | MongoDB repository, JWT service (RS256), password cryptography |
| `Auth.API` | Presentation | ASP.NET Core controller `api/Auth/*`, DI wiring, Swagger |
| `External.API` | Sample consumer | Weather API protected by a scope-based authorization policy |

Dependencies point inwards: API → Application → Domain. Infrastructure
implements the Application ports.

## Data

- **MongoDB** database `auth_database` stores users with hashed passwords,
  their claims, and the current refresh token.
- `Auth.Infrastructure/Repositories/MongoDB/Scripts/initialize.js` seeds
  sample users.
- **PII**: user emails and password hashes.

## Integrations

- **Synchronous**: REST/JSON over HTTP.
- **No message queues.**

## Non-functional requirements

<!-- Expected load, latency targets, availability, scaling approach. -->
