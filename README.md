# Median

NestJS + Prisma + PosgreSQL tutorial

Based on [Building a REST API with NestJS and Prisma](https://www.prisma.io/blog/nestjs-prisma-rest-api-7D056s1BmOL0) series by Tasin Ishmam published in Prisma Blog.

## Steps

### 1. Building a REST API with NestJS and Prisma

- create NestJS project

```bash
$ npx @nestjs/cli new median
```

- Create a PostgreSQL instance:
  - create `docker-compose.yml`
  - start docker container

```bash
$ docker-compose up -d
```

- set up Prisma

```bash
$ npm install -D prisma
$ npx prisma init
```

- set environment variable (`.env`)
- create Prisma schema (`prisma/prisma.schema`)
- migrate the database

```bash
$ npx prisma migrate dev --name "init"
```

- seed the database
  - create `prisma/seed.ts`
  - add the prisma.seed key to the end of your `package.json`
  - execute seeding

```bash
$ npx prisma db seed
```

- create Prisma service  
  (`prisma/prisma.module.ts`, `prisma/prisma.service.ts`)
- set up Swagger: install dependesies and initialise Swagger in `main.ts`

```bash
$ npm install --save @nestjs/swagger swagger-ui-express
```

- implement CRUD operations for Article model
  - start with `npx nest generate resource`
  - import `PrismaModule` in the `ArticleModule`
  - create CRUD endpoints
  - group endpoints in Swagger
  - update Swagger response types

### 2. Input Validation & Transformation

## Installation

```bash
$ npm install
$ docker-compose up -d
$ npx prisma migrate dev
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