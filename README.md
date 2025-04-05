# ToDo App – Full Stack Backend API

A secure and scalable task management backend built with **Node.js**, **Express**, and **Prisma ORM**. It supports user registration and login via **JWT**, allows users to manage personal todo items, and uses **PostgreSQL** as the underlying database. The app is containerized with Docker for easy local development and deployment.

---

## Features

- **User Authentication** – Register, log in, and access protected routes using JWT
- **Todo Management** – Authenticated users can create, edit, and delete their own todos
- **Secure API** – Protected endpoints using middleware
- **Database Layer** – Uses Prisma ORM to interact with a PostgreSQL database
- **Environment Config** – Secrets and DB credentials loaded from `.env`
- **Dockerized Setup** – Uses Docker Compose for app and PostgreSQL container
- **REST Client File** – Includes example `.rest` file for testing API endpoints

---

## Tech Stack

- **Backend**: Node.js, Express
- **Database**: PostgreSQL + Prisma
- **Auth**: JWT (JSON Web Tokens)
- **Deployment Ready**: Docker, Docker Compose
- **Testing**: `.rest` file with example requests

---

## Getting Started

### 1. Clone the repository

```bash
git clone https://github.com/yourusername/todo-backend.git
cd todo-backend
```

### 2. Create a `.env` file

```env
JWT_SECRET=your_jwt_secret
PORT=5003
DATABASE_URL="postgresql://user:password@localhost:5432/dbname"
```

You can use the sample in `.env.example` if available.

### 3. Run with Docker

Make sure Docker is installed and running, then:

```bash
docker-compose up --build
```

This will:
- Start PostgreSQL in a container
- Start the Node.js app in another container
- Connect both via shared network

### 4. Apply database migration

If you need to run migrations manually:

```bash
npx prisma migrate dev
```

---

## API Endpoints

All routes require `Authorization: Bearer <token>` unless otherwise noted.

### Auth Routes

| Method | Endpoint     | Description         |
|--------|--------------|---------------------|
| POST   | `/register`  | Register a new user |
| POST   | `/login`     | Log in and get JWT  |

### Todo Routes

| Method | Endpoint      | Description                |
|--------|---------------|----------------------------|
| GET    | `/todos`      | Get all todos for the user |
| POST   | `/todos`      | Add a new todo             |
| PUT    | `/todos/:id`  | Update a specific todo     |
| DELETE | `/todos/:id`  | Delete a specific todo     |

---

## Folder Structure

```
.
├── prisma/
│   └── schema.prisma         # DB schema
├── routes/
│   ├── authRoutes.js
│   └── todoRoutes.js
├── middleware/
│   └── authMiddleware.js
├── db.js                     # DB connection (Prisma)
├── server.js                 # Main app entry
├── docker-compose.yaml
├── Dockerfile
├── .env
└── todo-app.rest             # API testing
```

---

## Notes

- JWT tokens are required to access any `/todos` routes
- Passwords are hashed and stored securely (if implemented)
- You can extend the schema to support deadlines, tags, or priorities
