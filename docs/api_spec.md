# API Contract Specification

Base URL: `/api/v1`

## Authentication
- `POST /auth/register`
  - Input: `{ email, password, full_name }`
  - Output: 201 Created `{ id, email, full_name }`
- `POST /auth/login`
  - Input: `{ email, password }`
  - Output: 200 OK `{ access_token, token_type: "bearer" }`

## Classes
- `GET /classes`
  - Headers: `Authorization: Bearer <token>`
  - Output: 200 OK `[ { id, title, coach_name, capacity, start_time } ]`

## Bookings
- `POST /bookings`
  - Headers: `Authorization: Bearer <token>`
  - Input: `{ class_id }`
  - Output: 201 Created `{ booking_id, status: "confirmed" }`
  - Error: 400 Bad Request (Class Full), 409 Conflict (Already booked)