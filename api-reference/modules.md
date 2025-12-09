---
title: Modules Routes
description: CRUD endpoints and listing by faculty.
---

# Modules

- Base Path: `/modules`

## GET `/`

- Auth: None
- Request: none
- Validation: none
- Success: `200` list of modules
- Errors: `500`

## GET `/faculty/:facultyId`

- Auth: None
- Params:

```json
{
  "facultyId": "<facultyId>"
}
```

- Validation:
  - `facultyId`: MongoId, must exist
- Success: `200` modules for faculty
- Errors: `400` validation, `404` not found, `500`

## GET `/:id`

- Auth: None
- Params:

```json
{
  "id": "<moduleId>"
}
```

- Validation:
  - `id`: MongoId, must exist
- Success: `200` module
- Errors: `400` validation, `404` not found, `500`

## POST `/`

- Auth: `authenticate("admin")`
- Request Body (JSON):

```json
{
  "name": "Algorithms",
  "facultyId": "<facultyId>"
}
```

- Validation:
  - `name`: string, required, length 2–100, unique
  - `facultyId`: MongoId, required, must exist
- Success: `201` created
- Errors: `400` validation, `401`/`403`, `404` faculty not found, `409` conflict, `500`

## PUT `/:id`

- Auth: `authenticate("admin")`
- Params:

```json
{
  "id": "<moduleId>"
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
  "id": "<moduleId>"
}
```

- Validation:
  - `id`: MongoId, must exist
- Success: `200` deleted
- Errors: `400` validation, `401`/`403`, `404` not found, `500`
