# 3PL Warehouse Manager (3plcentral)

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
