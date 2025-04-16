# User Registration Endpoint Documentation

## Description
This endpoint allows new users to register by providing their basic details. The endpoint validates the input data and creates a new user in the system. On success, a JWT token along with the user details is returned.

## Request Body
The expected request body is in JSON format and must include the following properties:

- **fullname**: An object containing:
  - **firstname** *(string, required)*: Must be at least 3 characters long.
  - **lastname** *(string, optional)*: Must be at least 3 characters long if provided.
- **email** *(string, required)*: Must be a valid email and at least 5 characters long.
- **password** *(string, required)*: Must be at least 6 characters long.

### Example:
```json
{
  "fullname": {
    "firstname": "John",
    "lastname": "Doe"
  },
  "email": "john.doe@example.com",
  "password": "secret123"
}
```

## Response
- **user**: An object containing: 
  - **fullname** *(object)*
    - **firstname** *(string, required)*: Must be at least 3 characters long.
    - **lastname** *(string, optional)*: Must be at least 3 characters long if provided.
  - **email** *(string, required)*: Must be a valid email and at least 5 characters long.
  - **password** *(string, required)*: Must be at least 6 characters long.
- **token** *(string)*: JWT Token  


### Success (201 Created)
- **Status Code:** `201`
- Returns a JSON object containing:
  - **token**: The JWT token used for subsequent authenticated requests.
  - **user**: The registered user object with user details.

### Validation Error (400 Bad Request)
- **Status Code:** `400`
- Returns a JSON object containing:
  - **errors**: An array of error messages detailing validation failures.

## Notes
- The endpoint performs input validation using `express-validator`.
- Passwords are hashed using bcrypt before storing in the database.
- A JWT token is generated on successful registration which expires after 1 hour.

---

For any additional details, please refer to the server-side code and configuration files.