---
layout: page
title: Errors
parent: Developer API
---

# Errors

Simple OKR uses conventional HTTP response codes to indicate the success or
failure of an API request. In general: Codes in the `2xx` range indicate
success.  Codes in the `4xx` range indicate an error that failed given the
information provided (e.g., a required parameter was omitted). Codes in the
`5xx` range indicate an error with Simple OKR servers.

## Error response object

Errors returned by all Simple OKR APIs use the same error response structure:

| Attribute | Type | Description |
|-----------|------|-------------|
| code | integer | HTTP status code |
| message | string | Human readable error summary |
| details | object, optional | A free form object providing additional details about the error |

Example:

```json
{
  "code": 400,
  "message": "invalid request",
  "details": {
    "name": "name is required"
  }
}
```
