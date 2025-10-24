# SkillHub Backend API Documentation

## Authentication

### Login
```
POST /api/auth/login
```
Request body:
```json
{
  "email": "student@example.com",
  "password": "password123"
}
```

Response:
```json
{
  "success": true,
  "token": "JWT_TOKEN",
  "user": {
    "id": "USER_ID",
    "name": "John Student",
    "email": "student@example.com",
    "role": "student",
    "registrationNumber": "REG001"
  }
}
```

### Register
```
POST /api/auth/register
```
Request body:
```json
{
  "name": "New Student",
  "email": "newstudent@example.com",
  "password": "password123",
  "role": "student",
  "registrationNumber": "REG002"
}
```

Response:
```json
{
  "success": true,
  "token": "JWT_TOKEN",
  "user": {
    "id": "USER_ID",
    "name": "New Student",
    "email": "newstudent@example.com",
    "role": "student",
    "registrationNumber": "REG002"
  }
}
```

### Get Profile
```
GET /api/auth/profile
```
Headers:
```
Authorization: Bearer JWT_TOKEN
```

Response:
```json
{
  "success": true,
  "data": {
    "_id": "USER_ID",
    "name": "John Student",
    "email": "student@example.com",
    "role": "student",
    "registrationNumber": "REG001",
    "createdAt": "2024-01-01T00:00:00.000Z",
    "updatedAt": "2024-01-01T00:00:00.000Z"
  }
}
```

## Courses

### Get All Courses
```
GET /api/courses
```

Response:
```json
[
  {
    "_id": "COURSE_ID",
    "title": "Web Development Fundamentals",
    "code": "WEB101",
    "category": "Programming",
    "description": "Learn HTML, CSS, and JavaScript basics for web development.",
    "instructor": "Dr. Smith",
    "duration": "8 weeks",
    "level": "Beginner",
    "maxStudents": 30,
    "enrolled": 15,
    "startDate": "2024-02-01T00:00:00.000Z",
    "endDate": "2024-03-28T00:00:00.000Z",
    "syllabus": [
      {
        "module": "Module 1",
        "topic": "Introduction to Web Development",
        "tutorials": ["HTML Basics", "Setting up Development Environment"]
      }
    ],
    "isActive": true,
    "createdAt": "2024-01-01T00:00:00.000Z",
    "updatedAt": "2024-01-01T00:00:00.000Z"
  }
]
```

### Get Course by ID
```
GET /api/courses/:id
```

Response:
```json
{
  "_id": "COURSE_ID",
  "title": "Web Development Fundamentals",
  "code": "WEB101",
  "category": "Programming",
  "description": "Learn HTML, CSS, and JavaScript basics for web development.",
  "instructor": "Dr. Smith",
  "duration": "8 weeks",
  "level": "Beginner",
  "maxStudents": 30,
  "enrolled": 15,
  "startDate": "2024-02-01T00:00:00.000Z",
  "endDate": "2024-03-28T00:00:00.000Z",
  "syllabus": [
    {
      "module": "Module 1",
      "topic": "Introduction to Web Development",
      "tutorials": ["HTML Basics", "Setting up Development Environment"]
    }
  ],
  "isActive": true,
  "createdAt": "2024-01-01T00:00:00.000Z",
  "updatedAt": "2024-01-01T00:00:00.000Z"
}
```

## Student Endpoints

### Enroll in Course
```
POST /api/courses/:id/enroll
```
Headers:
```
Authorization: Bearer JWT_TOKEN
```

Response:
```json
{
  "message": "Successfully enrolled in Web Development Fundamentals"
}
```

### Get Enrolled Courses
```
GET /api/courses/enrolled
```
Headers:
```
Authorization: Bearer JWT_TOKEN
```

Response:
```json
[
  {
    "id": "COURSE_ID",
    "title": "Web Development Fundamentals",
    "code": "WEB101",
    "category": "Programming",
    "description": "Learn HTML, CSS, and JavaScript basics for web development.",
    "instructor": "Dr. Smith",
    "duration": "8 weeks",
    "level": "Beginner",
    "maxStudents": 30,
    "enrolled": 16,
    "startDate": "2024-02-01T00:00:00.000Z",
    "endDate": "2024-03-28T00:00:00.000Z",
    "syllabus": [
      {
        "module": "Module 1",
        "topic": "Introduction to Web Development",
        "tutorials": ["HTML Basics", "Setting up Development Environment"]
      }
    ],
    "enrolledAt": "2024-01-15T00:00:00.000Z"
  }
]
```

### Unenroll from Course
```
DELETE /api/courses/:id/unenroll
```
Headers:
```
Authorization: Bearer JWT_TOKEN
```

Response:
```json
{
  "message": "Successfully unenrolled from Web Development Fundamentals"
}
```

## Faculty Endpoints

### Create Course
```
POST /api/courses
```
Headers:
```
Authorization: Bearer JWT_TOKEN
```
Request body:
```json
{
  "title": "New Course",
  "code": "NC101",
  "category": "Programming",
  "description": "A new course",
  "instructor": "Dr. Smith",
  "duration": "8 weeks",
  "level": "Beginner",
  "maxStudents": 30,
  "startDate": "2024-02-01",
  "endDate": "2024-03-28",
  "syllabus": [
    {
      "module": "Module 1",
      "topic": "Introduction",
      "tutorials": ["Basics"]
    }
  ]
}
```

Response:
```json
{
  "_id": "COURSE_ID",
  "title": "New Course",
  "code": "NC101",
  "category": "Programming",
  "description": "A new course",
  "instructor": "Dr. Smith",
  "duration": "8 weeks",
  "level": "Beginner",
  "maxStudents": 30,
  "enrolled": 0,
  "startDate": "2024-02-01T00:00:00.000Z",
  "endDate": "2024-03-28T00:00:00.000Z",
  "syllabus": [
    {
      "module": "Module 1",
      "topic": "Introduction",
      "tutorials": ["Basics"]
    }
  ],
  "isActive": true,
  "createdAt": "2024-01-01T00:00:00.000Z",
  "updatedAt": "2024-01-01T00:00:00.000Z"
}
```

### Update Course
```
PUT /api/courses/:id
```
Headers:
```
Authorization: Bearer JWT_TOKEN
```

### Delete Course (Soft Delete)
```
DELETE /api/courses/:id
```
Headers:
```
Authorization: Bearer JWT_TOKEN
```

### Get Courses by Faculty
```
GET /api/courses/faculty/:facultyId
```
Headers:
```
Authorization: Bearer JWT_TOKEN
```