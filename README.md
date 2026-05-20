# Task Manager API

A RESTful API for managing personal tasks, built with Laravel 11 and JWT authentication.

## Features

- User registration and login with JWT authentication
- Create, read, update, and delete tasks
- Filter tasks by status (`todo`, `in_progress`, `done`)
- Secure endpoints — each user can only access their own tasks

## Tech Stack

- **PHP** 8.3
- **Laravel** 11
- **MySQL**
- **JWT Auth** (php-open-source-saver/jwt-auth)

## Requirements

- PHP >= 8.1
- Composer
- MySQL

## Installation

1. Clone the repository
```bash
   git clone https://github.com/fadhilahsyaffi/task-manager-api.git
   cd task-manager-api
```

2. Install dependencies
```bash
   composer install
```

3. Copy environment file and configure your database
```bash
   cp .env.example .env
```

4. Generate app key and JWT secret
```bash
   php artisan key:generate
   php artisan jwt:secret
```

5. Run migrations
```bash
   php artisan migrate
```

6. Start the server
```bash
   php artisan serve
```

## API Endpoints

### Auth

| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/api/auth/register` | Register a new user |
| POST | `/api/auth/login` | Login and get JWT token |
| POST | `/api/auth/logout` | Logout (requires token) |
| GET | `/api/auth/me` | Get current user info |

### Tasks

All task endpoints require `Authorization: Bearer {token}` header.

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/api/tasks` | Get all tasks |
| GET | `/api/tasks?status=todo` | Filter tasks by status |
| POST | `/api/tasks` | Create a new task |
| GET | `/api/tasks/{id}` | Get a specific task |
| PUT | `/api/tasks/{id}` | Update a task |
| DELETE | `/api/tasks/{id}` | Delete a task |

## Request & Response Examples

### Register
```json
POST /api/auth/register
{
    "name": "John Doe",
    "email": "john@example.com",
    "password": "password123",
    "password_confirmation": "password123"
}
```

### Create Task
```json
POST /api/tasks
Authorization: Bearer {token}

{
    "title": "Learn Laravel API",
    "description": "Build a REST API with JWT authentication",
    "status": "in_progress"
}
```

### Task Status Values
- `todo` — Task not started
- `in_progress` — Task in progress
- `done` — Task completed

## Testing with Postman

A Postman collection is included in this repository for easy API testing.

1. Download and install [Postman](https://www.postman.com/downloads)
2. Import `task-manager-api.postman_collection.json` into Postman
3. Set the `base_url` variable to `http://127.0.0.1:8000`
4. Register a new user first, then copy the token to the `token` variable
5. You're ready to test all endpoints!

## License

MIT