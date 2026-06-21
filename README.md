# NexusHR - Running Instructions

## Overview

NexusHR is a standalone microservices-based HR management platform consisting of:

* API Gateway
* Authentication Service
* Employee Service
* Payroll Service
* React + Vite Frontend

The application uses an H2 in-memory database and in-memory token cache, so no external database or Redis setup is required.

---

## Prerequisites

Ensure the following are installed and available in your system PATH:

* Java 21 (JDK)
* Node.js and npm

> Maven installation is optional. The included Maven Wrapper (`mvnw.cmd`) automatically downloads and uses the required Maven version.

---

## Project Structure

```text
nexushr/
├── api-gateway/
├── auth-service/
├── employee-service/
├── payroll-service/
├── frontend/
├── mvnw.cmd
├── pom.xml
├── package.json
└── docker-compose.yml
```

---

## Initial Setup

Install frontend and root dependencies:

```powershell
npm install

cd frontend
npm install

cd ..
```

Build all backend services:

```powershell
.\mvnw.cmd clean compile -DskipTests
```

---

## Run the Entire Application

From the project root directory, start all services with a single command:

```powershell
npm run dev
```

This command starts:

* Auth Service
* Employee Service
* Payroll Service
* API Gateway
* Frontend

---

## Application URLs

| Service          | URL                   |
| ---------------- | --------------------- |
| Frontend         | http://localhost:5173 |
| API Gateway      | http://localhost:8080 |
| Auth Service     | http://localhost:8081 |
| Employee Service | http://localhost:8082 |
| Payroll Service  | http://localhost:8083 |

---

## Default Admin Credentials

| Username | Password |
| -------- | -------- |
| admin    | admin123 |

---

## API Endpoints

### Auth Service

Base URL: `http://localhost:8081/api/auth`

* `POST /signup` — Register a new user
* `POST /login` — Login and receive a JWT token
* `POST /refresh` — Refresh JWT token
* `GET /me` — Get current user information

### Employee Service

Base URL: `http://localhost:8082/api`

* `GET /employees` — List employees
* `POST /employees` — Create employee
* `GET /employees/{id}` — Get employee details
* `PUT /employees/{id}` — Update employee
* `DELETE /employees/{id}` — Delete employee
* `GET /departments` — List departments
* `POST /attendance/check-in/{id}` — Check in
* `POST /attendance/check-out/{id}` — Check out
* `POST /leaves` — Apply for leave
* `GET /ai-insights/employee/{id}` — Employee AI insights
* `GET /ai-insights/summary` — Global AI summary

### Payroll Service

Base URL: `http://localhost:8083/api`

* `POST /payroll/run` — Run payroll for all employees
* `GET /payslips/employee/{id}` — Get employee payslips
* `GET /payroll/config/{employeeId}` — Get salary configuration

---

## Troubleshooting

### npm command not recognized

Restart your terminal or verify Node.js installation:

```powershell
node -v
npm -v
```

### Build failures

```powershell
.\mvnw.cmd clean compile -DskipTests
```

### Port conflicts

Ensure the following ports are available:

* 5173
* 8080
* 8081
* 8082
* 8083

### Backend services fail to start

Verify Java installation:

```powershell
java -version
```

Verify Maven Wrapper:

```powershell
.\mvnw.cmd -v
```
