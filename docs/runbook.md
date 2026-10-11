# Runbook

## Dashboards and logs

There are none yet. The service logs to stdout (ASP.NET Core console logging).

## Alerts

| Alert | Meaning | First steps |
| --- | --- | --- |
| | | |

## Common operations

- **Revoke a user's session.** Call `POST /api/Auth/SignOut` with the user ID.
  Their refresh token is invalidated, and the access token expires within 5
  minutes.
- **Rotate the signing key.** Generate a new RSA pair, update the private key
  here and the public key in every consuming service, then redeploy. Tokens
  that are already issued fail validation after the switch.

## Incident checklist

1. Acknowledge the alert and post in the incident channel.
2. Check recent deploys and roll back if the timing matches.
3. Check MongoDB health and connectivity.
4. Escalate to the owning team's on-call if not resolved in 15 minutes.
