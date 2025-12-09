---
title: Authentication Routes
description: Clean, minimal docs with JSON request bodies.
---

# Authentication

- Base Path: `/auth`

## GET `/`

- Auth: None
- Request: none
- Validation: none
- Success: `200` `{ message, status: "ok" }`
- Errors: `500` unexpected server errors

## POST `/register`

- Auth: None
- Request Body (JSON):

```json
{
  "username": "john_doe",
  "email": "john@example.com",
  "firstName": "John",
  "lastName": "Doe",
  "password": "P@ssw0rd!"
}
```

- Validation:
  - `username`: string, required, length 3–20, unique
  - `email`: string, required, valid email, unique
  - `firstName`: string, required, length 2–30
  - `lastName`: string, required, length 2–30
  - `password`: string, required, ≥6, must include uppercase, lowercase, digit, special char
- Success: `201` user created + token
- Errors: `400` validation errors, `409` conflict, `500` server errors

## POST `/login`

- Auth: None
- Request Body (JSON):

```json
{
  "email": "john@example.com",
  "password": "P@ssw0rd!"
}
```

- or -

```json
{
  "username": "john_doe",
  "password": "P@ssw0rd!"
}
```

- Validation:
  - `email`: optional string, valid if provided
  - `username`: optional string, valid if provided
  - `password`: string, required
- Success: `200` login success + token
- Errors: `400` validation errors, `401` invalid credentials, `500` server errors

## GET `/logout`

- Auth: `authenticate("user")`
- Request: none
- Validation: token must be valid
- Success: `200` logout success
- Errors: `401` unauthorized, `500` server errors
