# Lessons Learned

## 1. LLM should not own the whole workflow

The most stable design is to let the LLM handle language tasks and let deterministic nodes handle control tasks.

LLM is useful for:

- intent detection,
- field extraction,
- search explanation,
- help response.

Deterministic logic is better for:

- OTP generation,
- OTP expiry,
- attempt counting,
- routing,
- JSON extraction,
- HTTP action success/error handling.

## 2. State management is critical

Ticket creation and modification require multiple turns. Flow state is needed to keep:

- known fields,
- missing fields,
- OTP status,
- OTP scope,
- draft values,
- last action status.

## 3. Search is different from create/edit

Search should override create/edit context when the user clearly asks to view, show, list, find, summarize, or check ticket status.

## 4. Email input is context-sensitive

An email alone can mean different things depending on the previous intent. The router needs rules to avoid treating every email as create-ticket input.

## 5. OTP flow needs clear user guidance

Users need to understand:

- where OTP was sent,
- how long it is valid,
- what happens after wrong attempts,
- how to request a new OTP,
- why email validation exists.

## 6. Portfolio value

The project is useful as a career portfolio because it shows:

- real workflow design,
- applied AI use case,
- production deployment thinking,
- support-process automation,
- integration with email and spreadsheet backend.
