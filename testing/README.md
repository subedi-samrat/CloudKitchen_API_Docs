# Testing Guide

## Overview

This document provides guidelines for testing the Cloud Kitchen Management System. Our testing strategy encompasses unit tests, integration tests, and end-to-end (e2e) tests to ensure the reliability and functionality of our application.

## Table of Contents

1. [Test Environment Setup](#test-environment-setup)
2. [Types of Tests](#types-of-tests)
3. [Running Tests](#running-tests)
4. [Writing Tests](#writing-tests)
5. [Continuous Integration](#continuous-integration)
6. [Best Practices](#best-practices)

## Test Environment Setup

1. Ensure you have Node.js (v18 or later) and npm (v9 or later) installed.
2. Clone the repository and install dependencies:
   ```
   git clone https://github.com/your-repo/cloud-kitchen-api.git
   cd cloud-kitchen-api
   npm install
   ```
3. Set up a test database and update the `.env.test` file with the appropriate credentials.

## Types of Tests

### Unit Tests
- Test individual components and functions in isolation.
- Located in `src/**/*.spec.ts` files.

### Integration Tests
- Test the interaction between different modules and services.
- Located in `test/integration` directory.

### End-to-End (E2E) Tests
- Test the entire application flow from the API endpoints.
- Located in `test/e2e` directory.

## Running Tests

Use the following npm scripts to run tests:

- `npm run test`: Run unit tests
- `npm run test:e2e`: Run end-to-end tests
- `npm run test:cov`: Run tests with coverage report

## Writing Tests

- Use Jest as the testing framework.
- Follow the AAA (Arrange-Act-Assert) pattern.
- Mock external dependencies and database calls.
- Test both success and error scenarios.

Example test structure:

```typescript
describe('OrderService', () => {
  let service: OrderService;

  beforeEach(async () => {
    // Setup
  });

  it('should create an order', async () => {
    // Arrange
    // Act
    // Assert
  });
});
```

## Continuous Integration

- Tests are automatically run on every push and pull request.
- CI pipeline is configured in `.github/workflows/ci.yml`.
- Ensure all tests pass before merging changes.

## Best Practices

1. Maintain high test coverage (aim for at least 80%).
2. Keep tests independent and idempotent.
3. Use meaningful test descriptions.
4. Regularly update tests as the codebase evolves.
5. Use test data factories for consistent test data.
6. Implement API tests for all endpoints.

For more detailed information on development practices, refer to the [Development Guide](../development/README.md).
