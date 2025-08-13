# Account Inquiry API

**Owner:** Platform Team  
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
