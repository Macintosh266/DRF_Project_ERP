# Educational Center Management System

A Django REST Framework API for managing the day-to-day operations of an educational center. The system provides functionality for managing students, teachers, courses, groups, schedules, attendance, homework, staff, and news.

## Overview

This project is designed to centralize educational center operations through a RESTful API. It includes role-based permissions, JWT authentication, email verification workflows, and interactive API documentation.

## Features

### User Management and Authentication
- Custom user model with phone number as the primary login identifier.
- Separate user roles and status flags for administrators, teachers, and students.
- JWT-based authentication using Simple JWT.
- Login endpoint that returns access and refresh tokens.
- Password change functionality for authenticated users.
- Student and teacher registration workflows.
- Email verification code generation and verification.

### Students and Teachers
- Create, retrieve, update, and delete student records.
- Manage teacher profiles and their course/department assignments.
- Associate students with educational groups.
- Manage student and teacher account information.

### Courses, Groups, and Scheduling
- Manage courses and departments.
- Create and manage student groups.
- Associate teachers with groups.
- Manage classrooms, lesson types, and schedules.
- Track whether a lesson has started.

### Attendance Management
- Record attendance for students in a group.
- Retrieve attendance records by group.
- Configure attendance levels.
- Restrict attendance operations according to user permissions.

### Homework Management
- Teachers can assign homework to groups.
- Students can submit homework descriptions and files.
- Teachers can review submissions and assign scores.
- Homework records include due dates and submission information.

### News and Content
- Manage news entries and associated images.
- Manage informational content such as About and Services records.
- Apply permission rules to content management endpoints.

### Staff and Organizations
- Manage regions and organizations.
- Associate organization managers with user accounts.
- Store manager contact details and organization-related information.

### Statistics
- Retrieve student registration statistics grouped by month.
- Filter student statistics by date range and account status.
- Retrieve statistics about students who have completed or are still taking courses.

## Technology Stack

| Category | Technologies |
|---|---|
| Language | Python |
| Backend Framework | Django |
| API Framework | Django REST Framework |
| Database | SQLite |
| Authentication | Simple JWT |
| API Documentation | drf-yasg, Swagger, OpenAPI, ReDoc |
| Data Validation | DRF Serializers |
| Email | Django Email Backend |
| Configuration | python-dotenv |

## Project Structure

```text
yakuniy-imthon/
├── config/
│   ├── settings.py
│   ├── urls.py
│   ├── asgi.py
│   └── wsgi.py
├── configapp/
│   ├── models/
│   ├── serializers/
│   ├── views/
│   ├── migrations/
│   ├── add_permission.py
│   ├── make_token.py
│   └── urls.py
├── manage.py
├── .env.example
└── README.md
```

## Getting Started

### 1. Clone the repository

```bash
git clone <repository-url>
cd yakuniy-imthon
```

### 2. Create and activate a virtual environment

**Windows (PowerShell):**

```powershell
python -m venv venv
venv\Scripts\Activate.ps1
```

**Linux / macOS:**

```bash
python3 -m venv venv
source venv/bin/activate
```

### 3. Install dependencies

```bash
pip install Django djangorestframework djangorestframework-simplejwt drf-yasg python-dotenv PyYAML
```

If a `requirements.txt` file is added to the repository, install the pinned project dependencies with:

```bash
pip install -r requirements.txt
```

### 4. Configure environment variables

Create a `.env` file in the project root (the same directory as `manage.py`).

Example:

```env
SECRET_KEY=replace-with-a-secure-secret-key
DEBUG=True

EMAIL_BACKEND=django.core.mail.backends.smtp.EmailBackend
EMAIL_HOST=smtp.example.com
EMAIL_PORT=587
EMAIL_USE_TLS=True
EMAIL_HOST_USER=your-email@example.com
EMAIL_HOST_PASSWORD=your-email-app-password
```

Use credentials from your email provider. Do not commit `.env` or real credentials to version control.

### 5. Apply database migrations

```bash
python manage.py migrate
```

### 6. Create an administrator account

```bash
python manage.py createsuperuser
```

Follow the prompts to create the account. The custom user model uses a phone number as its username field.

### 7. Run the development server

```bash
python manage.py runserver
```

The API will be available at:

```text
http://127.0.0.1:8000/
```

## API Documentation

Interactive API documentation is provided by Swagger and ReDoc.

| Documentation | URL |
|---|---|
| Swagger UI | `http://127.0.0.1:8000/` |
| ReDoc | `http://127.0.0.1:8000/redoc/` |
| Django Admin | `http://127.0.0.1:8000/admin/` |

## Main API Routes

The application API is mounted under `/app/`.

| Resource / Operation | Route |
|---|---|
| Student management | `/app/Student/` |
| Group management | `/app/Group/` |
| Teacher management | `/app/Teacher/` |
| News management | `/app/News/` |
| Staff management | `/app/Staff/` |
| Schedule/table management | `/app/Table/` |
| Attendance level management | `/app/AttandanceLevel/` |
| Group attendance | `/app/attendance/<group_id>/` |
| Student registration | `/app/register/student/` |
| Teacher registration | `/app/register/teacher/` |
| Login | `/app/login/` |
| Change password | `/app/change/password/` |
| Send email verification code | `/app/code/send/` |
| Verify email code | `/app/code/chack/` |
| Assign homework to a group | `/app/homework/<group_id>/give/` |
| Submit homework | `/app/homework/<homework_id>/do/` |
| Review group homework | `/app/homework/<group_id>/check/` |
| Group student management | `/app/check/<group_id>/group/` |

The router also provides standard ViewSet actions for the registered resources. Refer to Swagger for the request methods, parameters, schemas, and response formats.

## Authentication

The API uses JWT authentication through Django REST Framework Simple JWT.

After successfully logging in, the API returns an access token and a refresh token.

For protected endpoints, include the access token in the HTTP Authorization header:

```http
Authorization: Bearer <access_token>
```

The project defines custom permission classes for administrators, teachers, students, and content-management operations.

## Data Models

The application includes models for:

- Users and email verification codes
- Students and parents
- Teachers, courses, and departments
- Groups, rooms, lesson types, and schedules
- Attendance records and attendance levels
- Homework and student submissions
- Staff, regions, and organizations
- News and news images
- About and Services content

## Development Notes

- The checked-in Django configuration uses SQLite as its database.
- Email verification depends on valid SMTP settings in the `.env` file.
- API schemas and endpoint details can be explored through Swagger UI.
- Keep secrets and environment-specific settings outside source control.
- Before production deployment, configure a secure `SECRET_KEY`, set `DEBUG=False`, define explicit `ALLOWED_HOSTS`, configure HTTPS, and review authentication, permissions, email verification, and database settings.

## Current Scope

This repository contains educational-center management functionality. A payment gateway or online payment processing module was not identified in the reviewed source code.
