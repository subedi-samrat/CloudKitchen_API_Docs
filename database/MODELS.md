# Database Models Documentation

## Core Models

### User Management

#### User
```prisma
model User {
  id                String       @id @default(uuid())
  name              String
  email             String       @unique
  phoneNumber       String?
  phoneVerified     Boolean      @default(false)
  alternativePhones Json?
  role              UserRole     @relation(fields: [roleId], references: [id])
  roleId            String
  blacklistStatus   String?
  blacklistReason   String?
  blacklistUntil    DateTime?
  blacklistHistory  Json?
  orderUpdateCount  Int          @default(0)
  orders            Order[]
  addresses         Address[]
  isActive          Boolean      @default(true)
  createdAt         DateTime     @default(now())
  updatedAt         DateTime     @updatedAt
}
```

#### UserRole
```prisma
model UserRole {
  id           String   @id @default(uuid())
  name         String   @unique
  description  String?
  permissions  String[]
  users        User[]
  createdAt    DateTime @default(now())
  updatedAt    DateTime @updatedAt
}
```

### Authentication

#### PhoneVerification
```prisma
model PhoneVerification {
  id              String    @id @default(uuid())
  phoneNumber     String
  otp             String
  expiresAt       DateTime
  attempts        Int       @default(0)
  dailyAttempts   Int       @default(0)
  lastAttemptDate DateTime  @default(now())
  verified        Boolean   @default(false)
  createdAt       DateTime  @default(now())
  updatedAt       DateTime  @updatedAt
}
```

### Order Management

#### Order
```prisma
model Order {
  id                 String           @id @default(uuid())
  orderNumber        String           @unique
  user               User             @relation(fields: [userId], references: [id])
  userId             String
  status             String
  items              OrderItem[]
  price              BasePrice        @relation(fields: [priceId], references: [id])
  priceId            String           @unique
  updateRequests     Int              @default(0)
  lastUpdateRequest  DateTime?
  inKitchenTime     DateTime?
  cancellationReason String?
  cancellationTime   DateTime?
  isUpdated          Boolean          @default(false)
  previousVersions   Json?
  createdAt          DateTime         @default(now())
  updatedAt          DateTime         @updatedAt
}
```

#### OrderItem
```prisma
model OrderItem {
  id                  String    @id @default(uuid())
  order               Order     @relation(fields: [orderId], references: [id])
  orderId             String
  menuItem            MenuItem  @relation(fields: [menuItemId], references: [id])
  menuItemId          String
  quantity            Int
  price               BasePrice @relation(fields: [priceId], references: [id])
  priceId             String    @unique
  customizations      Json?
  specialInstructions String?
  createdAt           DateTime  @default(now())
  updatedAt           DateTime  @updatedAt
}
```

### Menu Management

#### MenuItem
```prisma
model MenuItem {
  id                String     @id @default(uuid())
  name              String
  itemCode          String     @unique
  description       String
  price             BasePrice  @relation(fields: [priceId], references: [id])
  priceId           String     @unique
  category          Category   @relation(fields: [categoryId], references: [id])
  categoryId        String
  isVeg             Boolean
  isAvailable       Boolean    @default(true)
  preparationTime   Int
  inventory         Inventory?
  createdAt         DateTime   @default(now())
  updatedAt         DateTime   @updatedAt
}
```

#### Category
```prisma
model Category {
  id           String     @id @default(uuid())
  name         String
  description  String?
  isActive     Boolean    @default(true)
  menuItems    MenuItem[]
  createdAt    DateTime   @default(now())
  updatedAt    DateTime   @updatedAt
}
```

### Kitchen Operations

#### KitchenOrder
```prisma
model KitchenOrder {
  id                String            @id @default(uuid())
  orderId           String            @unique
  status            String
  priority          Int               @default(1)
  items             KitchenOrderItem[]
  estimatedPrepTime Int
  startedAt         DateTime?
  completedAt       DateTime?
  notes             String?
  createdAt         DateTime          @default(now())
  updatedAt         DateTime          @updatedAt
}
```

#### Inventory
```prisma
model Inventory {
  id            String    @id @default(uuid())
  menuItemId    String    @unique
  menuItem      MenuItem  @relation(fields: [menuItemId], references: [id])
  currentStock  Int
  minStock      Int
  maxStock      Int
  unit          String
  lastRestocked DateTime?
  createdAt     DateTime  @default(now())
  updatedAt     DateTime  @updatedAt
}
```

### Payment Management

#### PaymentTransaction
```prisma
model PaymentTransaction {
  id                    String    @id @default(uuid())
  orderId              String
  amount               Decimal   @db.Decimal(10, 2)
  currency             String
  provider             String
  providerTransactionId String?
  status               String
  metadata             Json?
  errorMessage         String?
  createdAt            DateTime  @default(now())
  updatedAt            DateTime  @updatedAt
}
```

### System Management

#### SystemLog
```prisma
model SystemLog {
  id         String    @id @default(uuid())
  level      String
  category   String
  message    String    @db.Text
  context    Json?
  severity   String
  expiresAt  DateTime?
  createdAt  DateTime  @default(now())
}
```

#### SecurityAlert
```prisma
model SecurityAlert {
  id          String    @id @default(uuid())
  userId      String
  type        String
  details     Json
  status      String
  reviewedBy  String?
  reviewedAt  DateTime?
  action      String?
  createdAt   DateTime  @default(now())
  updatedAt   DateTime  @updatedAt
}
```

## Database Indexes

### Performance Indexes
```prisma
@@index([email])
@@index([phoneNumber])
@@index([orderNumber])
@@index([status])
@@index([createdAt])
```

### Foreign Key Indexes
```prisma
@@index([userId])
@@index([menuItemId])
@@index([categoryId])
```

### Composite Indexes
```prisma
@@index([isActive, isAvailable])
@@index([provider, eventType])
```

## Data Types

### Common JSON Structures

#### Address JSON
```javascript
{
  street: String,
  city: String,
  state: String,
  postalCode: String,
  coordinates: {
    lat: Float,
    lng: Float
  }
}
```

#### Customization JSON
```javascript
{
  options: [{
    name: String,
    value: String,
    price: Float
  }]
}
```

#### Metadata JSON
```javascript
{
  version: String,
  platform: String,
  deviceInfo: {
    type: String,
    os: String,
    browser: String
  }
}
```

## Database Constraints

### Unique Constraints
- User email
- Phone number
- Order number
- Item code

### Check Constraints
- Price > 0
- Quantity > 0
- Stock >= 0

### Foreign Key Constraints
- ON DELETE: RESTRICT
- ON UPDATE: CASCADE

## Data Migration

### Version Control
```sql
-- Migration: 001_initial_schema
CREATE TABLE users (
  id UUID PRIMARY KEY,
  ...
);

-- Migration: 002_add_phone_verification
ALTER TABLE users
ADD COLUMN phone_verified BOOLEAN DEFAULT FALSE;
```

### Rollback Procedures
```sql
-- Rollback: 002_add_phone_verification
ALTER TABLE users
DROP COLUMN phone_verified;

-- Rollback: 001_initial_schema
DROP TABLE users;
```
