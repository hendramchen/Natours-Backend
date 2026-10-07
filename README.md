# Natours Backend API

A Node.js and Express REST API for the Natours travel booking application. This project provides a backend for managing tours, users, reviews, and authentication with MongoDB and JWT-based security.

## Overview

This backend was built as a learning project focused on modern backend development concepts, including:

- RESTful API design
- MongoDB + Mongoose models and validation
- JWT authentication and role-based authorization
- Password reset and email handling
- Filtering, sorting, pagination, and geospatial queries
- Security hardening for production-grade APIs

## Tech Stack

- Node.js
- Express.js
- MongoDB Atlas / Mongoose
- JWT for authentication
- Nodemailer for password reset emails
- Helmet, express-rate-limit, xss-clean, express-mongo-sanitize, hpp

## Features

- Tour management with CRUD operations
- Top tours and tour statistics endpoints
- Search, filtering, sorting, and pagination
- Geospatial tour search by distance and location
- User signup/login with secure password hashing
- Password update and forgot/reset password flows
- Role-based access control for admin, lead-guide, guide, and user roles
- Review creation and management linked to tours and users
- Global error handling and API security middleware

## Project Structure

```bash
.
├── app.js
├── server.js
├── config.env
├── package.json
├── README.md
├── controllers/
│   ├── authController.js
│   ├── errorController.js
│   ├── handlerFactory.js
│   ├── reviewController.js
│   ├── tourController.js
│   └── userController.js
├── models/
│   ├── reviewModel.js
│   ├── tourModel.js
│   └── userModel.js
├── routes/
│   ├── reviewRoutes.js
│   ├── tourRoutes.js
│   └── userRoutes.js
├── utils/
│   ├── apiFeatures.js
│   ├── appError.js
│   ├── catchAsync.js
│   └── email.js
├── public/
├── dev-data/
└── templates/
```

## Getting Started

### 1) Install dependencies

```bash
npm install
```

### 2) Configure environment variables

Create a `.env` file or use the existing `config.env` file and update it with your database and auth settings:

```bash
NODE_ENV=development
PORT=3000
DATABASE=your_mongodb_connection_string
DATABASE_PASSWORD=your_database_password
JWT_SECRET=your_jwt_secret
JWT_EXPIRES_IN=90d
JWT_COOKIE_EXPIRES_IN=90
EMAIL_USERNAME=your_email_username
EMAIL_PASSWORD=your_email_password
EMAIL_HOST=sandbox.smtp.mailtrap.io
EMAIL_PORT=25
```

### 3) Run the server

Development mode:

```bash
npm run start:dev
```

Production mode:

```bash
npm run start:prod
```

The API runs on:

```bash
http://localhost:3000
```

## Main API Endpoints

### Tours

```bash
GET /api/v1/tours
GET /api/v1/tours/:id
POST /api/v1/tours
PATCH /api/v1/tours/:id
DELETE /api/v1/tours/:id
GET /api/v1/tours/top-5-cheap
GET /api/v1/tours/tour-stats
GET /api/v1/tours/monthly-plan/:year
GET /api/v1/tours/tours-within/:distance/center/:latlng/unit/:unit
```

### Users

```bash
POST /api/v1/users/signup
POST /api/v1/users/login
POST /api/v1/users/forgotPassword
PATCH /api/v1/users/resetPassword/:token
PATCH /api/v1/users/updateMyPassword
GET /api/v1/users/me
PATCH /api/v1/users/updateMe
DELETE /api/v1/users/deleteMe
GET /api/v1/users
```

### Reviews

```bash
GET /api/v1/reviews
GET /api/v1/reviews/:id
POST /api/v1/tours/:tourId/reviews
PATCH /api/v1/reviews/:id
DELETE /api/v1/reviews/:id
```

## Example Requests

### Sign up a user

```bash
curl -X POST http://localhost:3000/api/v1/users/signup \
  -H "Content-Type: application/json" \
  -d '{
    "name": "John Doe",
    "email": "john@example.com",
    "password": "test1234",
    "passwordConfirm": "test1234"
  }'
```

### Get all tours

```bash
curl http://localhost:3000/api/v1/tours
```

### Login

```bash
curl -X POST http://localhost:3000/api/v1/users/login \
  -H "Content-Type: application/json" \
  -d '{
    "email": "john@example.com",
    "password": "test1234"
  }'
```

## Security Features

This API includes several important safeguards:

- Helmet for HTTP header protection
- Rate limiting to reduce abuse and brute-force attacks
- MongoDB query sanitization
- XSS protection for request payloads
- Parameter pollution prevention
- JWT-based protected routes and role restrictions

## Notes

This project is intended as a backend foundation for a Natours-style travel app and demonstrates many common production patterns used in real-world Node.js APIs.
