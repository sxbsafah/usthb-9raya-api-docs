---
title: Contributions & Resources Routes
description: Endpoints for contributions and their resources.
---

# Contributions

- Base Path: `/contributions`

## GET `/`

- Auth: None
- Request: none
- Validation: none
- Success: `200` list of contributions
- Errors: `500` unexpected server errors

## GET `/my/all`

- Auth: `authenticate("user")`
- Request: none
- Validation: token must be valid
- Success: `200` list of current user's contributions
- Errors: `401` unauthorized, `500` server errors

## GET `/pending`

- Auth: `authenticate("admin")`
- Request: none
- Validation: token must be valid (admin)
- Success: `200` list of pending contributions
- Errors: `401`/`403` unauthorized, `500` server errors

## GET `/:id`

- Auth: None
- Request Params: `{ id }`
- Validation:
  - `id`: MongoId, must exist in DB
- Success: `200` contribution
- Errors: `400` validation errors, `404` not found, `500` server errors

## POST `/`

- Auth: `authenticate("user")`
- Request: `multipart/form-data`
  - Fields: `description` (text), `files[]` (up to 10)
- Validation:
  - `description`: string, required, length 10–500
  - `files`: max 10, each ≤25MB; allowed types: pdf, jpg, jpeg, png
- Success: `201` contribution created with uploaded resources
- Errors: `400` validation errors, `401` unauthorized, `413` payload too large, `415` unsupported media type, `500` server errors

## PUT `/:id`

- Auth: `authenticate("user")`
- Request Params: `{ id }`
- Request: `multipart/form-data`
  - Fields: optional `files[]` (up to 10)
- Validation:
  - `id`: MongoId, must exist in DB
  - `files`: max 10, each ≤25MB; allowed types: pdf, jpg, jpeg, png
- Success: `200` contribution updated (resources may be added)
- Errors: `400` validation errors, `401` unauthorized, `404` not found, `413`/`415`, `500`

## DELETE `/:id`

- Auth: `authenticate("user")`
- Request Params: `{ id }`
- Validation:
  - `id`: MongoId, must exist in DB
- Success: `200` contribution deleted
- Errors: `400` validation errors, `401` unauthorized, `404` not found, `500`

# Resources

- Base Path: `/contributions/resources`

## GET `/all`

- Auth: None
- Request: none
- Validation: none
- Success: `200` list of all resources
- Errors: `500` server errors

## GET `/user/:userId`

- Auth: None
- Request Params: `{ userId }`
- Validation: none (controller filters by user)
- Success: `200` resources for user
- Errors: `404` not found, `500` server errors

## GET `/my`

- Auth: `authenticate("user")`
- Request: none
- Validation: token must be valid
- Success: `200` current user's resources
- Errors: `401` unauthorized, `500` server errors

## GET `/contributions/:id/resources`

- Auth: None
- Request Params: `{ id }`
- Validation:
  - `id`: MongoId, must exist in DB
- Success: `200` resources for contribution
- Errors: `400` validation errors, `404` not found, `500`

## PUT `/resource/:resourceId`

- Base Path: `/contributions`
- Auth: `authenticate("user")`
- Request Params: `{ resourceId }`
- Request: `multipart/form-data`
  - Field: `file` (single)
- Validation:
  - `resourceId`: MongoId, must exist in DB
  - `file`: ≤25MB; types: pdf, jpg, jpeg, png
- Success: `200` resource file replaced/updated
- Errors: `400` validation errors, `401` unauthorized, `404` not found, `413`/`415`, `500`

## PATCH `/resource/:resourceId/status`

- Base Path: `/contributions`
- Auth: `authenticate("admin")`
- Request Params: `{ resourceId }`
- Request Body (JSON): `{ status }`
- Validation:
  - `resourceId`: MongoId, must exist in DB
  - `status`: string, required, must be `approved` or `rejected`
- Success: `200` resource status updated
- Errors: `400` validation errors, `401`/`403` unauthorized, `404` not found, `500`
