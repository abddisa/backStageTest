# API Responses

This section outlines the typical responses you can expect from the `GET /api/share/shareHolderInfo/getAll` endpoint of the Share Holder Info API.

---

## ✅ 200 OK — Success

Returned when the request completes successfully.

### Example Response

```json
[
  {
    "id": 1,
    "name": "John Doe",
    "shares": 1200.0
  },
  {
    "id": 2,
    "name": "Jane Smith",
    "shares": 950.5
  }
]
