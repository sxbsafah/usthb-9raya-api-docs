---
title: SubModules Routes
description: CRUD endpoints and listing by module.
---

# SubModules

- Base Path: `/submodules`

## GET `/`

- Auth: None
- Request: none
- Validation: none
- Success: `200` list of submodules
- Errors: `500`

## GET `/module/:moduleId`

- Auth: None
- Params:

```json
{
  "moduleId": "<moduleId>"
}
```

- Validation:
  - `moduleId`: MongoId, must exist
- Success: `200` submodules for module
- Errors: `400` validation, `404` not found, `500`

## GET `/:id`

- Auth: None
- Params:

```json
{
  "id": "<subModuleId>"
}
```

- Validation:
  - `id`: MongoId, must exist
- Success: `200` submodule
- Errors: `400` validation, `404` not found, `500`

## POST `/`

- Auth: `authenticate("admin")`
- Request Body (JSON):

```json
{
  "name": "Data Structures",
  "moduleId": "<moduleId>"
}
```

- Validation:
  - `name`: string, required, length 2–100, unique
  - `moduleId`: MongoId, required, must exist
- Success: `201` created
- Errors: `400` validation, `401`/`403`, `404` module not found, `409` conflict, `500`

## PUT `/:id`

- Auth: `authenticate("admin")`
- Params:

```json
{
  "id": "<subModuleId>"
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
  "id": "<subModuleId>"
}
```

- Validation:
  - `id`: MongoId, must exist
- Success: `200` deleted
- Errors: `400` validation, `401`/`403`, `404` not found, `500`
