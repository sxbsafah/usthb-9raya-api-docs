---
title: Authentication Routes
description: Minimal, route-focused docs for Auth endpoints.
---

# Authentication

- Base Path: `/auth`

## GET `/`

- Auth: None
- Request: none
- Validation: none
- Success: `200` `{ message, status: "ok" }`
- Errors: `500` on unexpected server errors

## POST `/register`

- Auth: None
- Request Body (JSON): `{ username, email, firstName, lastName, password }`
- Validation:
  - `username`: string, required, length 3–20, unique
  - `email`: string, required, valid email, unique
  - `firstName`: string, required, length 2–30
  - `lastName`: string, required, length 2–30
  - `password`: string, required, ≥6, must include uppercase, lowercase, digit, special char
- Success: `201` user created + token (exact shape from controller)
- Errors:
  - `400` validation errors array (from `validateRequest`)
  - `409` if username/email already in use
  - `500` unexpected server errors

## POST `/login`

- Auth: None
- Request Body (JSON): `{ email? , username? , password }` (email or username required)
- Validation:
  - `email`: optional string, required if used, valid email
  - `username`: optional string, required if used
  - `password`: string, required
- Success: `200` login success + token
- Errors:
  - `400` validation errors array
  - `401` invalid credentials
  - `500` unexpected server errors

## GET `/logout`

- Auth: `authenticate("user")` required
- Request: none
- Validation: auth token must be valid
- Success: `200` logout success
- Errors:
  - `401` missing/invalid token
  - `500` unexpected server errors
