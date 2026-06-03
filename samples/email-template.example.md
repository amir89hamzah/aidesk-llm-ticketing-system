# AIDesk Email Template Example

## OTP email

Subject:

```text
AIDesk OTP Verification
```

Body:

```text
Your AIDesk OTP is {{ otp_code }}.

It will expire in 5 minutes.

If you did not request this action, ignore this email.
```

## Ticket created email

Subject:

```text
AIDesk Ticket Created: {{ case_id }}
```

Body:

```text
Ticket {{ case_id }} has been created.

Site: {{ site }}
System: {{ system }}
Problem: {{ problem_title }}
Start Date: {{ start_date }}
End Date: {{ end_date }}
```

## Ticket modified email

Subject:

```text
AIDesk Ticket Updated: {{ case_id }}
```

Body:

```text
Ticket {{ case_id }} has been updated.

Updated fields:
{{ changes }}
```
