# Database Documentation

## Overview

This document provides information about the database structure and models used in the Cloud Kitchen Management System. Our system uses PostgreSQL as the primary database, with Prisma as the ORM.

## Table of Contents

1. [Database Schema](#database-schema)
2. [Core Models](#core-models)
3. [Relationships](#relationships)
4. [Migrations](#migrations)
5. [Best Practices](#best-practices)

## Database Schema

The complete database schema can be found in the `prisma/schema.prisma` file. This file defines all the models and their relationships.

## Core Models

Our system includes the following core models:

- User
- UserRole
- PhoneVerification
- Order
- MenuItem
- Kitchen
- Delivery

For detailed information about each model, including their fields and relationships, please refer to the [MODELS.md](./MODELS.md) file.

## Relationships

The database schema includes various relationships between models, such as:

- One-to-Many: User to Order
- Many-to-Many: Order to MenuItem
- One-to-One: Order to Delivery

These relationships are defined in the Prisma schema and enforced at the database level.

## Migrations

Database migrations are managed using Prisma Migrate. To create a new migration:

```
npx prisma migrate dev --name your_migration_name
```

To apply migrations in production:

```
npx prisma migrate deploy
```

## Best Practices

1. Always use migrations for schema changes
2. Keep models normalized to reduce data redundancy
3. Use indexes for frequently queried fields
4. Implement soft deletes where appropriate
5. Use transactions for operations that modify multiple tables

For more information on database management and optimization, please refer to the [Development Guide](../development/README.md).
