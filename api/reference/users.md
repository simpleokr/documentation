---
layout: page
title: Users
parent: API Reference
grand_parent: Developer API
nav_order: 1
has_toc: true
---

# Users
{: .no_toc }

User object holds information about a user of an organization.

## Table of Contents
{: .no_toc .text-delta}

- TOC
{:toc}


## The user object

| Attribute | Type   | Description            |
|-----------|--------|------------------------|
| id        | string | Unique user identifier |
| name      | string | Full name of the user  |
| email     | string | Email address associated with the user |
| is_active | bool   | Indicator whether the user is active or not. Inactive users cannot sign into Simple OKR.              |
| created_at | string | Time when the user was created. RFC 3339 format. |

Example:

```json
{
  "id": "16682617-f25d-4df2-9f51-3c38298996b8",
  "name": "John Doe",
  "email": "email@example.com",
  "is_active": true,
  "created_at": "2018-02-20T12:32:56Z"
}
```

## List all users

Returns a list of your users.

### Request
{: .no_toc }

```
GET /v1/users
```

Request arguments:

| Argument | Type |  Description |
|----------|------|--------------|
| page_token | string, optional | Page identifier |

### Response
{: .no_toc }

Response object:

| Attribute | Type | Description |
|-----------|------|-------------|
| next_page_token | string, optional | Token for retrieving next page of results |
| users | list | A list of user objects |

Example:

```json
{
  "next_page_token": null,
  "users": [
    {
      "id": "16682617-f25d-4df2-9f51-3c38298996b8",
      "name": "John Doe",
      "email": "email@example.com",
      "is_active": true,
      "created_at": "2018-02-20T12:32:56Z"
    },
    {...},
    {...}
  ]
}
```

## Retrieve a user

Retrieve details about the existing user. Supply the unique user ID from a user
list response.

### Request
{: .no_toc }

```
GET /v1/users/:id
```

Request arguments:

| Argument | Type |  Description |
|----------|------|--------------|
| id | string | User identifier |

### Response
{: .no_toc }

Returns a user object on success.
