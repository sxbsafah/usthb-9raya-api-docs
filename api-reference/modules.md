---
title: Modules Routes
description: CRUD endpoints for modules and listing by faculty.
---

# Modules

- Base Path: `/modules`

## GET `/`

- Auth: None
- Request: none
- Validation: none
- Success: `200` list of modules
- Errors: `500` unexpected server errors

## GET `/faculty/:facultyId`

- Auth: None
- Request Params: `{ facultyId }`
- Validation:
  - `facultyId`: MongoId, must exist in DB
- Success: `200` modules for faculty
- Errors:
  - `400` validation errors
  - `404` faculty not found
  - `500` unexpected server errors

## GET `/:id`

- Auth: None
- Request Params: `{ id }`
- Validation:
  - `id`: MongoId, must exist in DB
- Success: `200` module
- Errors:
  - `400` validation errors
  - `404` not found
  - `500` unexpected server errors

## POST `/`

- Auth: `authenticate("admin")`
- Request Body (JSON): `{ name, facultyId }`
- Validation:
  - `name`: string, required, length 2–100, unique
  - `facultyId`: MongoId, required, must exist in DB
- Success: `201` created module
- Errors:
  - `400` validation errors
  - `401`/`403` unauthorized
  - `409` name already in use
  - `404` faculty not found
  - `500` unexpected server errors

## PUT `/:id`

- Auth: `authenticate("admin")`
- Request Params: `{ id }`
- Validation:
  - `id`: MongoId, must exist in DB
- Success: `200` updated module
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
