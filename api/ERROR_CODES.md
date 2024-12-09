# Error Codes Documentation

## Error Response Format
```javascript
{
  "success": false,
  "error": {
    "code": "ERROR_CODE",
    "message": "Human readable message",
    "details": {
      // Additional context-specific information
    }
  }
}
```

## Authentication Errors (1xxx)

### 1000 - Authentication
- `1001` - Invalid credentials
- `1002` - Token expired
- `1003` - Invalid token
- `1004` - Token required
- `1005` - Refresh token invalid
- `1006` - Account locked
- `1007` - Account disabled
- `1008` - Session expired
- `1009` - Multiple sessions detected

### 1100 - Phone Verification
- `1101` - Invalid OTP
- `1102` - OTP expired
- `1103` - Too many attempts
- `1104` - Daily limit exceeded
- `1105` - Phone number invalid
- `1106` - Verification required
- `1107` - Already verified
- `1108` - SMS service error
- `1109` - Verification in progress

## Authorization Errors (2xxx)

### 2000 - Permissions
- `2001` - Insufficient permissions
- `2002` - Role required
- `2003` - Invalid role
- `2004` - Access denied
- `2005` - Resource forbidden
- `2006` - IP blocked
- `2007` - Geographic restriction
- `2008` - Time restriction
- `2009` - Rate limit exceeded

### 2100 - Blacklist
- `2101` - User blacklisted
- `2102` - Temporary blacklist
- `2103` - Permanent blacklist
- `2104` - Blacklist pending review
- `2105` - Multiple violations
- `2106` - Appeal required
- `2107` - Cooldown period
- `2108` - Review required
- `2109` - Blacklist expired

## User Errors (3xxx)

### 3000 - Profile
- `3001` - Invalid user data
- `3002` - Email required
- `3003` - Phone required
- `3004` - Duplicate email
- `3005` - Duplicate phone
- `3006` - Invalid address
- `3007` - Profile incomplete
- `3008` - Invalid update
- `3009` - Profile locked

### 3100 - Validation
- `3101` - Required field missing
- `3102` - Invalid format
- `3103` - Value out of range
- `3104` - Invalid length
- `3105` - Pattern mismatch
- `3106` - Type mismatch
- `3107` - Constraint violation
- `3108` - Dependency missing
- `3109` - Validation failed

## Order Errors (4xxx)

### 4000 - Order Processing
- `4001` - Invalid order
- `4002` - Order not found
- `4003` - Order expired
- `4004` - Order cancelled
- `4005` - Order completed
- `4006` - Order locked
- `4007` - Status change invalid
- `4008` - Update window closed
- `4009` - Maximum updates reached

### 4100 - Order Items
- `4101` - Item not available
- `4102` - Insufficient stock
- `4103` - Invalid quantity
- `4104` - Price mismatch
- `4105` - Menu item inactive
- `4106` - Category unavailable
- `4107` - Customization invalid
- `4108` - Combination invalid
- `4109` - Item limit exceeded

### 4200 - Delivery
- `4201` - Address out of range
- `4202` - Invalid address
- `4203` - No delivery slots
- `4204` - Driver unavailable
- `4205` - Area not serviceable
- `4206` - Distance calculation failed
- `4207` - Route optimization failed
- `4208` - Delivery time invalid
- `4209` - Location access denied

## Payment Errors (5xxx)

### 5000 - Payment Processing
- `5001` - Payment failed
- `5002` - Invalid amount
- `5003` - Currency mismatch
- `5004` - Transaction failed
- `5005` - Payment expired
- `5006` - Payment cancelled
- `5007` - Refund failed
- `5008` - Payment method invalid
- `5009` - Provider error

### 5100 - COD
- `5101` - COD unavailable
- `5102` - Amount limit exceeded
- `5103` - Area restriction
- `5104` - Time restriction
- `5105` - History check failed
- `5106` - Verification required
- `5107` - Collection failed
- `5108` - Change not available
- `5109` - Documentation missing

## System Errors (6xxx)

### 6000 - Server
- `6001` - Internal error
- `6002` - Service unavailable
- `6003` - Database error
- `6004` - Cache error
- `6005` - Network error
- `6006` - Timeout
- `6007` - Rate limit
- `6008` - Maintenance mode
- `6009` - Resource exhausted

### 6100 - External Services
- `6101` - SMS service down
- `6102` - Email service down
- `6103` - Maps service error
- `6104` - Payment gateway down
- `6105` - Third party error
- `6106` - API limit reached
- `6107` - Integration failed
- `6108` - Service timeout
- `6109` - External validation failed

## Business Logic Errors (7xxx)

### 7000 - Kitchen
- `7001` - Kitchen closed
- `7002` - Preparation time exceeded
- `7003` - Staff unavailable
- `7004` - Quality check failed
- `7005` - Equipment failure
- `7006` - Capacity exceeded
- `7007` - Recipe unavailable
- `7008` - Ingredient shortage
- `7009` - Special order rejected

### 7100 - Inventory
- `7101` - Stock depleted
- `7102` - Low stock
- `7103` - Stock update failed
- `7104` - Item discontinued
- `7105` - Supplier issue
- `7106` - Storage full
- `7107` - Expiry alert
- `7108` - Quality issue
- `7109` - Inventory sync failed

## Response Examples

### Authentication Error
```javascript
{
  "success": false,
  "error": {
    "code": "1001",
    "message": "Invalid credentials provided",
    "details": {
      "remainingAttempts": 2,
      "lockoutTime": "5 minutes"
    }
  }
}
```

### Order Error
```javascript
{
  "success": false,
  "error": {
    "code": "4008",
    "message": "Order update window has closed",
    "details": {
      "orderId": "ORD123",
      "currentStatus": "IN_KITCHEN",
      "updateWindowClosed": "2024-12-08T14:52:22Z"
    }
  }
}
```

### Validation Error
```javascript
{
  "success": false,
  "error": {
    "code": "3101",
    "message": "Required fields missing",
    "details": {
      "fields": ["phoneNumber", "address"],
      "constraints": {
        "phoneNumber": "Must be a valid phone number",
        "address": "Delivery address is required"
      }
    }
  }
}
```
