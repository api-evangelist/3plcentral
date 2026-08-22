# 3PL Warehouse Manager (3plcentral)

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **Not from the company, and here with a question?** You are welcome here — we would rather be the
> front line and point you the right way than have a good report go nowhere. What this repository
> can answer is narrow, though, so it is worth knowing who you are actually looking for:
>
> - **A question about how the API works, an account, billing, or a bug in the service** — that is
>   the company's own support, not us. We profile this API; we do not operate it and cannot see
>   your account.
> - **A bug in an open-source project we only catalog** — file it on that project's own repository.
>   This has happened with a real and correct bug report that reached us instead of the people who
>   could fix it, which helped nobody.
> - **Anything about this listing itself** — the description, the tags, the rating, a missing or
>   wrong artifact — is ours. Open an issue here.
> - **Not sure, or something general about API Evangelist or APIs.io** — open an issue on the
>   [APIs.io Inbox](https://github.com/api-search/inbox) and we will route it.
>
> **This repository contains no software, and we will never ask you to download anything.** There is
> no build, release, installer, or binary here — only text and machine-readable API descriptions, so
> there is nothing here that can be "corrupt" or need "repairing". Any issue, comment, or email
> claiming otherwise and offering a download link is not from us and is hostile. Do not follow the
> link; it is a lure. Report it to GitHub and, if you like, tell us at
> [info@apievangelist.com](mailto:info@apievangelist.com) so we can take it down.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

3PL Warehouse Manager is the flagship cloud warehouse management system (WMS) built for third-party logistics providers, now sold under **Extensiv** and historically known as **"3PL Central"**. Its public integration surface is the **SecureWMS REST API** (base `https://secure-wms.com`), used to create and retrieve orders, manage SKU items and inventory, read stock summaries and stock details, submit and track inbound receivers (Advance Ship Notices / ASN), and enumerate customers, warehouses/facilities, and locations.

Authentication is OAuth 2.0 client-credentials: Base64-encode `clientId:clientSecret`, POST it as a Basic `Authorization` header to `https://secure-wms.com/AuthServer/api/Token` with a JSON body of `{"grant_type":"client_credentials","user_login_id":<id>}`, and use the returned short-lived bearer token (typically valid 30-60 minutes) on all other calls. Collection endpoints are paged with `pgnum`/`pgsiz` and filterable with Resource Query Language (RQL). All traffic must use HTTPS.

> **Relationship to `all/extensiv`:** This entry documents the **3PL Warehouse Manager product specifically** — the SecureWMS REST API. It is meant to be **complementary to, not a duplicate of**, the broader `all/extensiv` company entry. Extensiv is the parent company whose suite also spans Order Management, Integration Manager, Fulfillment Marketplace, and Warehouse Analytics; `all/extensiv` covers the company/suite level, while `all/3plcentral` stays scoped to the 3PL Warehouse Manager / SecureWMS API.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/3plcentral/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/3plcentral/refs/heads/main/apis.yml)

## Tags

- Warehouse Management
- WMS
- 3PL
- Logistics
- Fulfillment
- Inventory
- Orders
- SecureWMS
- Extensiv

## Timestamps

- **Created:** 2026-07-04
- **Modified:** 2026-07-04

## APIs

### 3PL Warehouse Manager Orders API

Create, retrieve, and list outbound orders — the most common use of the SecureWMS API. Orders carry customer, ship-to, line items, and shipping details; results are paged and filterable with RQL.

- **Base URL:** `https://secure-wms.com`
- **Endpoints:** `GET /orders` (confirmed), `POST /orders`, `GET /orders/{orderId}` (documented/modeled)

### 3PL Warehouse Manager Items API

List and read the SKU items defined for a customer under `/customers/{customerId}/items`.

- **Base URL:** `https://secure-wms.com`
- **Endpoints:** `GET /customers/{customerId}/items` (confirmed)

### 3PL Warehouse Manager Inventory API

Retrieve on-hand inventory (`/inventory`) and per-receive-line stock details (`/inventory/stockdetails`).

- **Base URL:** `https://secure-wms.com`
- **Endpoints:** `GET /inventory`, `GET /inventory/stockdetails` (confirmed)

### 3PL Warehouse Manager Stock Summaries API

Read rolled-up on-hand / available / allocated / committed quantities via `/inventory/stocksummaries`.

- **Base URL:** `https://secure-wms.com`
- **Endpoints:** `GET /inventory/stocksummaries` (confirmed)

### 3PL Warehouse Manager Receivers (ASN) API

Create and retrieve inbound receivers (Advance Ship Notices) via `/inventory/receivers`.

- **Base URL:** `https://secure-wms.com`
- **Endpoints:** `GET /inventory/receivers`, `POST /inventory/receivers`, `GET /inventory/receivers/{receiverId}` (documented/modeled)

### 3PL Warehouse Manager Customers API

List and read the customers (merchants) a 3PL fulfills for, under `/customers`.

- **Base URL:** `https://secure-wms.com`
- **Endpoints:** `GET /customers` (confirmed)

### 3PL Warehouse Manager Warehouses API

Enumerate warehouses/facilities and their bin locations via `/inventory/facilities` and `/inventory/facilities/{facilityId}/locations`.

- **Base URL:** `https://secure-wms.com`
- **Endpoints:** `GET /inventory/facilities/{facilityId}/locations` (confirmed), `GET /inventory/facilities` (modeled)

### 3PL Warehouse Manager Packages API

Read the packages (cartons) associated with a shipped order via `/orders/{orderId}/packages`.

- **Base URL:** `https://secure-wms.com`
- **Endpoints:** `GET /orders/{orderId}/packages` (modeled)

## Common Properties

- [GitHub Organization](https://github.com/tpl-central)
- [LinkedIn](https://www.linkedin.com/company/extensiv)
- [Website](https://www.extensiv.com/3pl-warehouse-manager)
- [Documentation](https://developer.3plcentral.com/)
- [Plans](plans/3plcentral-plans-pricing.yml)
- [Rate Limits](rate-limits/3plcentral-rate-limits.yml)
- [Fin Ops](finops/3plcentral-finops.yml)

## Endpoint Provenance

Read (`GET`) endpoints for customers, items, inventory, stock details, stock summaries, facility locations, and orders are **confirmed** against the public developer portal and the open-source [`singer-io/tap-3plcentral`](https://github.com/singer-io/tap-3plcentral) extractor. Order creation, receiver (ASN) create/list/get, the facilities collection, and order packages are **documented** in the developer portal; request/response shapes gated behind the authenticated portal are **modeled** honestly and marked per-operation with `x-endpoint-status` in the OpenAPI.

## Maintainers

**FN:** Kin Lane
**Email:** kin@apievangelist.com
