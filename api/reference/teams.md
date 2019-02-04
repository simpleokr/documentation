---
layout: page
title: Teams
parent: API Reference
grand_parent: Developer API
nav_order: 3
has_toc: true
---

# Teams
{: .no_toc }

Team objects are used to group users into teams.

## Table of Contents
{: .no_toc .text-delta}

- TOC
{:toc}


## The team object

| Attribute | Type   | Description            |
|-----------|--------|------------------------|
| id        | string | Unique team identifier |
| name      | string | Team name              |
| created_at | string | Time when the team was created. RFC 3339 format. |

Example:

```json
{
  "id": "16682617-f25d-4df2-9f51-3c38298996b8",
  "name": "Product Engineering",
  "created_at": "2018-02-20T12:32:56Z"
}
```

## Create a team

Create a new team object.

### Request
{: .no_toc }

```
POST /v1/teams
```

Request object:

| Attribute | Type | Description |
|-----------|------|-------------|
| name | string, optional | Team name |

Example:

```json
{
  "name": "Product Engineering"
}
```

### Response
{: .no_toc }

Returns a newly created team object.

## List all teams

Returns a list of your teams.

### Request
{: .no_toc }

```
GET /v1/teams
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
| teams | list | A list of team objects |

Example:

```json
{
  "next_page_token": null,
  "teams": [
    {
      "id": "16682617-f25d-4df2-9f51-3c38298996b8",
      "name": "Product Engineering",
      "created_at": "2018-02-20T12:32:56Z"
    },
    {...},
    {...}
  ]
}
```

## Retrieve a team

Retrieve details about the existing team. Supply the unique team ID from either
a team creation response or team list.

### Request
{: .no_toc }

```
GET /v1/teams/:id
```

Request arguments:

| Argument | Type |  Description |
|----------|------|--------------|
| id | string | Team identifier |

### Response
{: .no_toc }

Returns a team object on success.

## Update a team

Update details of an existing team.

### Request
{: .no_toc }


```
POST /v1/teams/:id
```

Request arguments:

| Argument | Type |  Description |
|----------|------|--------------|
| id | string | Team identifier |

Request object:

| Attribute | Type |  Description |
|----------|------|--------------|
| name | string | New team name to be set |

### Response
{: .no_toc }

Returns an updated team object.

## Delete a team

Delete an existing team.

### Request
{: .no_toc }

```
DELETE /v1/teams/:id
```

Request arguments:

| Argument | Type |  Description |
|----------|------|--------------|
| id | string | Identifier of a team to be deleted |

### Response
{: .no_toc }

Returns a 200 HTTP response on success.
