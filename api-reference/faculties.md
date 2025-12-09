---
title: Faculties Routes
description: CRUD endpoints for faculties with validations.
---

# Faculties

- Base Path: `/faculties`

## GET `/`

- Auth: None
- Request: none
- Validation: none
- Success: `200` list of faculties
- Errors: `500` unexpected server errors

## GET `/:id`

- Auth: None
- Request Params: `{ id }`
- Validation:
  - `id`: MongoId, must exist in DB
- Success: `200` faculty
- Errors:
  - `400` validation errors
  - `404` not found
  - `500` unexpected server errors

## POST `/`

- Auth: `authenticate("admin")`
- Request Body (JSON): `{ name }`
- Validation:
  - `name`: string, required, length 2–100, unique
- Success: `201` created faculty
- Errors:
  - `400` validation errors
  - `401`/`403` unauthorized
  - `409` name already in use
  - `500` unexpected server errors

## PUT `/:id`

- Auth: `authenticate("admin")`
- Request Params: `{ id }`
- Validation:
  - `id`: MongoId, must exist in DB
- Success: `200` updated faculty
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
