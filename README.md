
# API Documentation

# Authentication

**Register a New User**

**Endpoint**
```bash
POST /api/v1/auth/register
```

**Description**
Register a new user with the provided information. Returns authentication details if registration is successful.

- **Authorization**: None
- **Content-Type**: application/json

**Request**
```http
POST /api/v1/auth/register HTTP/1.1
Host: localhost
Content-Type: application/json

{
  "fullName": "John Doe",
  "email": "johndoe@example.com",
  "password": "your_password_here"
}
```

**Response - Success (HTTP 200 OK)**
```http
HTTP/1.1 200 OK

{
  "success": true,
  "message": "User registered successfully",
  "error": null,
  "data": {
    "access_token": "your_access_token",
    "refresh_token": "your_refresh_token"
  }
}
```

**Response - Error (HTTP 400 Bad Request)**
```http
HTTP/1.1 400 Bad Request

{
  "success": false,
  "error": "Registration failed. Email already exists.",
  "message": null,
  "data": {
    "access_token": null,
    "refresh_token": null
  }
}
```

**Authenticate a User**

**Endpoint**
```bash
POST /api/v1/auth/authenticate
```

**Description**
Authenticate a user using their email and password. Returns authentication details if authentication is successful.

- **Authorization**: None
- **Content-Type**: application/json

**Request**
```http
POST /api/v1/auth/authenticate HTTP/1.1
Host: localhost
Content-Type: application/json

{
  "email": "johndoe@example.com",
  "password": "your_password_here"
}
```

**Response - Success (HTTP 200 OK)**
```http
HTTP/1.1 200 OK

{
  "success": true,
  "message": "Authentication successful",
  "error": null,
  "data": {
    "access_token": "your_access_token",
    "refresh_token": "your_refresh_token"
  }
}
```

**Response - Error (HTTP 401 Unauthorized)**
```http
HTTP/1.1 401 Unauthorized

{
  "success": false,
  "error": "Authentication failed. Invalid credentials.",
  "message": null,
  "data": {
    "access_token": null,
    "refresh_token": null
  }
}
```

**Refresh Authentication Token**

**Endpoint**
```bash
POST /api/v1/auth/refresh-token
```

**Description**
Refresh an authentication token using a valid refresh token.

- **Authorization**: Bearer
- **Content-Type**: application/json

**Request**
```http
POST /api/v1/auth/refresh-token HTTP/1.1
Host: localhost
Authorization: Bearer access_token
Content-Type: application/json
```

**Response - Success (HTTP 200 OK)**
```http
HTTP/1.1 200 OK

{
  "success": true,
  "message": "Token refreshed successfully",
  "error": null,
  "data": {
    "access_token": "your_new_access_token",
    "refresh_token": "your_refresh_token"
  }
}
```

**Response - Error (HTTP 401 Unauthorized)**
```http
HTTP/1.1 401 Unauthorized

{
  "success": false,
  "error": "Token refresh failed. Invalid token or expired token.",
  "message": null,
  "data": {
    "access_token": null,
    "refresh_token": null
  }
}
```

**Initiate Password Reset**

**Endpoint**
```bash
POST /api/v1/auth/password/forgot-password
```

**Description**
Initiate a password reset process for the specified email address.

- **Authorization**: None
- **Content-Type**: application/json

**Request**
```http
POST /api/v1/auth/password/forgot-password HTTP/1.1
Host: localhost
Content-Type: application/json

{
  "email": "user@example.com"
}
```

**Response - Success (HTTP 200 OK)**
```http
HTTP/1.1 200 OK

{
  "success": true,
  "message": "Please check your email. Email is sent successfully.",
  "error": null
}
```

**Response - Error (HTTP 400 Bad Request)**
```http
HTTP/1.1 400 Bad Request

{
  "success": false,
  "error": "Invalid Email",
  "message": "Email is required and cannot be empty."
}
```

**Reset Password**

**Endpoint**
```bash
POST /api/v1/auth/password/reset-password
```

**Description**
Reset the password for a user using a valid reset token.

- **Authorization**: None
- **Content-Type**: application/json

**Request**
```http
POST /api/v1/auth/password/reset-password HTTP/1.1
Host: localhost
Content-Type: application/json

{
  "newPassword": "newPassword123"
}
```

**Response - Success (HTTP 200 OK)**
```http
HTTP/1.1 200 OK

{
  "success": true,
  "message": "Password reset successfully",
  "error": null
}
```

**Response - Error (HTTP 400 Bad Request)**
```http
HTTP/1.1 400 Bad Request

{
  "success": false,
  "error": "Invalid or expired reset token",
  "message": null
}
```

**Response - Error (HTTP 400 Bad Request, User Not Found)**
```http
HTTP/1.1 400 Bad Request

{
  "success": false,
  "error": "User not found",
  "message": null
}
```

**Response - Error (HTTP 400 Bad Request, Invalid Token)**
```http
HTTP/1.1 400 Bad Request

{
  "success": false,
  "error": "Invalid token",
  "message": null
}
```

# User Profile API Documentation

**Get User Profile**

**Endpoint**
```bash
GET /api/v1/user/profile
```

**Description**
Get the user profile.

- **Authorization**: Bearer
- **Content-Type**: application/json

**Request**
```http
GET /api/v1/user/profile HTTP/1.1
Host: localhost
Authorization: Bearer access_token
Content-Type: application/json
```

**Response - Success (HTTP 200 OK)**
```http
HTTP/1.1 200 OK

{
  "success": true,
  "message": "Successfully updated user profile",
  "error": null,
  "data": {
    "email": "user@example.com",
    "contact_number": "+1234567890",
    "bio": "A passionate developer who loves coding and building great applications.",
    "dob": "1990

-08-15",
    "socialMediaLinks": ["https://facebook.com/user123", "https://twitter.com/user123"],
    "preferredLanguage": ["English", "Spanish"],
    "genre": ["Action", "Drama"],
    "city": "New York",
    "country": "USA",
    "coverImageUrl": "https://example.com/cover.jpg",
    "profileImageUrl": "https://example.com/profile.jpg"
  }
}
```

**Response - Error (HTTP 400 Bad Request)**
```http
HTTP/1.1 400 Bad Request

{
  "success": false,
  "error": "error message",
  "message": "Error while fetching user data"
}
```

**Update User Profile**

**Endpoint**
```bash
PUT /api/v1/user/profile/update
```

**Description**
Update the user profile.

- **Authorization**: Bearer
- **Content-Type**: application/json

**Request**
```http
PUT /api/v1/user/profile/update HTTP/1.1
Host: localhost
Authorization: Bearer access_token
Content-Type: application/json

{
  "dob": "1990-08-15",
  "gender": "MALE",
  "city": "New York",
  "country": "USA",
  "preferredLanguage": ["English", "Spanish"],
  "genre": ["Action", "Drama"],
  "socialMediaLinks": ["https://facebook.com/user123", "https://twitter.com/user123"],
  "profileImageUrl": "https://example.com/profile.jpg",
  "coverImageUrl": "https://example.com/cover.jpg",
  "isActive": true,
  "bio": "A passionate developer who loves coding and building great applications."
}
```

**Response - Success (HTTP 200 OK)**
```http
HTTP/1.1 200 OK

{
  "success": true,
  "message": "Successfully updated user profile",
  "error": null,
  "data": {
    "email": "user@example.com",
    "contact_number": "+1234567890",
    "bio": "A passionate developer who loves coding and building great applications.",
    "dob": "1990-08-15",
    "socialMediaLinks": ["https://facebook.com/user123", "https://twitter.com/user123"],
    "preferredLanguage": ["English", "Spanish"],
    "genre": ["Action", "Drama"],
    "city": "New York",
    "country": "USA",
    "coverImageUrl": "https://example.com/cover.jpg",
    "profileImageUrl": "https://example.com/profile.jpg"
  }
}
```

**Response - Error (HTTP 400 Bad Request)**
```http
HTTP/1.1 400 Bad Request

{
  "success": false,
  "error": "error message",
  "message": "Error while fetching user data"
}
```

