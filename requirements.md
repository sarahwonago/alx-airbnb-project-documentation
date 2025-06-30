# Airbnb Clone – Feature Requirements Specification

## Objective
This document outlines the technical and functional requirements for key backend features of the Airbnb Clone project. It includes API specifications, data formats, validation rules, and performance considerations.

---

## Feature 1: User Authentication

### Functional Requirements
- Allow users to register as guests or hosts
- Authenticate users via email and password
- Support OAuth (e.g., Google login)

### API Endpoints
- `POST /api/auth/register`
- `POST /api/auth/login`
- `POST /api/auth/logout`
- `GET /api/auth/profile`

### Input Specifications
#### Register:
```json
{
  "first_name": "Grace",
  "last_name": "Mwangi",
  "email": "grace@example.com",
  "password": "password123",
  "role": "guest"
}
```

#### Login:
```json
{
  "email": "grace@example.com",
  "password": "password123"
}
```

### Output (Success):
```json
{
  "token": "<JWT_TOKEN>",
  "user": {
    "id": "UUID",
    "first_name": "Grace",
    "role": "guest"
  }
}
```

### Validation Rules
- Email must be unique and valid
- Password minimum length: 8 characters
- Role must be one of: `guest`, `host`

### Performance Criteria
- Response time: < 300ms on successful login
- Token expiry: 1 hour

---

## Feature 2: Property Management

### Functional Requirements
- Hosts can create, update, delete, and view property listings
- Include images, location, amenities, and availability

### API Endpoints
- `POST /api/properties`
- `GET /api/properties`
- `GET /api/properties/:id`
- `PUT /api/properties/:id`
- `DELETE /api/properties/:id`

### Input Specifications (Create Listing):
```json
{
  "name": "Ocean View Villa",
  "description": "Beautiful beachfront villa",
  "location": "Diani, Kenya",
  "pricepernight": 15000,
  "amenities": ["Wi-Fi", "Pool", "Air Conditioning"]
}
```

### Output (Success):
```json
{
  "id": "UUID",
  "host_id": "UUID",
  "created_at": "timestamp"
}
```

### Validation Rules
- Name and location required
- Price must be a positive decimal
- Description max: 1000 characters

### Performance Criteria
- Search and filter should respond < 500ms
- Paginate results for better performance

---

## Feature 3: Booking System

### Functional Requirements
- Guests can book properties for specific dates
- Hosts and guests can view/cancel bookings
- Prevent overlapping bookings

### API Endpoints
- `POST /api/bookings`
- `GET /api/bookings/:id`
- `GET /api/bookings/user/:userId`
- `DELETE /api/bookings/:id`

### Input Specifications (Create Booking):
```json
{
  "property_id": "UUID",
  "start_date": "2025-08-10",
  "end_date": "2025-08-15"
}
```

### Output (Success):
```json
{
  "booking_id": "UUID",
  "status": "pending",
  "total_price": 75000
}
```

### Validation Rules
- Dates must be in the future and valid format
- End date > Start date
- No booking if date range overlaps

### Performance Criteria
- Booking creation: < 400ms with availability check
- Response should include total price and status

---


