# Architecture

AIDesk is built as a Flowise Agent Flow that orchestrates LLM decisions, JavaScript transformation nodes, HTTP calls, OTP verification, SMTP email delivery, and Google Sheets storage.

## Components

| Component | Role |
|---|---|
| User / Engineer | Provides ticket request, search query, update request, or OTP |
| AIDesk Chat UI | Public chat interface hosted at `www.aidesk.rest` |
| Flowise Agent Flow | Main workflow engine |
| OpenAI GPT-4o | Router, search responder, help assistant |
| OpenAI GPT-4o mini | Field extraction and validation tasks |
| Google Apps Script | API layer between Flowise and Google Sheets |
| Google Sheets | Ticket storage |
| SMTP relay | Sends OTP and notification emails |
| VPS | Hosting environment |
| Nginx | Reverse proxy and HTTPS entry point |

## Main routes

AIDesk begins by routing user input into one of these intents:

| Intent | Purpose |
|---|---|
| `general` | Help/user guide |
| `create` | Create a new support ticket |
| `edit` | Modify/update an existing ticket |
| `search` | Search or explain existing tickets |
| `otp_verify` | Verify OTP code |

## Data flow

1. User sends message to AIDesk.
2. LLM router classifies the message.
3. Flowise condition router sends the message to the relevant branch.
4. Create/modify branches extract structured data from natural language.
5. Required fields are checked.
6. OTP is generated and sent by SMTP relay.
7. User replies with OTP.
8. OTP is verified.
9. Create or modify action is committed through Google Apps Script.
10. Ticket is stored or updated in Google Sheets.
11. User receives success/error message.

## Design principle

AIDesk is designed as a controlled AI workflow, not a free-form chatbot. The LLM is used for:

- routing,
- field extraction,
- validation support,
- search response summarization,
- user guidance.

Critical actions are guarded by deterministic logic such as:

- JSON extraction,
- field validation,
- OTP expiry,
- attempt limit,
- routing conditions,
- HTTP response handling.
