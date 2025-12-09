---
title: SubModules Routes
description: CRUD endpoints for submodules and listing by module.
---

# SubModules

- Base Path: `/submodules`

## GET `/`

- Auth: None
- Request: none
- Validation: none
- Success: `200` list of submodules
- Errors: `500` unexpected server errors

## GET `/module/:moduleId`

- Auth: None
- Request Params: `{ moduleId }`
- Validation:
  - `moduleId`: MongoId, must exist in DB
- Success: `200` submodules for module
- Errors:
  - `400` validation errors
  - `404` module not found
  - `500` unexpected server errors

## GET `/:id`

- Auth: None
- Request Params: `{ id }`
- Validation:
  - `id`: MongoId, must exist in DB
- Success: `200` submodule
- Errors:
  - `400` validation errors
  - `404` not found
  - `500` unexpected server errors

## POST `/`

- Auth: `authenticate("admin")`
- Request Body (JSON): `{ name, moduleId }`
- Validation:
  - `name`: string, required, length 2–100, unique
  - `moduleId`: MongoId, required, must exist in DB
- Success: `201` created submodule
- Errors:
  - `400` validation errors
  - `401`/`403` unauthorized
  - `409` name already in use
  - `404` module not found
  - `500` unexpected server errors

## PUT `/:id`

- Auth: `authenticate("admin")`
- Request Params: `{ id }`
- Validation:
  - `id`: MongoId, must exist in DB
- Success: `200` updated submodule
- Errors:
  - `400` validation errors
  - `401`/`403` unauthorized
  - `404` not found
  - `500` unexpected server errors

## DELETE `/:id`

- Auth: `authenticate("admin")`
- Request Params: `{ id }`
- Validation:
  - `id`: MongoId, must exist in DB
- Success: `200` deleted confirmation
- Errors:
  - `400` validation errors
  - `401`/`403` unauthorized
  - `404` not found
  - `500` unexpected server errors
