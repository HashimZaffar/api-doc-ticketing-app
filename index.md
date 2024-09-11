
```markdown
# Ticket Booking System API Documentation

## Overview
The Ticket Booking System API allows for comprehensive management of users, events, and tickets. Key functionalities include user authentication, event creation and management, ticket booking and cancellation, and administrative tasks.

## Base URL
```
https://api.yourdomain.com/v1
```

## Authentication
All endpoints requiring user context are protected using JWT (JSON Web Tokens). Include the `Authorization` header with the Bearer token in your requests.

---

## Endpoints

### User Authentication

#### Register User
- **Endpoint:** `POST /users/register`
- **Description:** Registers a new user in the system.
- **Request Data:**
  ```json
  {
    "username": "string",
    "email": "string",
    "password": "string"
  }
  ```
  - **Required Fields:** `username`, `email`, `password`
- **Response Data:**
  - **Success:**
    ```json
    {
      "message": "User registered successfully.",
      "userId": "string"
    }
    ```
  - **Error:**
    ```json
    {
      "error": "string",
      "message": "string"
    }
    ```
- **HTTP Status Codes:**
  - `201 Created`: User registered successfully.
  - `400 Bad Request`: Invalid input parameters.
  - `500 Internal Server Error`: Server-side error.

#### Login User
- **Endpoint:** `POST /users/login`
- **Description:** Authenticates a user and returns an access token.
- **Request Data:**
  ```json
  {
    "email": "string",
    "password": "string"
  }
  ```
  - **Required Fields:** `email`, `password`
- **Response Data:**
  - **Success:**
    ```json
    {
      "token": "string",
      "userId": "string"
    }
    ```
  - **Error:**
    ```json
    {
      "error": "string",
      "message": "string"
    }
    ```
- **HTTP Status Codes:**
  - `200 OK`: Token issued successfully.
  - `401 Unauthorized`: Authentication failed.
  - `500 Internal Server Error`: Server-side error.

### Event Management

#### Create Event
- **Endpoint:** `POST /events`
- **Description:** Creates a new event.
- **Request Data:**
  ```json
  {
    "name": "string",
    "date": "string (ISO 8601 date format)",
    "location": "string",
    "description": "string",
    "capacity": "integer"
  }
  ```
  - **Required Fields:** `name`, `date`, `location`, `capacity`
- **Response Data:**
  - **Success:**
    ```json
    {
      "message": "Event created successfully.",
      "eventId": "string"
    }
    ```
  - **Error:**
    ```json
    {
      "error": "string",
      "message": "string"
    }
    ```
- **HTTP Status Codes:**
  - `201 Created`: Event created successfully.
  - `400 Bad Request`: Invalid input parameters.
  - `500 Internal Server Error`: Server-side error.

#### Get Event Details
- **Endpoint:** `GET /events/{eventId}`
- **Description:** Retrieves detailed information about a specific event.
- **Request Data:**
  - **Path Parameters:** `eventId` (string)
- **Response Data:**
  - **Success:**
    ```json
    {
      "eventId": "string",
      "name": "string",
      "date": "string (ISO 8601 date format)",
      "location": "string",
      "description": "string",
      "capacity": "integer",
      "ticketsAvailable": "integer"
    }
    ```
  - **Error:**
    ```json
    {
      "error": "string",
      "message": "string"
    }
    ```
- **HTTP Status Codes:**
  - `200 OK`: Event details retrieved successfully.
  - `404 Not Found`: Event does not exist.
  - `500 Internal Server Error`: Server-side error.

#### Update Event
- **Endpoint:** `PUT /events/{eventId}`
- **Description:** Updates the details of an existing event.
- **Request Data:**
  ```json
  {
    "name": "string",
    "date": "string (ISO 8601 date format)",
    "location": "string",
    "description": "string",
    "capacity": "integer"
  }
  ```
  - **Required Fields:** `name`, `date`, `location`, `capacity`
- **Response Data:**
  - **Success:**
    ```json
    {
      "message": "Event updated successfully."
    }
    ```
  - **Error:**
    ```json
    {
      "error": "string",
      "message": "string"
    }
    ```
- **HTTP Status Codes:**
  - `200 OK`: Event updated successfully.
  - `400 Bad Request`: Invalid input parameters.
  - `404 Not Found`: Event does not exist.
  - `500 Internal Server Error`: Server-side error.

#### Get All Events
- **Endpoint:** `GET /events`
- **Description:** Retrieves a list of all events.
- **Response Data:**
  - **Success:**
    ```json
    [
      {
        "eventId": "string",
        "name": "string",
        "date": "string (ISO 8601 date format)",
        "location": "string"
      }
    ]
    ```
  - **Error:**
    ```json
    {
      "error": "string",
      "message": "string"
    }
    ```
- **HTTP Status Codes:**
  - `200 OK`: Events retrieved successfully.
  - `500 Internal Server Error`: Server-side error.

### Ticket Management

#### Book Ticket
- **Endpoint:** `POST /tickets`
- **Description:** Books tickets for a specific event.
- **Request Data:**
  ```json
  {
    "eventId": "string",
    "userId": "string",
    "quantity": "integer"
  }
  ```
  - **Required Fields:** `eventId`, `userId`, `quantity`
- **Response Data:**
  - **Success:**
    ```json
    {
      "message": "Ticket(s) booked successfully.",
      "ticketId": "string"
    }
    ```
  - **Error:**
    ```json
    {
      "error": "string",
      "message": "string"
    }
    ```
- **HTTP Status Codes:**
  - `201 Created`: Ticket(s) booked successfully.
  - `400 Bad Request`: Invalid input parameters.
  - `404 Not Found`: Event or user does not exist.
  - `500 Internal Server Error`: Server-side error.

#### Cancel Ticket
- **Endpoint:** `DELETE /tickets/{ticketId}`
- **Description:** Cancels a booked ticket.
- **Request Data:**
  - **Path Parameters:** `ticketId` (string)
- **Response Data:**
  - **Success:**
    ```json
    {
      "message": "Ticket canceled successfully."
    }
    ```
  - **Error:**
    ```json
    {
      "error": "string",
      "message": "string"
    }
    ```
- **HTTP Status Codes:**
  - `200 OK`: Ticket canceled successfully.
  - `404 Not Found`: Ticket does not exist.
  - `500 Internal Server Error`: Server-side error.

#### Get User Tickets
- **Endpoint:** `GET /users/{userId}/tickets`
- **Description:** Retrieves all tickets booked by a specific user.
- **Request Data:**
  - **Path Parameters:** `userId` (string)
- **Response Data:**
  - **Success:**
    ```json
    [
      {
        "ticketId": "string",
        "eventId": "string",
        "eventName": "string",
        "date": "string (ISO 8601 date format)",
        "quantity": "integer"
      }
    ]
    ```
  - **Error:**
    ```json
    {
      "error": "string",
      "message": "string"
    }
    ```
- **HTTP Status Codes:**
  - `200 OK`: Tickets retrieved successfully.
  - `404 Not Found`: User does not exist.
  - `500 Internal Server Error`: Server-side error.

---

## Error Handling

### Error Response Format
- **Error Response:**
  ```json
  {
    "error": "string",
    "message": "string"
  }
  ```

### Common Error Codes
- `400 Bad Request`: Invalid input parameters or missing data.
- `401 Unauthorized`: Authentication failure or invalid token.
- `404 Not Found`: Requested resource does not exist.
- `500 Internal Server Error`: An unexpected error occurred on the server.
