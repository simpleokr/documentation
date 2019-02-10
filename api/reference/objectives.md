---
layout: page
title: Objectives
parent: API Reference
grand_parent: Developer API
nav_order: 4
has_toc: true
---

# Objectives
{: .no_toc }

Objectives let you capture company, team or personal goals as part of the OKR
process.

## Table of Contents
{: .no_toc .text-delta}

- TOC
{:toc}

## The objective object

| Attribute | Type   | Description            |
|-----------|--------|------------------------|
| id        | string | Unique objective identifier |
| name      | string | Name of the objective |
| created_at | string | Time when the objective was created. RFC 3339 format |
| modified_at | string | Time when the objective was last updated. RFC 3339 format |
| team_id | string, nullable | Unique team identifier. Indicates the team assigned to the objective |
| assignee_id | string, nullable | Unique user identifier. Indicates the user assigned to the objective |
| description | string, nullable | Description of the objective |
| is_personal | bool | Flag indicating whether this is a personal objective |
| is_company | bool | Flag indicating whether this is a company objective |
| parent_objective_id | string, nullable | Unique objective identifier. Indicates objective alignment |
| cycle_id | string | Unique delivery cycle identifier. Indicates the delivery cycle this objective belongs to |

Example:

```json
{
  "id": "16682617-f25d-4df2-9f51-3c38298996b8",
  "name": "Become best at OKRs",
  "created_at": "2018-02-20T12:32:56Z",
  "modified_at": "2018-02-20T12:32:56Z",
  "team_id": null,
  "assignee_id": null,
  "description": null,
  "is_personal": false,
  "is_company": true,
  "parent_objective_id": null,
  "cycle_id": "12345678-f25d-4df2-9f51-3c38298996b8"
}
```

## Create an objective

Create a new objective object.

### Request
{: .no_toc }

```
POST /v1/objectives
```

Request object:

| Attribute | Type | Description |
|-----------|------|-------------|
| name | string | Objective name |
| cycle_id | string | Delivery cycle identifier |
| description | string, optional | Objective description |
| team_id | string, optional | Team identifier |
| assignee_id | string, optional | User identifier |
| parent_objective_id | string, optional | Objective identifier |
| is_company | bool | Flag indicating whether this is a company objective |
| is_personal | bool | Flag indicating whether this is a personal objective |

Example:

```json
{
  "name": "Become best at OKRs",
  "cycle_id": "12345678-f25d-4df2-9f51-3c38298996b8",
  "description": null,
  "team_id": null,
  "assignee_id": null,
  "parent_objective_id": null,
  "is_company": true,
  "is_personal": false
}
```

### Response
{: .no_toc }

Returns a newly created objective object.

## List all objectives

Returns a list of your objectives.

### Request
{: .no_toc }

```
GET /v1/objectives
```

Request arguments:

| Argument | Type |  Description |
|----------|------|--------------|
| cycle_id | string | Cycle identifier |
| page_token | string, optional | Page identifier |

### Response
{: .no_toc }

Response object:

| Attribute | Type | Description |
|-----------|------|-------------|
| next_page_token | string, optional | Token for retrieving next page of results |
| objectives | list | A list of objective objects |

Example:

```json
{
  "next_page_token": null,
  "objectives": [
    {
      "name": "Become best at OKRs",
      "cycle_id": "12345678-f25d-4df2-9f51-3c38298996b8",
      "description": null,
      "team_id": null,
      "assignee_id": null,
      "parent_objective_id": null,
      "is_company": true,
      "is_personal": false
    },
    {...},
    {...}
  ]
}
```

## Retrieve an objective

Retrieve details about the objective. Supply the unique objective ID from
either a objective creation response or objective list.

### Request
{: .no_toc }

```
GET /v1/objectives/:id
```

Request arguments:

| Argument | Type |  Description |
|----------|------|--------------|
| id | string | Objective identifier |

### Response
{: .no_toc }

Returns an objective object.


## Update an objective

Update details of an objective.

### Request
{: .no_toc }

```
POST /v1/objectives/:id
```

Request arguments:

| Argument | Type |  Description |
|----------|------|--------------|
| id | string | Cycle identifier |

Request object:

Request body is an entire objective object with new values. Any omitted
attributes will inherit default false value of that particular type.


### Response
{: .no_toc }

Returns an updated objective object.

## Delete an objective

Delete an existing objective and all information associated with it.

### Request
{: .no_toc }

```
DELETE /v1/objectives/:id
```

Request arguments:

| Argument | Type |  Description |
|----------|------|--------------|
| id | string | Identifier of a objective to be deleted |

### Response
{: .no_toc }

Returns a 200 HTTP response on success.

## Add key result to an objective

Add a new key result to an objective.

### Request
{: .no_toc }

```
POST /v1/objectives/:id/keyresults
```

Request arguments:

| Argument | Type |  Description |
|----------|------|--------------|
| id | string | Identifier of a objective |

Request object:

Request body is a key result object.

### Response
{: .no_toc }

Returns a newly created key result object.

## List key results for an objective

Lists all key results for an objective.

### Request
{: .no_toc }

```
GET /v1/objectives/:id/keyresults
```

Request arguments:

| Argument | Type |  Description |
|----------|------|--------------|
| id | string | Identifier of a objective |

### Response
{: .no_toc }

Returns a list of key results associated with the objective.

Response object:

| Attribute | Type | Description |
|-----------|------|-------------|
| next_page_token | string, optional | Token for retrieving next page of results |
| keyresults | list | A list of key result objects |
