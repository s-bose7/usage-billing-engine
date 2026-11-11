# Architecture — usage-billing-engine

_Questions this document answers:_
- Components, and what each one owns
- Data flow from "API call happened" to "wallet debited"
- Data model (tables / topics / keys)
- Where idempotency is enforced, and with which key
- What happens on crash at each arrow in the flow
