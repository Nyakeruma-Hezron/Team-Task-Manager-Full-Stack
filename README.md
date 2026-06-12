
# TeamFlow - Full-Stack Task Management Platform

TeamFlow is a comprehensive, full-stack project management application designed to streamline team collaboration, task assignment, and progress tracking through an intuitive Kanban interface.

**Live Environment:** [https://comrade.name.ng](https://comrade.name.ng)

## 🚀 Features

* **Secure Authentication**: JWT-based authentication with bcrypt password hashing.
* **Project Workspaces**: Create unlimited projects and seamlessly invite team members via email.
* **Interactive Kanban Board**: Visual task management across "To Do," "In Progress," and "Done" stages.
* **Advanced Task Management**: Assign tasks, define priority levels (Low, Medium, High), and establish due dates.
* **Role-Based Access Control (RBAC)**: Delineated permissions between "Admins" (full control) and "Members" (status updates only).
* **Centralized Dashboard**: A high-level overview of active projects, pending assignments, and overdue tasks.

## 🛠️ Technology Stack & Architecture

This application utilizes a modern, containerized microservices architecture optimized for secure and scalable deployment.

| Layer | Technology |
| :--- | :--- |
| **Frontend** | React.js (Vite) with custom CSS (Glassmorphism design) |
| **Backend** | Node.js, Express.js REST API |
| **Database** | PostgreSQL (managed via Prisma ORM) |
| **Caching Layer** | Redis |
| **Reverse Proxy** | Nginx (acts as an API Gateway handling all external routing) |
| **Infrastructure** | Fully containerized using Docker & Docker Compose |

## 🐳 Quick Start (Docker Setup)

The entire application is containerized, making local development and deployment incredibly straightforward.

### Prerequisites
* Docker
* Docker Compose

### Installation & Execution

**1. Clone the repository:**
```bash
git clone [https://github.com/Nyakeruma-Hezron/Team-Task-Manager-Full-Stack.git](https://github.com/Nyakeruma-Hezron/Team-Task-Manager-Full-Stack.git)
cd Team-Task-Manager-Full-Stack

```

**2. Configure Environment Variables:**
Navigate to the backend directory and create your `.env` file:

```bash
cd backend
cp .env.example .env

```

Ensure your `.env` contains the essential variables:

```env
PORT=3000
DATABASE_URL="postgresql://taskuser:supersecretpassword@db:5432/taskmanager?schema=public"
REDIS_URL="redis://redis:6379"
JWT_SECRET="your_secure_random_string"
FRONTEND_URL="http://localhost"

```

**3. Spin up the containers:**
Return to the root directory and start the stack in detached mode:

```bash
cd ..
docker compose up -d --build

```

**4. Run Database Migrations:**
Push the Prisma schema to the newly created PostgreSQL container to build your tables:

```bash
docker compose exec backend npx prisma db push

```

### Access the Application

* **Frontend UI**: `http://localhost`

> **Note:** Nginx automatically proxies any requests starting with `/api/` directly to the hidden backend container.

## 📡 API Reference

### Authentication

* `POST /api/auth/signup` - Register a new account
* `POST /api/auth/login` - Authenticate and retrieve JWT
* `GET /api/auth/me` - Retrieve current user profile

### Projects & Members

* `GET /api/projects` - Retrieve user's projects
* `POST /api/projects` - Initialize a new project
* `GET /api/projects/:id` - Retrieve project details, tasks, and member list
* `POST /api/projects/:id/members` - Invite a user to a project

### Tasks

* `POST /api/projects/:id/tasks` - Create a new task within a project
* `PUT /api/projects/:id/tasks/:taskId` - Update task parameters (status, assignee, priority)
* `DELETE /api/projects/:id/tasks/:taskId` - Remove a task

## 📂 Project Structure

```text
Team-Task-Manager-Full-Stack/
├── docker-compose.yml       # Master infrastructure configuration
├── nginx/                   # Nginx reverse proxy configurations
├── redis/                   # Redis cache configurations
├── frontend/                # React.js SPA
│   ├── src/components/      # Reusable UI elements
│   ├── src/pages/           # Main application views
│   └── src/context/         # Global state management
└── backend/                 # Node.js API
    ├── prisma/              # Database schema and migrations
    ├── src/controllers/     # Request handlers and business logic
    ├── src/routes/          # API endpoint definitions
    └── src/middleware/      # Authentication and RBAC guards

```

```

```
