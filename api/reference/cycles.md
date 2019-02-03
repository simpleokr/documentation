---
layout: page
title: Cycles
parent: API Reference
grand_parent: Developer API
nav_order: 3
has_toc: true
---

# Cycles
{: .no_toc }

Delivery cycles are used to organize objectives into time-bound groups.
Delivery cycle is how we track performance and progress of your OKRs.

## Table of Contents
{: .no_toc .text-delta}

- TOC
{:toc}

## The cycle object

| Attribute | Type   | Description            |
|-----------|--------|------------------------|
| id        | string | Unique delivery cycle identifier |
| name      | string | Name of the delivery cycle             |
| created_at | string | Time when the delivery cycle was created. RFC 3339 format. |

Example:

```json
{
  "id": "16682617-f25d-4df2-9f51-3c38298996b8",
  "name": "2019 Q1",
  "created_at": "2018-02-20T12:32:56Z"
}
```

## Create a cycle

Create a new delivery cycle object.

### Request
{: .no_toc }

```
POST /v1/cycles
```

Request object:

| Attribute | Type | Description |
|-----------|------|-------------|
| name | string, optional | Delivery cycle name |

Example:

```json
{
  "name": "2019 Q1"
}
```

### Response
{: .no_toc }

Returns a newly created delivery cycle object.

## List all cycles

Returns a list of your delivery cycles.

### Request
{: .no_toc }

```
GET /v1/cycles
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
| cycles | list | A list of cycle objects |

Example:

```json
{
  "next_page_token": null,
  "cycles": [
    {
      "id": "16682617-f25d-4df2-9f51-3c38298996b8",
      "name": "2019 Q1",
      "created_at": "2018-02-20T12:32:56Z"
    },
    {...},
    {...}
  ]
}
```


## Retrieve a cycle

Retrieve details about the existing delivery cycle. Supply the unique cycle ID from either
a cycle creation response or cycle list.

### Request
{: .no_toc }

```
GET /v1/cycles/:id
```

Request arguments:

| Argument | Type |  Description |
|----------|------|--------------|
| id | string | Cycle identifier |

### Response
{: .no_toc }

Returns a delivery cycle object.


## Update a cycle

Update details of an existing cycle.

### Request
{: .no_toc }

```
POST /v1/cycles/:id
```

Request arguments:

| Argument | Type |  Description |
|----------|------|--------------|
| id | string | Cycle identifier |

Request object:

| Attribute | Type |  Description |
|----------|------|--------------|
| name | string | New cycle name to be set |

### Response
{: .no_toc }

Returns an updated delivery cycle object.

## Delete a cycle

Delete an existing delivery cycle and all objectives associated with it.

### Request
{: .no_toc }

```
DELETE /v1/cycles/:id
```

Request arguments:

| Argument | Type |  Description |
|----------|------|--------------|
| id | string | Identifier of a cycle to be deleted |

### Response
{: .no_toc }

Returns a 200 HTTP response on success.
