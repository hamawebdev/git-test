# Medcin Platform API Documentation

## Authentication
All endpoints require JWT Bearer token authentication.
```
Authorization: Bearer <jwt_token>
```

---

## Course Progress API

### Get Progress Overview
**GET** `/api/v1/students/progress/overview`

Returns comprehensive progress overview including courses, quiz scores, and exam results.

**Response:**
```json
{
  "success": true,
  "data": {
    "completedCourses": [
      {
        "courseId": 1,
        "courseName": "Basic Anatomy",
        "moduleId": 1,
        "moduleName": "Anatomy",
        "uniteId": 1,
        "uniteName": "Medical Sciences",
        "layer1Completed": true,
        "layer2Completed": true,
        "layer3Completed": false,
        "progressPercentage": 66.67
      }
    ],
    "quizScores": [
      {
        "quizId": 1,
        "quizTitle": "Anatomy Quiz 1",
        "score": 85,
        "percentage": 85.0,
        "completedAt": "2025-08-25T10:00:00.000Z"
      }
    ],
    "examResults": [
      {
        "examId": 1,
        "examTitle": "Midterm Exam",
        "score": 78,
        "percentage": 78.0,
        "completedAt": "2025-08-25T11:00:00.000Z"
      }
    ],
    "overallStats": {
      "totalQuizzesTaken": 5,
      "averageQuizScore": 82.5,
      "coursesInProgress": 3,
      "coursesCompleted": 1,
      "totalExamsTaken": 2,
      "averageExamScore": 75.0
    }
  }
}
```

### Update Course Progress
**PUT** `/api/v1/students/courses/{courseId}/progress`

Updates progress for a specific course layer.

**Request Body:**
```json
{
  "layer": 2,        // 1, 2, or 3
  "completed": true  // true or false
}
```

**Response:**
```json
{
  "success": true,
  "message": "Course layer 2 progress updated successfully"
}
```

---

## Common Response Format

All endpoints follow this response structure:

**Success Response:**
```json
{
  "success": true,
  "data": { /* endpoint-specific data */ },
  "meta": {
    "timestamp": "2025-08-25T18:55:29.114Z",
    "requestId": "unique-request-id"
  }
}
```

**Error Response:**
```json
{
  "success": false,
  "error": {
    "type": "ValidationError",
    "message": "Validation failed",
    "timestamp": "2025-08-25T18:55:29.114Z",
    "requestId": "unique-request-id"
  }
}
```
