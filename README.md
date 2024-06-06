# Median

NestJS + Prisma + PosgreSQL tutorial

Based on [Building a REST API with NestJS and Prisma](https://www.prisma.io/blog/nestjs-prisma-rest-api-7D056s1BmOL0) series by Tasin Ishmam published in Prisma Blog.

## Steps

### 1. Building a REST API with NestJS and Prisma

- Create NestJS project

```bash
$ npx @nestjs/cli new median
```

- Create a PostgreSQL instance:
  - create `docker-compose.yml`
  - start docker container

```bash
$ docker-compose up -d
```

- Set up Prisma

```bash
$ npm install -D prisma
$ npx prisma init
```

- Set environment variable (`.env`)
- Create Prisma schema (`prisma/prisma.schema`)
- Migrate the database

```bash
$ npx prisma migrate dev --name "init"
```

- Seed the database
  - create `prisma/seed.ts`
  - add the prisma.seed key to the end of your `package.json`
  - execute seeding

```bash
$ npx prisma db seed
```

- Create Prisma service  
  (`prisma/prisma.module.ts`, `prisma/prisma.service.ts`)
- set up Swagger: install dependesies and initialise Swagger in `main.ts`

```bash
$ npm install --save @nestjs/swagger swagger-ui-express
```

- Implement CRUD operations for Article model
  - start with `npx nest generate resource`
  - import `PrismaModule` in the `ArticleModule`
  - create CRUD endpoints
  - group endpoints in Swagger
  - update Swagger response types

### 2. Input Validation & Transformation

- Set up ValidationPipe globally
  - `npm install class-validator class-transformer`
  - in `main.ts` file and use the `app.useGlobalPipes` method to make `ValidationPipe` available globally in your application
- Add validation rules to `CreateArticleDto`
- Strip unnecessary properties from client requests
- Transform dynamic URL paths with `ParseIntPipe`

### 3. Error Handling

- Detect and throw exceptions directly in controller
- Handle exceptions by using exception filters:
  - create a manual exception filter - `prisma-client-exception/prisma-client-exception.filter.ts`
  - apply the exception filter to your application in `main.ts`

### 4. Handling Relational Data

- Add a `User` model to the database
  - update `prisma/schema.prisma`
  - applay migration - `npx prisma migrate dev --name "add-user-model"`
  - update `prisma.seed.ts` and execute `npx prisma db seed`
- Add an `authorId` field to `ArticleEntity`
- Implement CRUD endpoints for `Users`
  - generate new `users` REST resource - `npx nest generate resource`
  - add `PrismaClient` to the `Users` module
  - define the `User` entity and DTO classes
  - define the `UsersService` class
  - sefine the `UsersController` class
- Exclude `password` field from the response body
  - use the `ClassSerializerInterceptor` to remove a field from the response
- Returning the author along with an article

### 5. Authentication

- Implementing authentication in REST API
  - create a new `auth` module - `npx nest generate resource` - without generate CRUD entry points
  - install `passport`
    - `npm install --save @nestjs/passport passport @nestjs/jwt passport-jwt`
    - `npm install --save-dev @types/passport-jwt`
  - configure passport in `src/auth.module.ts`
- Implement a `POST/auth/login` endpoint
  - create `asc/auth/dto/login.dto.ts` file and define `LoginDto` class
  - create `asc/auth/entity/auth.entity.ts` file and define `AuthEntity` class
  - create a new `login` method inside `AuthService`
  - create the `POST/auth/login` method inside `AuthController`
- Implement JWT authentication strategy
  - create `asc/auth/strategy/jwt.strategy.ts` file and define `JwtStrategy` class
  - add the `JwtStrategy` as a provider in the `AuthModule`
  - to make `UsersService` accessible in the `JwtStrategy` class, add it in the exports of the `UsersModule`
- Implement JWT auth guard
  - create `asc/auth/jwt-auth.guard.ts` file and define `JwtAuthGuard` class
  - add the `JwtAuthGuard` to routes in the `UsersController`
- Integrate authentication in Swagger
- Hashing passwords
  - `npm install bcrypt`
  - `npm install --save-dev @types/bcrypt`
  - update the `create` and `update` methods in the `UsersService` to hash the password before storing it in the database
  - update your database seed script (`prisma/seed.ts`) to hash the passwords before inserting them into the database
  - `npx prisma db seed`
  - update the `login` method in the `AuthService` to use hashed passwords:

## Installation

```bash
$ npm install
$ docker-compose up -d
$ npx prisma migrate dev
$ npx prisma db seed
```

## Running the app

```bash
# development
$ npm run start
# Now, you should be able to access the API documentation at http://localhost:3000/api/

# watch mode
$ npm run start:dev

# production mode
$ npm run start:prod
```

## Test

```bash
# unit tests
$ npm run test

# e2e tests
$ npm run test:e2e

# test coverage
$ npm run test:cov
```

## Support

Nest is an MIT-licensed open source project. It can grow thanks to the sponsors and support by the amazing backers. If you'd like to join them, please [read more here](https://docs.nestjs.com/support).

## Stay in touch

- Author - [Kamil Myśliwiec](https://kamilmysliwiec.com)
- Website - [https://nestjs.com](https://nestjs.com/)
- Twitter - [@nestframework](https://twitter.com/nestframework)

## License

Nest is [MIT licensed](LICENSE).
