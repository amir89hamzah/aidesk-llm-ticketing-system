# Flowise Node Map

This Flowise export contains **70 nodes** and **66 edges**.

## Node inventory

| Label | Type | Model | Category |
|---|---|---|---|
| `Start` | Start | - | Agent Flows |
| `LLM_0` | LLM | gpt-4o | Agent Flows |
| `JSON_intent` | Tool | - | Agent Flows |
| `Router_1` | Condition | - | Agent Flows |
| `LLM_1` | LLM | gpt-4o-mini | Agent Flows |
| `Sticky Note` | StickyNote | - | Agent Flows |
| `LLM_3` | LLM | gpt-4o-mini | Agent Flows |
| `LLM_4_SearchResponder` | LLM | gpt-4o | Agent Flows |
| `LLM_5` | LLM | gpt-4o | Agent Flows |
| `LLM_Checker2` | LLM | gpt-4o-mini | Agent Flows |
| `Router` | Condition | - | Agent Flows |
| `Sticky Note (1)` | StickyNote | - | Agent Flows |
| `JS_GenerateOTP` | CustomFunction | - | Agent Flows |
| `JSON_otp_code` | Tool | - | Agent Flows |
| `AskOTP` | DirectReply | - | Agent Flows |
| `AskMoreInfo` | DirectReply | - | Agent Flows |
| `JS_OTP_Verify` | CustomFunction | - | Agent Flows |
| `OTP_Result` | Condition | - | Agent Flows |
| `Reply_OTP_Verify` | DirectReply | - | Agent Flows |
| `JSON_otp_attempts` | Tool | - | Agent Flows |
| `JSON_otp_status_message` | Tool | - | Agent Flows |
| `JSON_otp_last_entered` | Tool | - | Agent Flows |
| `JSON_otp_verified` | Tool | - | Agent Flows |
| `JSON_otp_status` | Tool | - | Agent Flows |
| `JSON_otp_code` | Tool | - | Agent Flows |
| `JSON_otp_expires_at` | Tool | - | Agent Flows |
| `OTP_intent` | Condition | - | Agent Flows |
| `Error_Intent` | DirectReply | - | Agent Flows |
| `JS_OTP_Scope` | CustomFunction | - | Agent Flows |
| `JS_interpret1` | CustomFunction | - | Agent Flows |
| `Router_HTTP1` | Condition | - | Agent Flows |
| `Create_Success` | DirectReply | - | Agent Flows |
| `JSON_action_ok` | Tool | - | Agent Flows |
| `JSON_op_type` | Tool | - | Agent Flows |
| `JSON_case_id` | Tool | - | Agent Flows |
| `JSON_message_user` | Tool | - | Agent Flows |
| `JS_Cleanup1` | CustomFunction | - | Agent Flows |
| `Error_Intent2` | DirectReply | - | Agent Flows |
| `JS_AllInOne_Draft3` | CustomFunction | - | Agent Flows |
| `LLM_Checker3` | LLM | gpt-4o-mini | Agent Flows |
| `OTP_Router_3` | Condition | - | Agent Flows |
| `JS_OTP_Scope_3` | CustomFunction | - | Agent Flows |
| `Reply_Verify_3` | DirectReply | - | Agent Flows |
| `JSON_otp_code (1)` | Tool | - | Agent Flows |
| `JSON_otp_expires_at (7)` | Tool | - | Agent Flows |
| `AskOTP_3` | DirectReply | - | Agent Flows |
| `JS_GenerateOTP_3` | CustomFunction | - | Agent Flows |
| `HTTP_Modify_Update` | HTTP | - | Agent Flows |
| `commit_success` | Tool | - | Agent Flows |
| `commit_message` | Tool | - | Agent Flows |
| `commit_case_id` | Tool | - | Agent Flows |
| `commit_error_code` | Tool | - | Agent Flows |
| `Router_HTTP2` | Condition | - | Agent Flows |
| `Error_Intent3` | DirectReply | - | Agent Flows |
| `JS_Cleanup2` | CustomFunction | - | Agent Flows |
| `Modify_Success` | DirectReply | - | Agent Flows |
| `HTTP_Search` | HTTP | - | Agent Flows |
| `HTTP_CreateTicket` | HTTP | - | Agent Flows |
| `sanitize_http_create` | CustomFunction | - | Agent Flows |
| `sanitize_http_modify` | CustomFunction | - | Agent Flows |
| `Create_SendOTP` | HTTP | - | Agent Flows |
| `Create_Success` | HTTP | - | Agent Flows |
| `Modify_Success` | HTTP | - | Agent Flows |
| `Modify_SendOTP` | HTTP | - | Agent Flows |
| `sanitize_create_sendOTP` | CustomFunction | - | Agent Flows |
| `JS_JSONSafeForHttp` | CustomFunction | - | Agent Flows |
| `Sticky Note` | StickyNote | - | Agent Flows |
| `JS_AllInOne_CreateDraft` | CustomFunction | - | Agent Flows |
| `JS_NormalizeValidateDates_Create` | CustomFunction | - | Agent Flows |
| `JS_NVDates_Modify` | CustomFunction | - | Agent Flows |

## Main logical groups

### Routing

- `LLM_0` classifies the user message.
- `JSON_intent` extracts the intent from the LLM output.
- `Router_1` sends the message to general, create, edit, search, or OTP verification branches.

### Create ticket

- `LLM_1` extracts ticket fields.
- `JS_AllInOne_CreateDraft` merges extracted values into draft state.
- `JS_NormalizeValidateDates_Create` normalizes and validates dates.
- `LLM_Checker2` checks if required fields are complete.
- `JS_GenerateOTP` creates OTP.
- `Create_SendOTP` sends OTP via SMTP relay.
- `HTTP_CreateTicket` commits ticket creation through Google Apps Script.

### Modify / update ticket

- `LLM_3` extracts case ID and changes.
- `JS_AllInOne_Draft3` builds modification draft.
- `JS_NVDates_Modify` normalizes modification dates.
- `LLM_Checker3` checks readiness for OTP.
- `JS_GenerateOTP_3` generates OTP for modification.
- `HTTP_Modify_Update` commits modification through Google Apps Script.

### Search

- `HTTP_Search` retrieves relevant/current ticket data.
- `LLM_4_SearchResponder` explains the ticket result to the user.

### OTP

- `JS_OTP_Verify` verifies OTP input.
- JSON extractor nodes update OTP state fields.
- `OTP_Result` and `OTP_intent` route verified OTP to create or modify commit.

### User guide

- `LLM_5` explains how the chatbot works and guides users.
