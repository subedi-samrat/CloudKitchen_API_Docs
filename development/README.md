# Development Guide

## Overview
This document provides guidelines for developers working on the Cloud Kitchen Management System Backend API. This project is built using NestJS, a progressive Node.js framework.

## Prerequisites
- Node.js (v18 or later)
- npm (v9 or later)
- Git

## Getting Started

1. Clone the repository:
   ```
   git clone https://github.com/your-repo/cloud-kitchen-api.git
   cd cloud-kitchen-api
   ```

2. Install dependencies:
   ```
   npm install
   ```

3. Set up environment variables:
   - Copy `.env.example` to `.env`
   - Fill in the required environment variables

4. Run database migrations:
   ```
   npx prisma migrate dev
   ```

5. Start the development server:
   ```
   npm run start:dev
   ```

## Project Structure

- `src/` - Source code
  - `modules/` - Feature modules (auth, order, menu, etc.)
  - `common/` - Shared utilities, interceptors, and pipes
- `test/` - Test files
- `docs/` - Project documentation
- `prisma/` - Database schema and migrations

## Development Workflow

1. Create a new branch for your feature or bug fix
2. Write code and tests
3. Run linter: `npm run lint`
4. Run tests: `npm run test`
5. Commit changes and push to your branch
6. Create a pull request for review

## API Documentation

We use Swagger for API documentation. After starting the development server, you can access the Swagger UI at:

```
http://localhost:3000/api
```

## Helpful Commands

- `npm run start:dev` - Start the development server with hot-reload
- `npm run build` - Build the project
- `npm run test` - Run unit tests
- `npm run test:e2e` - Run end-to-end tests
- `npm run lint` - Run ESLint

## Best Practices

- Follow NestJS best practices and design patterns
- Write unit tests for new features
- Keep modules small and focused
- Use dependency injection
- Document your code and APIs

## Troubleshooting

If you encounter any issues during development, please check the following:

1. Ensure all dependencies are installed
2. Verify that your `.env` file is correctly configured
3. Check if the database is running and accessible
4. Clear the dist/ folder and rebuild the project

If problems persist, please reach out to the lead developer or create an issue in the project repository.

## Additional Resources

- [NestJS Documentation](https://docs.nestjs.com/)
- [Prisma Documentation](https://www.prisma.io/docs/)
- [Project Specification](../PROJECT_SPECIFICATION.md)
- [API Documentation](../api/README.md)
- [Database Schema](../database/README.md)

Happy coding!

