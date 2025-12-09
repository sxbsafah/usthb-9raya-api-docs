---
title: Contributions & Resources Routes
description: Multipart requests highlighted with JSON examples and validations.
---

# Contributions

- Base Path: `/contributions`

## GET `/`

- Auth: None
- Request: none
- Validation: none
- Success: `200` list of contributions
- Errors: `500`

## GET `/my/all`

- Auth: `authenticate("user")`
- Request: none
- Validation: token must be valid
- Success: `200` my contributions
- Errors: `401`, `500`

## GET `/pending`

- Auth: `authenticate("admin")`
- Request: none
- Validation: admin token must be valid
- Success: `200` pending contributions
- Errors: `401`/`403`, `500`

## GET `/:id`

- Auth: None
- Params:

```json
{
  "id": "<contributionId>"
}
```

- Validation:
  - `id`: MongoId, must exist
- Success: `200` contribution
- Errors: `400`, `404`, `500`

## POST `/` (multipart/form-data)

- Auth: `authenticate("user")`
- Content-Type: `multipart/form-data`
- Fields:
  - `description` (text)
  - `files[]` (up to 10)
- Example (JSON representation of fields):

```json
{
  "description": "Lecture notes and slides",
  "files": ["<binary>", "<binary>"]
}
```

- Validation:
  - `description`: string, required, length 10–500
  - `files`: max 10, each ≤25MB; allowed: pdf, jpg, jpeg, png
- Success: `201` created with resources
- Errors: `400` validation, `401` unauthorized, `413` too large, `415` unsupported, `500`

## PUT `/:id` (multipart/form-data)

- Auth: `authenticate("user")`
- Params:

```json
{
  "id": "<contributionId>"
}
```

- Content-Type: `multipart/form-data`
- Fields (optional):
  - `files[]` (up to 10)
- Example:

```json
{
  "files": ["<binary>"]
}
```

- Validation:
  - `id`: MongoId, must exist
  - `files`: max 10, each ≤25MB; allowed: pdf, jpg, jpeg, png
- Success: `200` updated
- Errors: `400`, `401`, `404`, `413`/`415`, `500`

## DELETE `/:id`

- Auth: `authenticate("user")`
- Params:

```json
{
  "id": "<contributionId>"
}
```

- Validation:
  - `id`: MongoId, must exist
- Success: `200` deleted
- Errors: `400`, `401`, `404`, `500`

# Resources

- Base Path: `/contributions/resources`

## GET `/all`

- Auth: None
- Request: none
- Validation: none
- Success: `200` resources
- Errors: `500`

## GET `/user/:userId`

- Auth: None
- Params:

```json
{
  "userId": "<userId>"
}
```

- Validation: none
- Success: `200` resources by user
- Errors: `404`, `500`

## GET `/my`

- Auth: `authenticate("user")`
- Request: none
- Validation: token must be valid
- Success: `200` my resources
- Errors: `401`, `500`

## GET `/contributions/:id/resources`

- Auth: None
- Params:

```json
{
  "id": "<contributionId>"
}
```

- Validation:
  - `id`: MongoId, must exist
- Success: `200` resources for contribution
- Errors: `400`, `404`, `500`

## PUT `/resource/:resourceId` (multipart/form-data)

- Base Path: `/contributions`
- Auth: `authenticate("user")`
- Params:

```json
{
  "resourceId": "<resourceId>"
}
```

- Content-Type: `multipart/form-data`
- Fields:
  - `file` (single)
- Example:

```json
{
  "file": "<binary>"
}
```

- Validation:
  - `resourceId`: MongoId, must exist
  - `file`: ≤25MB; allowed: pdf, jpg, jpeg, png
- Success: `200` resource updated
- Errors: `400`, `401`, `404`, `413`/`415`, `500`

## PATCH `/resource/:resourceId/status`

- Base Path: `/contributions`
- Auth: `authenticate("admin")`
- Params:

```json
{
  "resourceId": "<resourceId>"
}
```

- Request Body (JSON):

```json
{
  "status": "approved"
}
```

- Validation:
  - `resourceId`: MongoId, must exist
  - `status`: `approved` or `rejected`
- Success: `200` status updated
- Errors: `400`, `401`/`403`, `404`, `500`
