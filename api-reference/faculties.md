---
title: Faculties Routes
description: CRUD endpoints with JSON bodies and validations.
---

# Faculties

- Base Path: `/faculties`

## GET `/`

- Auth: None
- Request: none
- Validation: none
- Success: `200` list of faculties
- Errors: `500` server errors

## GET `/:id`

- Auth: None
- Params:

```json
{
  "id": "<facultyId>"
}
```

- Validation:
  - `id`: MongoId, must exist
- Success: `200` faculty
- Errors: `400` validation, `404` not found, `500`

## POST `/`

- Auth: `authenticate("admin")`
- Request Body (JSON):

```json
{
  "name": "Computer Science"
}
```

- Validation:
  - `name`: string, required, length 2–100, unique
- Success: `201` created
- Errors: `400` validation, `401`/`403` unauthorized, `409` conflict, `500`

## PUT `/:id`

- Auth: `authenticate("admin")`
- Params:

```json
{
  "id": "<facultyId>"
}
```

- Validation:
  - `id`: MongoId, must exist
- Success: `200` updated
- Errors: `400` validation, `401`/`403`, `404` not found, `500`

## DELETE `/:id`

- Auth: `authenticate("admin")`
- Params:

```json
{
  "id": "<facultyId>"
}
```

- Validation:
  - `id`: MongoId, must exist
- Success: `200` deleted
- Errors: `400` validation, `401`/`403`, `404` not found, `500`
