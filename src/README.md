# Mergington High School Activities API

A super simple FastAPI application that allows students to view and sign up for extracurricular activities.

## Features

- View all available extracurricular activities
- View registered students
- Teacher login for registering and unregistering students

## Getting Started

1. Install the dependencies:

   ```
   pip install fastapi uvicorn
   ```

2. Run the application:

   ```
   python app.py
   ```

3. Open your browser and go to:
   - API documentation: http://localhost:8000/docs
   - Alternative documentation: http://localhost:8000/redoc

## API Endpoints

| Method | Endpoint                                                          | Description                                                         |
| ------ | ----------------------------------------------------------------- | ------------------------------------------------------------------- |
| GET    | `/activities`                                                     | Get all activities with their details and current participant count |
| POST   | `/activities/{activity_name}/signup?email=student@mergington.edu` | Sign up for an activity                                             |
| POST   | `/auth/login`                                                     | Start a teacher session                                               |
| POST   | `/auth/logout`                                                    | End the current teacher session                                      |
| GET    | `/auth/me`                                                        | Get the current teacher session                                      |

The signup and unregister endpoints require an authenticated teacher session.
Students can still use `GET /activities` to view activities and participants.

The development teacher account is stored in `teachers.json` with a PBKDF2 password hash:

- Username: `teacher`
- Password: `mergington-teacher`

## Data Model

The application uses a simple data model with meaningful identifiers:

1. **Activities** - Uses activity name as identifier:

   - Description
   - Schedule
   - Maximum number of participants allowed
   - List of student emails who are signed up

2. **Students** - Uses email as identifier:
   - Name
   - Grade level

Activity data is stored in memory, which means it will be reset when the server restarts.
Teacher credentials are stored in `teachers.json`. Set the `SESSION_SECRET` environment
variable to replace the development session-signing secret before deploying.
