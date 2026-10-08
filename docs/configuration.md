# Configuration

Settings come from `Auth.API/appsettings.json`. Environment variables override
them using ASP.NET Core's `Section__Key` convention.

| Setting | Env var override | Default | Notes |
| --- | --- | --- | --- |
| `MongoDBSettings:ConnectionString` | `MongoDBSettings__ConnectionString` | `mongodb://localhost:27017` | docker-compose sets `mongodb://host.docker.internal:27017` |
| `MongoDBSettings:DatabaseName` | `MongoDBSettings__DatabaseName` | `auth_database` | |
| `JwtSettings:AccessTokenSettings:Issuer` | `JwtSettings__AccessTokenSettings__Issuer` | `http://localhost:5000/` | |
| `JwtSettings:AccessTokenSettings:Audience` | `JwtSettings__AccessTokenSettings__Audience` | `http://localhost/` | |
| `JwtSettings:AccessTokenSettings:LifeTimeInSeconds` | `JwtSettings__AccessTokenSettings__LifeTimeInSeconds` | `300` | |
| `JwtSettings:AccessTokenSettings:privateKey` | `JwtSettings__AccessTokenSettings__privateKey` | sample key | **Secret.** See the warning below |
| `JwtSettings:AccessTokenSettings:publicKey` | `JwtSettings__AccessTokenSettings__publicKey` | sample key | Shared with every consuming service |
| `JwtSettings:RefreshTokenSettings:Length` | `JwtSettings__RefreshTokenSettings__Length` | `64` | Bytes |
| `JwtSettings:RefreshTokenSettings:LifeTimeInMinutes` | `JwtSettings__RefreshTokenSettings__LifeTimeInMinutes` | `60` | |

!!! danger "Sample signing key is committed"
    `appsettings.json` contains a sample RSA **private key**, marked "DO NOT
    USE in production". Any real deployment must generate its own key pair and
    inject the private key from a secret store (for example AWS Secrets
    Manager) through `JwtSettings__AccessTokenSettings__privateKey`. The
    committed key must never be used outside local development.
