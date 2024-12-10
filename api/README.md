# Cloud Kitchen Management System API Documentation

## Overview

This document provides comprehensive information about the Cloud Kitchen Management System API. The API is built using NestJS and serves as the backend for managing various aspects of the cloud kitchen operations.

## Table of Contents

1. [API Endpoints](#api-endpoints)
2. [Authentication](#authentication)
3. [Error Handling](#error-handling)
4. [Data Models](#data-models)
5. [Versioning](#versioning)
6. [Rate Limiting](#rate-limiting)

## API Endpoints

Detailed information about API endpoints can be found in the [ENDPOINTS.md](./ENDPOINTS.md) file. This includes:

- Base URL
- Authentication endpoints
- User management endpoints
- Order management endpoints
- Menu management endpoints
- Kitchen operations endpoints
- Delivery management endpoints

## Authentication

The API uses JWT (JSON Web Tokens) for authentication. Phone verification (OTP) is required for initial user registration. For more details on the authentication flow, refer to the [AUTH_FLOW.md](../guides/AUTH_FLOW.md) document.

## Error Handling

The API uses standard HTTP status codes and provides detailed error messages. For a complete list of error codes and their meanings, see [ERROR_CODES.md](./ERROR_CODES.md).

## Data Models

Information about the data models used in the API can be found in the [MODELS.md](../database/MODELS.md) file. This includes details about:

- User model
- Order model
- Menu item model
- Kitchen model
- Delivery model

## Versioning

The API uses versioning to ensure backward compatibility. The current version is v1, which is reflected in the base URL: `/api/v1`.

## Rate Limiting

To prevent abuse, the API implements rate limiting. Details about rate limits for different endpoints can be found in the [RATE_LIMITS.md](./RATE_LIMITS.md) file.

## Additional Resources

- [System Architecture](../architecture/README.md)
- [Development Guide](../development/README.md)
- [Testing Guide](../testing/README.md)
- [Deployment Guide](../deployment/README.md)

For any additional questions or support, please contact the development team or create an issue in the project repository.
