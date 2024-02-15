# Enhanced FastAPI Contacts API with Authentication and Authorization

## Overview

This iteration of the FastAPI Contacts API builds upon the previous version by implementing authentication and authorization mechanisms. Users are now required to register, and authentication is performed securely. Additionally, the application utilizes JWT tokens for authorization, ensuring that all contact operations are carried out only by registered users. Each user has access only to their respective contact operations.

## Authentication and Authorization

### User Registration

- Endpoint: `POST /register/`
- Request Body:
  ```json
  {
    "email": "user@example.com",
    "password": "securepassword"
  }
  ```
- Response (Successful):
  ```json
  {
    "user_id": 1,
    "email": "user@example.com"
  }
  ```
- Response (Conflict - User Already Exists):
  ```json
  {
    "detail": "User with this email already exists"
  }
  ```

### User Login (Authentication)

- Endpoint: `POST /token/`
- Request Body:
  ```json
  {
    "email": "user@example.com",
    "password": "securepassword"
  }
  ```
- Response (Successful):
  ```json
  {
    "access_token": "your_access_token",
    "token_type": "bearer"
  }
  ```
- Response (Unauthorized - Invalid Credentials):
  ```json
  {
    "detail": "Invalid credentials"
  }
  ```

### JWT Token Authorization

- All contact-related endpoints (`/contacts/`, `/contacts/{contact_id}/`, `/contacts/search/`, `/contacts/birthdays/`) require the inclusion of the `Authorization` header with the bearer token:
  ```
  Authorization: Bearer your_access_token
  ```

### CRUD Operations (Authorized)

- CRUD operations on contacts are accessible only to authenticated users with valid JWT tokens.
- Users can only access and modify their own contacts.

## Security Measures

- Passwords are securely hashed, and the application does not store them in plain text in the database.
- JWT tokens are used for secure authorization.

## Error Handling

- Appropriate HTTP status codes and detailed error messages are provided for different scenarios, such as conflict during registration, unauthorized access, and invalid credentials.

## Conclusion

The enhanced FastAPI Contacts API with authentication and authorization provides a secure environment for managing contacts. By implementing user registration, authentication, and JWT token authorization, the application ensures that only registered users can access and manipulate their contact information. The addition of these security measures enhances the overall integrity of the API.
