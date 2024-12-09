# Cloud Kitchen Management System - Project Specification

## 1. System Overview
A comprehensive cloud kitchen management platform that handles user authentication, order processing, kitchen operations, and delivery management.

## 2. Core Features

### 2.1 User Authentication & Management
#### Phone Verification System
- OTP-based phone verification
  - 10-minute OTP expiration
  - 5 daily attempt limit (reset at midnight)
  - Remaining attempts notification
  - Alternative phone numbers (no verification required)
  - Abuse prevention mechanisms

#### User Types & Roles
1. **Admin**
   - Full CRUD permissions
   - System configuration access
   - User management
   - Analytics access

2. **Manager**
   - Create, Read, Update (no delete)
   - Staff management
   - Order management
   - Inventory management

3. **Staff**
   - Limited create and read permissions
   - Order processing
   - Kitchen operations

4. **Delivery Agent**
   - Read-only access
   - Delivery status updates
   - Route information

5. **Customer**
   - Profile management
   - Order placement
   - Order history
   - Address management

### 2.2 Order Management System

#### Order States
1. **Created**
   - Initial order state
   - Payment pending (for COD)

2. **Confirmed**
   - Payment confirmed (COD)
   - Kitchen notified

3. **InKitchen**
   - Order preparation started
   - 5-minute cancellation window starts

4. **Preparing**
   - Past cancellation window
   - Food preparation in progress

5. **Ready**
   - Order ready for delivery
   - Delivery agent assignment

6. **OutForDelivery**
   - Order with delivery agent
   - Live tracking available

7. **Delivered**
   - Order completed
   - Customer confirmation received

8. **Cancelled**
   - Order cancelled
   - Reason recorded

#### Order Update System
- Maximum 3 update requests per order
- Updates allowed within 10 minutes of order placement
- Price recalculation based on current menu prices
- Update requests tracked for customer behavior analysis

#### Order Cancellation Rules
- 5-minute cancellation window after "InKitchen" status
- Complete cancellation requires admin approval after window
- Cancellation frequency tracked for blacklisting

### 2.3 Blacklist System

#### Triggers
1. **Cancellations**
   - 3 post-confirmation cancellations in rolling 7 days
   - Tracked per user

2. **Payment Issues**
   - 3 payment issues in a week
   - Includes failed/incomplete payments

3. **Customer Complaints**
   - 2 serious complaints
   - Admin verification required

#### Blacklist Types
1. **Temporary Blacklist**
   - 1-week duration
   - Admin notification on expiry
   - Customer can browse menu but cannot order

2. **Permanent Blacklist**
   - After 3 temporary blacklists
   - Requires admin approval
   - Complete order restriction

### 2.4 Delivery Management

#### Distance Calculation
- 10km delivery radius (10.2km buffer)
- Google Maps API integration
- Distance calculation caching
- Retry mechanism for API failures

#### Delivery Assignment
- Based on agent availability
- Optimized for delivery time
- Agent load balancing

### 2.5 Kitchen Operations

#### Inventory Management
- Real-time stock tracking
- Low stock alerts
- Automatic reorder suggestions
- Waste management tracking

#### Order Preparation
- Priority-based queuing
- Preparation time tracking
- Staff assignment
- Quality checks

## 3. Technical Implementation

### 3.1 Database Schema
- Implemented using Prisma ORM
- PostgreSQL database
- Structured for scalability
- Optimized indexes

### 3.2 API Architecture
- RESTful API design
- JWT authentication
- Rate limiting
- Error handling
- API documentation

### 3.3 Security Measures
- Phone verification
- Role-based access control
- Input validation
- SQL injection prevention
- XSS protection

### 3.4 Logging System
- Comprehensive event logging
- User action tracking
- Error logging
- Security incident logging
- 3-month retention policy

## 4. Payment Flow (COD)

### 4.1 Order Placement
1. Customer places order
2. System validates order and delivery address
3. Order marked as "Created"

### 4.2 Payment Process
1. Customer selects COD
2. Order confirmed without payment
3. Payment status tracked
4. Collection marked on delivery

### 4.3 Payment Confirmation
1. Delivery agent collects payment
2. Updates payment status
3. Order marked as complete
4. Payment reconciliation

## 5. Monitoring and Analytics

### 5.1 System Monitoring
- Server health monitoring
- API performance tracking
- Error rate monitoring
- Resource utilization

### 5.2 Business Analytics
- Order analytics
- Customer behavior
- Kitchen performance
- Delivery metrics

## 6. Future Enhancements
1. Online payment integration
2. Customer loyalty program
3. Advanced analytics
4. Mobile application
5. Multi-kitchen support

---

This specification is subject to updates and modifications based on business requirements and technical considerations.
