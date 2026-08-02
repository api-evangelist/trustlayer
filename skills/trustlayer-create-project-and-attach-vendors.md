---
name: Create a project and attach vendors
description: Create a project in TrustLayer, attach parties (vendors) to it, and check the project's compliance profile.
api: openapi/trustlayer-platform-v1-openapi.yaml
operations: [post-projects, post-projects-id-relationships-parties, get-projects-projectId-compliance-profile]
---

# Create a project and attach vendors

Use the TrustLayer Platform API v1 (base URL `https://api.trustlayer.io/v1`).

## Auth
Send `Authorization: <API token>` on every request.

## Steps
1. **Create the project** — `post-projects` (`POST /projects`) with the project name/details (e.g. a job site, property, or program). Capture the project id.
2. **Attach vendors** — `post-projects-id-relationships-parties` (`POST /projects/{projectId}/relationships/parties`) to associate one or more existing parties with the project.
3. **Check project compliance** — `get-projects-projectId-compliance-profile` (`GET /projects/{projectId}/compliance-profile`) to review the requirement set applied at the project level.

## Rules
- Create parties first (see `trustlayer-onboard-vendor-and-request-coi.md`); the attach step references existing party ids.
- Handle 400 (validation), 401 (bad token), 404 (unknown project/party id), 409 (conflict). See `errors/trustlayer-problem-types.yml`.
- Detach with `DELETE /projects/{projectId}/relationships/parties/{partyId}` when a vendor leaves the project.
