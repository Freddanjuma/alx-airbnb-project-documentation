# Technical and Functional Requirements

This document outlines the backend requirements for three key features of the Airbnb Project: **User Authentication**, **Property Management**, and **Booking System**.

---

## 1. User Authentication

### Functional Requirements
- Users can register with an email and password.
- Users can log in and log out securely.
- Passwords must be hashed before saving.
- JWT tokens are used for session management.

### API Endpoints
| Method | Endpoint | Description |
|--------|-----------|-------------|
| POST | `/api/register/` | Register a new user |
| POST | `/api/login/` | Authenticate user and return JWT |
| POST | `/api/logout/` | Invalidate user session |

### Input / Output Specification
**Input (Register):**
```json
{
  "email": "user@example.com",
  "password": "password123"
}

Output (Success):

{
  "message": "User registered successfully",
  "user_id": 12
}

Validation Rules

Email must be unique and valid.

Password must be at least 8 characters long.

Performance Criteria

Registration and login responses should complete within 1.5 seconds.

Token validation must be stateless and efficient.

2. Property Management
Functional Requirements

Hosts can add, update, or delete their property listings.

Guests can view all available properties.

Images can be uploaded and linked to listings.

API Endpoints
Method	Endpoint	Description
GET	/api/properties/	List all properties
POST	/api/properties/	Create a new property (Host only)
PUT	/api/properties/{id}/	Update property details
DELETE	/api/properties/{id}/	Remove property listing
Input / Output Specification

Input (Create Property):

{
  "title": "Modern Apartment",
  "location": "Accra",
  "price_per_night": 80.00,
  "description": "Fully furnished with Wi-Fi and AC"
}


Output (Success):

{
  "message": "Property created successfully",
  "property_id": 21
}

Validation Rules

All fields required.

Price must be a positive number.

Performance Criteria

Property search queries should complete in under 2 seconds.

Image uploads handled asynchronously.

3. Booking System
Functional Requirements

Guests can book available properties.

Prevent double-booking of the same property.

Hosts can view and manage their bookings.

API Endpoints
Method	Endpoint	Description
POST	/api/bookings/	Create a booking
GET	/api/bookings/{user_id}/	Retrieve all bookings for a user
DELETE	/api/bookings/{id}/	Cancel a booking
Input / Output Specification

Input (Booking):

{
  "property_id": 21,
  "check_in": "2025-11-10",
  "check_out": "2025-11-14"
}


Output (Success):

{
  "message": "Booking confirmed",
  "booking_id": 56
}

Validation Rules

Check-in date must be before check-out date.

Property must not already be booked for the given dates.

Performance Criteria

Booking confirmation should be completed in under 3 seconds.

Concurrency-safe database transactions to avoid double-booking.

4. Security and Data Protection

HTTPS for all API endpoints.

Secure password storage (bcrypt).

Token-based authentication.

Compliance with GDPR for user data handling.