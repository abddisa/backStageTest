# Share Holder Info API

The **Share Holder Info API** provides detailed information about shareholders based on their unique shareholder number.

---

## Overview

This API allows internal and external systems to retrieve complete shareholder details in a standardized format.  
It is designed for integration into financial platforms, compliance systems, and reporting tools.

---

## Features

- **Lookup by Shareholder Number** – Retrieve full details for a specific shareholder.
- **JSON Response Format** – Easily consumable by various applications.
- **Real-Time Data** – Always returns the latest available shareholder information.
- **Secure Access** – Supports authentication for authorized users only.

---

### Endpoint
GET /api/shareholder/{shareholderNumber}


### Path Parameters

| Parameter         | Type   | Required | Description                             |
|-------------------|--------|----------|-----------------------------------------|
| shareholderNumber | string | Yes      | Unique identifier for the shareholder. |

---

## Example Request

```bash
curl -X GET "https://api.example.com/api/shareholder/SH12345" \
  -H "Authorization: Bearer <token>"


## Request

Success (200 OK)
{
  "shareholderNumber": "SH12345",
  "fullName": "John Doe",
  "dateOfBirth": "1980-05-15",
  "nationality": "Ethiopian",
  "shareCount": 1500,
  "contact": {
    "email": "johndoe@example.com",
    "phone": "+251912345678"
  }
}

Not Found (404)
{
  "error": "Shareholder not found"
}








