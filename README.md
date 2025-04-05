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

### 1. Prerequisites

Make sure you have **Docker Desktop** installed:  
[Download Docker](https://www.docker.com/products/docker-desktop/)

Docker is required to run both the PostgreSQL database and the backend server in isolated containers.

---

### 2. Clone the repository

```bash
git clone https://github.com/yourusername/todo-backend.git
cd todo-backend
```

---

### 3. Create a `.env` file

```env
JWT_SECRET=your_jwt_secret
PORT=5003
DATABASE_URL="postgresql://user:password@localhost:5432/dbname"
```

You can use the sample in `.env.example` if available.

---

### 4. Run the app using Docker

Make sure Docker is running, then:

```bash
docker-compose up --build
```

This will:
- Start a PostgreSQL container
- Start the Node.js app container
- Link both using a shared network

---

### 5. Apply database migration (if needed)

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

## Dependencies Explained

- **express** – Node.js web framework for routing and middleware
- **jsonwebtoken** – For issuing and verifying access tokens
- **bcrypt** – For hashing user passwords (if implemented)
- **prisma** – Modern ORM for SQL databases
- **@prisma/client** – Auto-generated client from Prisma schema
- **dotenv** – Loads environment variables from `.env` file
- **cors** – Handles cross-origin requests
- **nodemon (dev)** – Auto-restarts the server on file changes

---

## Notes

- JWT tokens are required to access any `/todos` routes
- You can expand the schema with fields like `completed`, `dueDate`, or `priority`
- Data is persistent as long as the database volume exists in Docker

