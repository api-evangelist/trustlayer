---
name: Onboard a vendor and request their certificate of insurance
description: Create a party (vendor) in TrustLayer, add a contact, and send them a document request to collect their certificate of insurance (COI).
api: openapi/trustlayer-platform-v1-openapi.yaml
operations: [post-parties, post-parties-id-contacts, post-parties-partyId-document-request]
---

# Onboard a vendor and request their COI

Use the TrustLayer Platform API v1 (base URL `https://api.trustlayer.io/v1`).

## Auth
Send `Authorization: <API token>` on every request (v1 apiKey scheme "Token", in the header). Obtain the token from your TrustLayer workspace.

## Steps
1. **Create the vendor** — `post-parties` (`POST /parties`) with the vendor's name and any custom data. Capture the returned party id.
2. **Add a contact** — `post-parties-id-contacts` (`POST /parties/{partyId}/contacts`) using the id from step 1, so requests reach a real person.
3. **Request documents** — `post-parties-partyId-document-request` (`POST /parties/{partyId}/document-request`) to email the contact and ask them to upload their COI and any other required documents.

## Rules
- Errors are returned with an HTTP status; handle 400 (validation), 401 (bad token), 404 (unknown id). See `errors/trustlayer-problem-types.yml`.
- No idempotency-key is supported — avoid duplicate `POST /parties` calls by checking `get-parties` first.
- v1 is deprecated (sunset 2027-03-31); for new builds prefer v2 (`https://api.trustlayer.io/v2`).
