# Homework Management System

A .NET 6 Web API for managing homework assignments, users, and submissions with PostgreSQL, JWT authentication, role-based authorization, and clean architecture.

## Features
- User registration and login (Admin, Teacher, Student roles)
- JWT authentication and role-based authorization
- Homework assignment and submission
- Admin controls
- Clean architecture with service classes
- EF Core, Serilog (file/console), Swagger, BCrypt
- Global exception handling middleware

## Setup Steps

### Prerequisites
- [.NET 6 SDK](https://dotnet.microsoft.com/download/dotnet/6.0)
- [PostgreSQL](https://www.postgresql.org/download/)

### 1. Clone the repository
```sh
git clone <your-repo-url>
cd HomeworkManagementSystem
```

### 2. Configure the database
- Update `appsettings.json` with your PostgreSQL connection string:
  ```json
  "ConnectionStrings": {
    "DefaultConnection": "Host=localhost;Port=5432;Username=postgres;Password=root;Database=Homework"
  }
  ```
- Ensure the database `Homework` exists in PostgreSQL.

### 3. Run database migrations (if needed)
```sh
dotnet ef database update
```

### 4. Run the application
```sh
dotnet run
```
- The API will be available at `https://localhost:5001` (see launchSettings.json).

### 5. API Documentation
- Swagger UI: `https://localhost:5001/swagger`
- Use the "Authorize" button to enter a JWT token for protected endpoints.

### 6. Seed Data
- On first run, the database is seeded with:
  - Admin: `admin@example.com` / `Admin123!`
  - Teacher: `teacher1@example.com` / `Teacher123!`
  - Students: `student1@example.com`, `student2@example.com`, `student3@example.com` / `Student123!`

## Assumptions
- Only one student can be assigned per homework (for multi-student, refactor required).
- Passwords are hashed with BCrypt.
- JWT tokens include user id, username, email, and role claims.
- All exceptions are logged via Serilog and handled by global middleware.
- DTOs are used for API requests (e.g., HomeworkDto, SubmissionDto).

## Logging
- Logs are written to `logs/log.txt` and the console using Serilog.

## Customization
- To change JWT settings, update the `Jwt` section in `appsettings.json`.
- To add more roles or features, extend the models, DTOs, and controllers as needed.

## Bonus Features (Optional)

- **File upload support for homework submissions:**
  - Endpoint: `POST /api/submissions/with-file` (multipart/form-data, use `file` field)
- **Notifications for upcoming deadlines:**
  - Background service logs upcoming homework deadlines (next 24h) to Serilog (see `DeadlineNotificationService`).
- **Teacher feedback/comments on submissions:**
  - Endpoint: `POST /api/submissions/comment/{submissionId}` (body: comment string, Teacher only)

---

For any issues, please open an issue or contact the maintainer.#   H o m e w o r k M a n a g e m e n t S y s t e m  
 