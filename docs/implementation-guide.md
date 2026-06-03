# Implementation Guide

This guide explains how someone can rebuild the same concept without using the production secrets.

## 1. Prepare storage

Create a Google Sheet with columns similar to:

```text
case_id
created_at
updated_at
engineer_email
site
system
pic
problem_title
action_description
start_date
end_date
current
version
status
```

Recommended design:

- Keep only latest row as `current = yes`, or
- Store revision rows and mark latest version as current.

## 2. Create Google Apps Script endpoint

Build a simple HTTP endpoint that supports actions such as:

- `create_ticket`
- `modify_ticket`
- `search_ticket`

Expected behavior:

- Create: generate/accept a case ID and append ticket row.
- Modify: add new latest revision or update latest row depending on design.
- Search: return rows as JSON.
- Return structured success/error response.

Example response shape:

```json
{
  "success": true,
  "case_id": "CASE-20260110-001",
  "message_user": "Ticket created successfully."
}
```

## 3. Create SMTP relay

AIDesk uses an internal SMTP relay endpoint to send:

- OTP email,
- create success email,
- modify success email.

Example API shape:

```json
{
  "to": "engineer@example.com",
  "subject": "Your AIDesk OTP",
  "text": "Your OTP is 123456. It will expire in 5 minutes."
}
```

## 4. Build Flowise Agent Flow

Core Flowise branches:

1. Router
2. Create ticket
3. Modify ticket
4. Search ticket
5. OTP verification
6. Help/general guide

Use LLM nodes for:

- intent classification,
- field extraction,
- user-facing search response,
- help assistant.

Use JavaScript nodes for:

- merging state,
- validating dates,
- generating OTP,
- verifying OTP,
- preparing JSON-safe payloads.

Use HTTP nodes for:

- Google Apps Script,
- SMTP relay.

## 5. Add OTP control

Recommended OTP state:

```text
otp_status
otp_code
otp_email
otp_attempts
otp_verified
otp_expires_at
otp_scope
otp_last_entered
otp_status_message
```

Recommended rules:

- OTP expires after 5 minutes.
- Wrong attempts increment counter.
- Lock after 3 wrong attempts.
- Clear OTP code after successful verification.
- Track scope: create or modify.

## 6. Deploy

Suggested deployment:

1. Run Flowise in Docker.
2. Put Nginx in front of Flowise.
3. Point domain to VPS.
4. Configure HTTPS.
5. Keep `.env` out of Git.
6. Test create, search, modify, OTP expired, OTP wrong, and OTP locked cases.

## 7. Test cases

Minimum test set:

- Create ticket with all fields.
- Create ticket with missing fields.
- Create ticket with invalid email.
- OTP correct.
- OTP wrong once.
- OTP wrong three times.
- OTP expired.
- Search by case ID.
- Search by site/system/PIC.
- Modify ticket with valid case ID.
- Modify ticket with missing case ID.
