---
title: Account Inquiry API
description: Retrieve account information including balances, details, and customer relationships
---

# Account Inquiry API

## Overview

The Account Inquiry API provides secure, programmatic access to account information for authorized applications. This RESTful API enables developers to retrieve account details, balances, and customer-account relationships while maintaining strict security and compliance standards.

![API Flow Diagram](https://example.com/images/account-inquiry-flow.png)

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


