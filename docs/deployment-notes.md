# Deployment Notes

## Public deployment

AIDesk is deployed publicly at:

```text
https://www.aidesk.rest
```

## Hosting design

The production deployment uses:

- VPS hosting
- Docker / Docker Compose
- Flowise Agent Flow
- Nginx reverse proxy
- HTTPS public access
- SMTP relay service
- Google Apps Script as ticket API
- Google Sheets as ticket storage

## Example deployment layout

```text
Internet
  ↓
Domain: www.aidesk.rest
  ↓
Nginx reverse proxy
  ↓
Flowise container
  ↓
Agent Flow
  ↓
Google Apps Script / SMTP relay / OpenAI API
```

## Example Docker Compose

See [`../docker-compose.example.yml`](../docker-compose.example.yml).

The provided compose file is a safe example only. It is not a production backup.

## Environment variables

See [`../.env.example`](../.env.example).

Production `.env` files must never be committed to GitHub.

## Notes

- Do not expose Flowise admin UI publicly without authentication.
- Do not commit OpenAI keys, SMTP credentials, Google Script deployment IDs, or spreadsheet IDs.
- Use a reverse proxy for public access.
- Keep the SMTP relay isolated from public unauthenticated access where possible.
