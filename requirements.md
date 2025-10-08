# Technical and Functional Requirements – Airbnb Clone Backend

This document outlines the technical and functional requirements for core backend features of the Airbnb Clone project.

---

## 1. User Authentication

### Functional Requirements:
- Users must be able to register with name, email, and password.
- Users can log in using email and password.
- Authenticated sessions must be maintained (using JWT or sessions).
- Users can log out and reset passwords.

### API Endpoints:
| Method | Endpoint        | Description          |
|--------|------------------|----------------------|
| POST   | /api/auth/register | Register a new user |
| POST   | /api/auth/login    | Log in user         |
| POST   | /api/auth/logout   | Log out user        |
| POST   | /api/auth/reset-password | Request password reset |

### Input Specifications:
- **Register/Login**: `email`, `password`, `name` (register only)
- **Password Rules**: Minimum 8 characters, alphanumeric

### Output Specifications:
- **Success**: JWT token and user data
- **Failure**: Error message (400 for bad input, 401 for invalid credentials)

### Validation Rules:
- Email must be valid and unique
- Password must meet security criteria
- All required fields must be present

### Performance Criteria:
- Authentication requests must respond within 300ms under normal load
- Password hashing must use a secure algorithm (e.g., bcrypt)

---

## 2. Property Management

### Functional Requirements:
- Hosts can create, update, delete, and view their listings.
- Guests can browse and view listing details.
- Listings contain: title, description, price, address, images, amenities.

### API Endpoints:
| Method | Endpoint            | Description               |
|--------|---------------------|---------------------------|
| POST   | /api/properties     | Create new property       |
| GET    | /api/properties     | List all properties       |
| GET    | /api/properties/:id | Get property by ID        |
| PUT    | /api/properties/:id | Update property details   |
| DELETE | /api/properties/:id | Delete a property         |

### Input Specifications:
- Required: `title`, `description`, `price`, `location`
- Optional: `images`, `amenities`

### Output Specifications:
- JSON with full property object
- Includes host ID, timestamps

### Validation Rules:
- Title and description must be non-empty
- Price must be a positive number
- Only property owner (host) can update or delete

### Performance Criteria:
- CRUD operations must complete within 500ms
- Properties list must support pagination and filtering

---

## 3. Booking System

### Functional Requirements:
- Guests can book available properties.
- Hosts can view bookings on their listings.
- Prevent overlapping bookings.
- Users can cancel bookings.

### API Endpoints:
| Method | Endpoint             | Description               |
|--------|----------------------|---------------------------|
| POST   | /api/bookings        | Create a new booking      |
| GET    | /api/bookings        | View user bookings        |
| GET    | /api/bookings/:id    | Get booking details       |
| DELETE | /api/bookings/:id    | Cancel a booking          |

### Input Specifications:
- `property_id`, `start_date`, `end_date`
- Dates must be in ISO 8601 format

### Output Specifications:
- Booking confirmation with booking ID and total cost
- Error message if dates overlap or property is unavailable

### Validation Rules:
- No overlapping dates allowed per property
- Start date must be before end date
- User cannot book their own property

### Performance Criteria:
- Booking creation must check availability in < 300ms
- List responses must support pagination

---


