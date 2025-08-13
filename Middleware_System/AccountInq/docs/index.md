---
title: Account Inquiry API
description: Retrieve account information including balances, details, and customer relationships
---

# Account Inquiry API

## Overview

The Account Inquiry API provides secure, programmatic access to account information for authorized applications. This RESTful API enables developers to retrieve account details, balances, and customer-account relationships while maintaining strict security and compliance standards.

## Getting Started

### Prerequisites
- Valid API credentials (client ID and secret)
- OAuth 2.0 implementation
- Whitelisted IP addresses (for production access)

### Sandbox Environment
```text
Base URL: https://api.sandbox.yourcompany.com/account/v1
Test Customer ID: cust_12345
Test Account ID: acct_67890

### Authentication
All endpoints require Bearer Token authentication:

GET /accounts/{accountId}
Authorization: Bearer {access_token}
X-Client-ID: your_client_id

### Response
Status: 200 OK
{
  "accountId": "string",
  "accountType": "string",
  "accountSubType": "string",
  "accountName": "string",
  "status": "string",
  "openedDate": "date",
  "currency": "string",
  "balances": {
    "current": "number",
    "available": "number",
    "hold": "number"
  },
  "routingNumber": "string",
  "maskedAccountNumber": "string",
  "owners": [
    {
      "customerId": "string",
      "name": "string",
      "relationship": "string"
    }
  ],
  "metadata": {
    "lastTransactionDate": "datetime",
    "lastUpdated": "datetime"
  }
}

### Field Descriptions:
### Field Descriptions

| Field                     | Type     | Description                          | Required | Values/Format           | Example                  |
|---------------------------|----------|--------------------------------------|----------|-------------------------|--------------------------|
| `accountId`               | string   | Unique account identifier            | Yes      | 5-20 alphanumeric chars | "acct_67890"             |
| `accountType`             | string   | Primary classification               | Yes      | `CHECKING`, `SAVINGS`   | "SAVINGS"                |
| `currentBalance`          | number   | Ledger balance (USD)                 | No       | Decimal (2 places)      | 4523.78                  |
| `openedDate`              | string   | Account opening date                 | No       | YYYY-MM-DD              | "2023-01-15"             |
| `status`                  | string   | Current account state                | Yes      | `ACTIVE`, `CLOSED`      | "ACTIVE"                 |
| `owners[].relationship`   | string   | Customer's relationship to account   | No       | `PRIMARY`, `SECONDARY`  | "PRIMARY"                |
| `lastUpdated`             | string   | Timestamp of last update             | No       | ISO 8601 format         | "2023-06-25T08:15:42Z"   |

