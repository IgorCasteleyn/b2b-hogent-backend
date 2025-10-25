# Delaware - B2B Platform Backend API

> A robust Node.js/Koa backend API for a B2B e-commerce platform featuring order management, supplier and customer handling, and approval workflows.

## Table of Contents

- [Delaware - B2B Platform Backend API](#delaware---b2b-platform-backend-api)
  - [Table of Contents](#table-of-contents)
  - [Features](#features)
  - [Tech Stack](#tech-stack)
  - [Prerequisites](#prerequisites)
  - [Installation](#installation)
  - [Configuration](#configuration)
  - [Running the Application](#running-the-application)
  - [Testing](#testing)
  - [Project Structure](#project-structure)
  - [API Endpoints](#api-endpoints)
    - [Authentication](#authentication)
    - [Customers (Klant)](#customers-klant)
    - [Suppliers (Leverancier)](#suppliers-leverancier)
    - [Products](#products)
    - [Orders](#orders)
    - [Approvals](#approvals)
  - [Security Features](#security-features)

## Features

- **User Management**: Customer and supplier account management with role-based access
- **Product Catalog**: Full product management system
- **Order Management**: Complete order lifecycle with order details tracking
- **Approval Workflows**: Multi-step approval process for customers and suppliers
- **Notifications**: Email notification system for order updates
- **Address Management**: Comprehensive address handling for multiple locations
- **Authentication**: JWT-based authentication with Argon2 password hashing
- **Security**: Helmet middleware for enhanced HTTP security
- **API Documentation**: Swagger/OpenAPI integration
- **Logging**: Winston-based structured logging
- **Input Validation**: Joi schema validation for all requests

## Tech Stack

- **Runtime**: Node.js with Koa framework
- **Database**: MySQL 8.0+
- **Authentication**: JWT + Argon2
- **ORM/Query Builder**: Knex.js
- **Testing**: Jest + Supertest
- **Documentation**: Swagger/OpenAPI
- **Security**: Helmet, CORS
- **Email**: Nodemailer
- **Logging**: Winston

## Prerequisites

Before you begin, ensure you have the following installed:

- **Node.js** (v14 or higher)
- **Yarn** or **npm**
- **MySQL Community Server** (v8.0 or higher)

## Installation

1. **Clone the repository**

```bash
git clone <repository-url>
cd delaware-backend
```

2. **Install dependencies**

```bash
yarn install
```

3. **Set up your environment variables**

Create a `.env` file in the project root:

```env
NODE_ENV=development
DATABASE_HOST=your-database-host
DATABASE_USERNAME=your-username
DATABASE_PASSWORD=your-password
DATABASE_NAME=your-database-name
DATABASE_PORT=3306
AUTH_JWT_SECRET=your-very-secure-secret-key-minimum-32-chars
APP_EMAIL=your-email@gmail.com
APP_PASSWORD=your-app-specific-password
```

## Configuration

The application uses a configuration system based on `NODE_ENV`:

- `development` - Development environment with debug logging
- `production` - Production environment with optimized settings
- `test` - Testing environment with isolated database

Configuration files are located in `/config` directory.

## Running the Application

**Development mode** (with auto-reload):

```bash
yarn start
```

The API will be available at `http://localhost:3000` (default port)

## Testing

**Run all tests**:

```bash
yarn test
```

**Run tests with coverage report**:

```bash
yarn test:coverage
```

Create a `.env.test` file for test configuration:

```env
NODE_ENV=test
DATABASE_HOST=localhost
DATABASE_PORT=3306
DATABASE_NAME=test_db_name
DATABASE_USERNAME=root
DATABASE_PASSWORD=your-password
```

## Project Structure

```
src/
 core/                 # Core utilities and middleware
    auth.js          # Authentication logic
    jwt.js           # JWT token handling
    roles.js         # Role-based authorization
    validation.js    # Request validation
    logging.js       # Logging configuration
 data/                # Database layer
    migrations/      # Database migrations
    seeds/           # Database seeders
 repository/          # Data access layer
    users.js
    klant.js         # Customers
    leverancier.js   # Suppliers
    order.js
    ...
 service/             # Business logic layer
    users.js
    klant.js
    order.js
    ...
 rest/                # API routes/controllers
    klant.js
    leverancier.js
    order.js
    ...
 createServer.js      # Server initialization
 index.js             # Application entry point
```

## API Endpoints

All endpoints are prefixed with `/api`.

### Authentication

- `POST /api/auth/login` - User login
- `POST /api/auth/register` - User registration

### Customers (Klant)

- `GET /api/klant` - List all customers
- `POST /api/klant` - Create new customer
- `GET /api/klant/:id` - Get customer details
- `PUT /api/klant/:id` - Update customer
- `DELETE /api/klant/:id` - Delete customer

### Suppliers (Leverancier)

- `GET /api/leverancier` - List all suppliers
- `POST /api/leverancier` - Create new supplier
- `GET /api/leverancier/:id` - Get supplier details

### Products

- `GET /api/product` - List all products
- `POST /api/product` - Create new product
- `PUT /api/product/:id` - Update product

### Orders

- `GET /api/order` - List all orders
- `POST /api/order` - Create new order
- `GET /api/order/:id` - Get order details
- `PUT /api/order/:id` - Update order status

### Approvals

- `GET /api/goedkeuring-klant` - Customer approvals
- `GET /api/goedkeuring-leverancier` - Supplier approvals

For complete API documentation, visit `/api/docs` when the application is running (Swagger UI).

## Security Features

- **JWT Authentication**: Secure token-based authentication
- **Password Hashing**: Argon2 for strong password encryption
- **CORS**: Cross-origin resource sharing configuration
- **Helmet**: HTTP security headers
- **Input Validation**: Request body validation with Joi
- **Database Prepared Statements**: Protection against SQL injection via Knex.js
