# {API_NAME} API Reference

> **Version:** {VERSION}
> **Last updated:** {DATE}
> **Base URL:** `{BASE_URL}`

## Overview

{Brief description of the API and its purpose.}

## Authentication

{Authentication method, required headers, token format.}

## Endpoints

### {METHOD} {PATH}

{Description of what this endpoint does.}

**Parameters**

| Name | Type | In | Required | Description |
|------|------|----|----------|-------------|
| {name} | {type} | {path/query/body} | {yes/no} | {description} |

**Request Example**

```{language}
{request code example}
```

**Response**

```json
{
  "status": "success",
  "data": {}
}
```

**Error Responses**

| Status | Code | Description |
|--------|------|-------------|
| 400 | {error_code} | {description} |
| 404 | {error_code} | {description} |

---

## Types

### {TypeName}

{Description of the type.}

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| {field} | {type} | {yes/no} | {description} |

## Error Codes

| Code | HTTP Status | Description | Resolution |
|------|-------------|-------------|------------|
| {code} | {status} | {description} | {what to do} |

## Rate Limits

{Rate limit policy, headers returned, and what happens when exceeded.}

## Versioning

{API versioning strategy, deprecation policy, and migration guidance.}

## Changelog

| Date | Version | Changes |
|------|---------|---------|
| {date} | {version} | {summary of changes} |
