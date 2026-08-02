---
name: Check a vendor's compliance status
description: Look up a vendor (party) in TrustLayer, inspect its compliance profile, and retrieve its compliance certificate.
api: openapi/trustlayer-platform-v1-openapi.yaml
operations: [get-parties, get-parties-partyId-compliance-profile, get-parties-id-compliance-certificate]
---

# Check a vendor's compliance status

Use the TrustLayer Platform API v1 (base URL `https://api.trustlayer.io/v1`).

## Auth
Send `Authorization: <API token>` on every request.

## Steps
1. **Find the vendor** — `get-parties` (`GET /parties`) and match on name, or use a known party id directly.
2. **Read its requirements** — `get-parties-partyId-compliance-profile` (`GET /parties/{partyId}/compliance-profile`) to see the compliance profile (the requirement set) the vendor is measured against.
3. **Retrieve the certificate** — `get-parties-id-compliance-certificate` (`GET /parties/{partyId}/compliance-certificate`) to pull the current compliance certificate / status for the vendor.

## Rules
- A 404 on the certificate means none has been generated yet — the vendor may still owe documents; trigger `post-parties-partyId-document-request`.
- Handle 401 (bad token) and 403 (token lacks workspace access). See `errors/trustlayer-problem-types.yml`.
- To react to status changes in real time instead of polling, subscribe to webhooks (`record_compliance` / `party_compliance` events) — see `asyncapi/trustlayer-webhooks.yml`.
