# Simple svelte app with base role auth

### Where to start? A.K.A Project setup
I used pnpm, so be aware that npm commands may differ a little bit.

#### [Scaffolding](https://en.wikipedia.org/wiki/Scaffold_(programming)) the project
```bash
  pnpm create svelte name_of_project 
```

#### Installing needed modules
```bash
  pnpm install
```

#### Setuping the data base using [**Supabase**](https://supabase.com/) and [**Prisma**](https://www.prisma.io/)
- Initializing prisma schema (postgresql is default provider) 
  ```bash
    pnpx prisma install --datasource-provider	postgresql
  ```

- Adding prisma packages to your project
  ```bash
    pnpm add prisma --save-dev
    pnpm add @prisma/client
  ```

- Setting up DATABASE_URL inside .env file [Supabase example](https://community.dronahq.com/t/connecting-to-a-supabase-database/980)
  ```env
    DATABASE_URL="your_connection_string"
  ```

- Creating models inside schema.prisma (enums doesn't work in certain providers like sqlite)

```prisma
  // ...
  model User {
    id    Int     @id @default(autoincrement())
    email String  @unique
    name  String?
    role  Role    @default(USER)
    todos Todo[]
  }

  model Todo {
    id        Int      @id @default(autoincrement())
    name      String
    completed Boolean
    createdAt DateTime @default(now())
    updatedAt DateTime @updatedAt
    creator   User     @relation(fields: createdId, references: [id])
    createdId Int
  }

  enum Role {
    USER
    ADMIN
  }
```




