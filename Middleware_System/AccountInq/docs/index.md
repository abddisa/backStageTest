# Account Inquiry API

**Owner:** Bunna Bank System development Team  
**System:** Middleware System  
**Status:** Production  
**Last Updated:** 2025-08-13

The Account Inquiry API lets internal services fetch account metadata, balances, and status in real time. It is read-only and optimized for low-latency lookups.

> If you are new to TechDocs, see the project’s `mkdocs.yml` and `catalog-info.yaml` examples in the repo root.

---

## Base URL

- **Prod:** `https://api.example.com/accounts`  
- **Staging:** `https://staging-api.example.com/accounts`

> Replace `example.com` with your org domain.

## Authentication & Authorization

- **Auth:** OAuth 2.0 Client Credentials (preferred) or mutual TLS (mTLS)
- **Scopes:** `accounts:read`
- **Headers:**
  - `Authorization: Bearer <access_token>`
  - `X-Correlation-Id: <uuid>` *(optional but recommended)*

401 for invalid/expired tokens, 403 if token lacks `accounts:read`.

## Idempotency & Caching

- **GET** operations are safe and cacheable.
- Clients may cache **200 OK** responses for up to **30s** unless `Cache-Control` states otherwise.

## Rate Limits

- Default: **600 requests / minute** per client.  
- `429 Too Many Requests` when exceeded. Back off with exponential jitter.

---

## Resources

### Account
Represents a bank account and its public metadata.

| Field | Type | Description |
|---|---|---|
| `accountId` | string | Internal UUID for the account. |
| `foracid` | string | Core banking account number. |
| `cifId` | string | Customer identifier. |
| `accountName` | string | Account holder name (masked when required). |
| `productCode` | string | Product or scheme code (e.g., `SBA`, `CAA`). |
| `branchCode` | string | Branch/sol id. |
| `currency` | string | ISO 4217 code (e.g., `ETB`, `USD`). |
| `balance` | number | Ledger balance. |
| `availableBalance` | number | Available balance. |
| `status` | string | `ACTIVE`, `BLOCKED`, `DORMANT`, `CLOSED`. |
| `openedAt` | string | ISO 8601 timestamp. |
| `updatedAt` | string | ISO 8601 timestamp. |

---

## Endpoints

### GET `/accounts/{accountId}`
Fetch a single account by internal `accountId`.

**Request**
GET /accounts/2b3c9a9f-7a0a-4f1a-a5ab-9b6f9b2b1720
Authorization: Bearer <token>
Accept: application/json


**Response — 200**
```json
{
  "accountId": "2b3c9a9f-7a0a-4f1a-a5ab-9b6f9b2b1720",
  "foracid": "0012345678901",
  "cifId": "CIF123456",
  "accountName": "AB***A K***",
  "productCode": "SBA",
  "branchCode": "1001",
  "currency": "ETB",
  "balance": 15420.75,
  "availableBalance": 15000.25,
  "status": "ACTIVE",
  "openedAt": "2023-05-22T10:15:30Z",
  "updatedAt": "2025-08-12T18:40:03Z"
}


###Failure
404 if not found
410 if the account is closed and purged from lookup

### GET /accounts
Search or fetch by business keys.
Query Parameters
| Name      | Type    | Required | Description                             |         |         |           |
| --------- | ------- | -------- | --------------------------------------- | ------- | ------- | --------- |
| `foracid` | string  | no       | Exact core account number.              |         |         |           |
| `cifId`   | string  | no       | Customer identifier (returns multiple). |         |         |           |
| `status`  | string  | no       | Filter by \`ACTIVE                      | BLOCKED | DORMANT | CLOSED\`. |
| `limit`   | integer | no       | Default `50`, max `200`.                |         |         |           |
| `cursor`  | string  | no       | Opaque cursor for pagination.           |         |         |           |
