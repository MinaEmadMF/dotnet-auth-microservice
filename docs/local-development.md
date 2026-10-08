# Local development

## Prerequisites

- Docker Desktop
- .NET 5 SDK, if you run the projects outside Docker
- A MongoDB client (`mongosh` or Compass) to run the seed script

## Run locally

```bash
docker-compose up
```

Then run `Auth.Infrastructure/Repositories/MongoDB/Scripts/initialize.js`
against `mongodb://localhost:27017` to create the sample users.

| Service | URL |
| --- | --- |
| Auth API | <http://localhost:5000> |
| External (weather) API | <http://localhost:5050> |
| MongoDB | `mongodb://localhost:27017` |

## Tests

There is no test project yet.

## Common problems

- **Auth API cannot reach MongoDB inside Docker.** The compose file uses
  `host.docker.internal`, so make sure Docker Desktop exposes it (the default
  on Windows and macOS).
- **Login fails with valid credentials.** The seed script has not been run.
