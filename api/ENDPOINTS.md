# API Endpoints Documentation

## Base URL
```
/api/v1
```

## Authentication Endpoints

### Phone Verification
```
POST /auth/send-otp
POST /auth/verify-otp
POST /auth/resend-otp
```

### Authentication
```
POST /auth/login
POST /auth/refresh-token
POST /auth/logout
```

### User Management
```
POST   /users
GET    /users
GET    /users/:id
PUT    /users/:id
DELETE /users/:id
```

## User Profile Endpoints

### Profile Management
```
GET    /profile
PUT    /profile
PUT    /profile/phone
POST   /profile/addresses
GET    /profile/addresses
PUT    /profile/addresses/:id
DELETE /profile/addresses/:id
```

### Order History
```
GET    /profile/orders
GET    /profile/orders/:id
```

## Menu Management Endpoints

### Categories
```
POST   /categories
GET    /categories
GET    /categories/:id
PUT    /categories/:id
DELETE /categories/:id
```

### Menu Items
```
POST   /menu-items
GET    /menu-items
GET    /menu-items/:id
PUT    /menu-items/:id
DELETE /menu-items/:id
GET    /menu-items/category/:categoryId
```

## Order Management Endpoints

### Customer Orders
```
POST   /orders
GET    /orders/:id
PUT    /orders/:id/update
POST   /orders/:id/cancel
GET    /orders/:id/status
```

### Kitchen Orders
```
GET    /kitchen/orders
PUT    /kitchen/orders/:id/status
GET    /kitchen/orders/current
GET    /kitchen/orders/history
```

### Order Updates
```
POST   /orders/:id/update-request
GET    /orders/:id/update-requests
PUT    /orders/:id/update-requests/:requestId
```

## Inventory Management Endpoints

### Inventory
```
GET    /inventory
GET    /inventory/:id
PUT    /inventory/:id
POST   /inventory/stock-update
GET    /inventory/low-stock
```

### Stock History
```
GET    /inventory/:id/history
POST   /inventory/:id/adjustment
```

## Delivery Management Endpoints

### Delivery Zones
```
POST   /delivery/zones
GET    /delivery/zones
PUT    /delivery/zones/:id
DELETE /delivery/zones/:id
```

### Delivery Orders
```
GET    /delivery/orders
GET    /delivery/orders/:id
PUT    /delivery/orders/:id/status
POST   /delivery/orders/:id/assign
```

## Admin Endpoints

### User Management
```
GET    /admin/users
POST   /admin/users
PUT    /admin/users/:id
DELETE /admin/users/:id
```

### Blacklist Management
```
POST   /admin/blacklist
GET    /admin/blacklist
PUT    /admin/blacklist/:id
DELETE /admin/blacklist/:id
```

### System Management
```
GET    /admin/logs
GET    /admin/metrics
GET    /admin/alerts
POST   /admin/settings
```

## Response Format

### Success Response
```json
{
  "success": true,
  "data": {
    // Response data
  },
  "message": "Operation successful"
}
```

### Error Response
```json
{
  "success": false,
  "error": {
    "code": "ERROR_CODE",
    "message": "Error message",
    "details": {
      // Additional error details
    }
  }
}
```

## Authentication

### Headers
```
Authorization: Bearer {token}
```

### Rate Limiting
- 100 requests per minute for authenticated users
- 20 requests per minute for unauthenticated users

## Error Codes

See [ERROR_CODES.md](./ERROR_CODES.md) for detailed error codes and descriptions.
