# Workflow

## 1. General / Help flow

Purpose:

- Explain what AIDesk can do.
- Guide users on how to create, search, or modify tickets.
- Explain OTP behavior and email validation rules.

Main nodes:

- `LLM_5`
- Direct reply nodes

## 2. Create ticket flow

Purpose:

Create a new engineering support ticket from natural-language input.

High-level steps:

1. User asks to create a ticket.
2. Router detects `create`.
3. `LLM_1` extracts ticket fields.
4. JavaScript nodes merge new input with existing draft state.
5. Date normalization/validation runs.
6. `LLM_Checker2` checks required fields.
7. If fields are missing, AIDesk asks for the missing fields.
8. If all fields are present, OTP is generated.
9. OTP is sent through SMTP relay.
10. User replies with OTP.
11. OTP is verified.
12. Ticket is committed through Google Apps Script.
13. Success message is returned.

Required fields:

- engineer_email
- system
- site
- pic
- problem_title
- action_description
- start_date
- end_date

## 3. Modify / update ticket flow

Purpose:

Modify an existing ticket while keeping control and traceability.

High-level steps:

1. User asks to modify/update an existing `case_id`.
2. Router detects `edit`.
3. `LLM_3` extracts the case ID, engineer email, and requested changes.
4. JavaScript nodes normalize and validate the modification draft.
5. `LLM_Checker3` checks if the request is ready for OTP.
6. OTP is generated and sent.
7. User replies with OTP.
8. OTP is verified.
9. Modify/update action is committed through Google Apps Script.
10. Success or error is returned.

Allowed modification fields:

- site
- pic
- problem_title
- action_description
- start_date
- end_date

## 4. Search ticket flow

Purpose:

Allow the user to search, view, summarize, or calculate information from tickets.

High-level steps:

1. User asks to search or view tickets.
2. Router detects `search`.
3. HTTP search request is sent to Google Apps Script.
4. Current/latest ticket rows are returned.
5. `LLM_4_SearchResponder` explains only the relevant result.

Search behavior:

- case ID has highest priority,
- person names may match `engineer_email` or `pic`,
- equipment names may match `system`, `problem_title`, or `action_description`,
- site names filter by `site`,
- if data is missing, the bot says so instead of guessing.

## 5. OTP verification flow

Purpose:

Protect create/modify actions from accidental or unauthorized commits.

Behavior:

- OTP is 6 digits.
- OTP has expiry time.
- OTP status can be `sent`, `verified`, `expired`, or `locked`.
- Incorrect attempts are counted.
- Too many failed attempts locks the OTP flow.
- After successful OTP verification, create/modify commit is allowed depending on OTP scope.

OTP scopes:

- `create`
- `modify_update`
