# Security Notes

This repository is safe for public portfolio use because production secrets are redacted or excluded.

## Do not commit

- `.env`
- OpenAI API key
- SMTP username/password
- Google Apps Script deployment ID
- Google Sheet ID
- Flowise credentials
- VPS IP/SSH details
- real customer emails
- real ticket data
- internal company documents
- client names that are confidential
- screenshots showing secrets or admin URLs

## Redacted items

The exported Flowise JSON has been sanitized to remove:

- active Google Apps Script endpoint,
- active Google Sheet ID,
- personal emails,
- credential fields.

## OTP safety

The OTP workflow includes:

- 6-digit OTP generation,
- 5-minute expiry,
- attempt counter,
- lockout after repeated failure,
- clearing OTP after successful verification.

## Public demo caution

The public demo domain may be accessible. Avoid putting any confidential data into demo prompts.

## Recommended improvements

- Add authentication for admin access.
- Add rate limiting for OTP requests.
- Store OTP hashes instead of plain OTP where possible.
- Move audit log to a database.
- Restrict SMTP relay access to internal network/container network.
- Add monitoring for failed OTP attempts.
