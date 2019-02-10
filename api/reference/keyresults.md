---
layout: page
title: Key Results
parent: API Reference
grand_parent: Developer API
nav_order: 5
has_toc: true
---

# Key Results
{: .no_toc }

Key results are quantitative metrics that let you track Objective's performance.

## Table of Contents
{: .no_toc .text-delta}

- TOC
{:toc}

## The key result object

| Attribute | Type   | Description            |
|-----------|--------|------------------------|
| id        | string | Unique key result identifier. |
| name      | string | Name of the key result. |
| created_at | string | Time when the key result was created. RFC 3339 format. |
| modified_at | string | Time when the key result was last updated. RFC 3339 format. |
| objective_id | string | Objective identifier. |
| confidence | string | Decimal string between 0.0 and 1.0 indicating confidence of reaching the target. |
| type | string | Metric type. One of `milestone`, `baseline`, `range`, `positive`, `negative`. |
| current_value | string | Decimal. Current metric value. |
| target_value_min | string, nullable | Decimal. Minimum target value. |
| target_value_max | string, nullable | Decimal. Maximum target value. |

Target values are optional for some metric types.

- `postive` and `negative` metrics will have only `target_value_min` set.
- `range` metrics will have both `target_value_min` and `target_value_max` set.
- `baseline` will not have either of the target values set.
- `milestone` will always have `target_value_min` set to `1.00`.

Example:

```json
{
  "id": "16682617-f25d-4df2-9f51-3c38298996b8",
  "name": "$40K in revenue from subscription sales",
  "created_at": "2018-02-20T12:32:56Z",
  "modified_at": "2018-02-20T12:32:56Z",
  "objective_id": "12345678-f25d-4df2-9f51-3c38298996b8",
  "type": "positive",
  "confidence": "0.50",
  "current_value": "10000.00",
  "target_value_min": "40000.00",
  "target_value_max": null
}
```

## List all key results

Returns a list of your key results.

### Request
{: .no_toc }

```
GET /v1/keyresults
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
| keyresults | list | A list of key result objects |

Example:

```json
{
  "next_page_token": null,
  "keyresults": [
    {
      "id": "16682617-f25d-4df2-9f51-3c38298996b8",
      "name": "$40K in revenue from subscription sales",
      "created_at": "2018-02-20T12:32:56Z",
      "modified_at": "2018-02-20T12:32:56Z",
      "objective_id": "12345678-f25d-4df2-9f51-3c38298996b8",
      "type": "positive",
      "confidence": "0.50",
      "current_value": "10000.00",
      "target_value_min": "40000.00",
      "target_value_max": null
    },
    {...},
    {...}
  ]
}
```

## Retrieve an key result

Retrieve details about the key result. Supply the unique key result ID from
either a key result creation response or key result list.

### Request
{: .no_toc }

```
GET /v1/keyresults/:id
```

Request arguments:

| Argument | Type |  Description |
|----------|------|--------------|
| id | string | Key result identifier |

### Response
{: .no_toc }

Returns an key result object.


## Update an key result

Update details of an key result.

### Request
{: .no_toc }

```
POST /v1/keyresults/:id
```

Request arguments:

| Argument | Type |  Description |
|----------|------|--------------|
| id | string | Key result identifier |

Request object:

Request body is an entire key result object with new values. Any omitted
attributes will inherit default false value of that particular type.


### Response
{: .no_toc }

Returns an updated key result object.

## Delete a key result

Delete an existing key result and all information associated with it.

### Request
{: .no_toc }

```
DELETE /v1/keyresults/:id
```

Request arguments:

| Argument | Type |  Description |
|----------|------|--------------|
| id | string | Identifier of a key result to be deleted |

### Response
{: .no_toc }

Returns a 200 HTTP response on success.
