# Hospital System API Reference

## Base URL
```
https://api.hospital-system.com/v1
```

## Authentication
All API requests require authentication using Bearer tokens.

```
Authorization: Bearer <your-token>
```

## Endpoints

### Authentication
#### POST /auth/login
Login to the system and receive an authentication token.

**Request Body:**
```json
{
  "username": "string",
  "password": "string",
  "role": "string"
}
```

**Response:**
```json
{
  "token": "string",
  "user": {
    "id": "number",
    "username": "string",
    "role": "string",
    "permissions": ["string"]
  }
}
```

### Patient Management
#### GET /patients
Retrieve list of patients.

**Query Parameters:**
- `page`: Page number (default: 1)
- `limit`: Items per page (default: 20)
- `search`: Search term for patient name or ID

**Response:**
```json
{
  "data": [
    {
      "id": "number",
      "firstName": "string",
      "lastName": "string",
      "dateOfBirth": "string",
      "phoneNumber": "string",
      "email": "string"
    }
  ],
  "pagination": {
    "page": "number",
    "limit": "number",
    "total": "number",
    "totalPages": "number"
  }
}
```

#### POST /patients
Create a new patient record.

**Request Body:**
```json
{
  "firstName": "string",
  "lastName": "string",
  "dateOfBirth": "string",
  "phoneNumber": "string",
  "email": "string",
  "address": {
    "street": "string",
    "city": "string",
    "state": "string",
    "zipCode": "string"
  },
  "emergencyContact": {
    "name": "string",
    "phoneNumber": "string",
    "relationship": "string"
  }
}
```

#### GET /patients/{id}
Retrieve a specific patient by ID.

#### PUT /patients/{id}
Update patient information.

#### DELETE /patients/{id}
Remove a patient record.

### Forms Management
#### GET /forms
Retrieve available form templates.

#### POST /forms/{formId}/submissions
Submit a completed form.

#### GET /forms/submissions
Retrieve form submissions.

### Reports
#### GET /reports/admissions
Generate admission reports.

**Query Parameters:**
- `startDate`: Start date (YYYY-MM-DD)
- `endDate`: End date (YYYY-MM-DD)
- `format`: Response format (json, csv, pdf)

#### GET /reports/discharges
Generate discharge reports.

## Error Responses
All endpoints return standard HTTP status codes:

- `200`: Success
- `201`: Created
- `400`: Bad Request
- `401`: Unauthorized
- `403`: Forbidden
- `404`: Not Found
- `500`: Internal Server Error

**Error Response Format:**
```json
{
  "error": {
    "code": "string",
    "message": "string",
    "details": "string"
  }
}
```

## Rate Limiting
API requests are limited to 1000 requests per hour per user. Rate limit headers are included in responses:

```
X-RateLimit-Limit: 1000
X-RateLimit-Remaining: 999
X-RateLimit-Reset: 1640995200
```