# CodeCraftHub API

A beginner-friendly **REST API** to track personal learning goals (courses).

Built with **Node.js** and **Express**, this API stores data in a JSON file (`courses.json`) instead of using a database.

It exposes CRUD endpoints under:

/api/courses

and includes both **path-based** and **body-based** update/delete options.

---

# Project Overview

- Lightweight REST API for managing learning courses
- Data persisted in a JSON file (`courses.json`)
- Auto-generated incremental IDs starting from **1**
- `created_at` timestamp added on creation
- Validation for required fields and allowed status values
- No authentication or user management (for learning REST API basics)

---

# Features

- Create a new course
- Retrieve all courses
- Retrieve a specific course by ID
- Update a course (full replace) via path parameter or request body
- Partially update a course (`PATCH`)
- Delete a course by ID or by ID in request body
- Automatic JSON data file creation (`courses.json`) if missing
- Basic error handling for:
  - Missing fields
  - Course not found
  - Invalid status values
  - File I/O errors

---

# Tech Stack

- **Node.js**
- **Express**

---

# Prerequisites

- Node.js (LTS recommended)

---

# Installation

1. Create a project folder and navigate into it.

2. Save the application file as:

app.js

3. Create `package.json` (or use the one provided).

4. Install dependencies:

npm install express

### Notes

The application stores data in a JSON file named:

courses.json

If the file does not exist, it will be **created automatically**.

---

# Running the Application

Start the server:

npm start

Or run directly:

node app.js

The server runs on port **5000** by default.

Access the API at:

http://localhost:5000

---

# API Endpoint Documentation

Base API path:

/api/courses

---

# POST /api/courses

### Description

Add a new course.

### Required Body Fields

- `name`
- `description`
- `target_date` (YYYY-MM-DD)
- `status`

Allowed status values:

- Not Started
- In Progress
- Completed

### Response

`201 Created` with the new course including `id` and `created_at`.

### Example Request

json
{
"name": "Learn Node.js",
"description": "Fundamentals of Node.js & Express",
"target_date": "2026-05-01",
"status": "Not Started"
}

### Example Response

json
{
"id": 1,
"name": "Learn Node.js",
"description": "Fundamentals of Node.js & Express",
"target_date": "2026-05-01",
"status": "Not Started",
"created_at": "2024-07-01T12:34:56.789Z"
}

---

# GET /api/courses

### Description

Retrieve all courses.

### Optional Query

?id=NUMBER

Fetch a specific course by ID.

### Examples

GET /api/courses
GET /api/courses?id=1

Response:

- `200 OK` with an array of courses
- If `?id=` is used, returns a single course

---

# GET /api/courses/:id

### Description

Retrieve a specific course using a path parameter.

### Example

GET /api/courses/1

Response:

- `200 OK` with the course object
- `404 Not Found` if the course does not exist

---

# PUT /api/courses

### Description

Update a course by sending the ID in the request body.

### Required Body Fields

- `id`
- `name`
- `description`
- `target_date`
- `status`

### Example Request

json
{
"id": 1,
"name": "Learn Node.js",
"description": "Updated description",
"target_date": "2026-05-15",
"status": "In Progress"
}

Response:

- `200 OK`
- `404 Not Found`

---

# PUT /api/courses/:id

### Description

Update a specific course using a path parameter.

### Required Fields

- `name`
- `description`
- `target_date`
- `status`

### Example Request

json
{
"name": "Learn Node.js",
"description": "Updated description",
"target_date": "2026-05-15",
"status": "In Progress"
}

Response:

- `200 OK`
- `404 Not Found`

---

# PATCH /api/courses/:id

### Description

Partially update a course.

### Allowed Fields

- `name`
- `description`
- `target_date`
- `status`

### Validation

If updating `target_date`:

YYYY-MM-DD

If updating `status`, it must be one of:

- Not Started
- In Progress
- Completed

### Example Request

json
{
"status": "Completed"
}

Response:

- `200 OK`
- `404 Not Found`

---

# DELETE /api/courses/:id

### Description

Delete a course using the path parameter.

Example:

DELETE /api/courses/1

Response:

- `200 OK`
- `404 Not Found`

---

# DELETE /api/courses

### Description

Delete a course by sending the ID in the request body.

### Required Body Field

- `id`

### Example Request

json
{
"id": 1
}

Response:

- `200 OK`
- `404 Not Found`

---

# Data Storage Details

Data is stored in:

courses.json

If the file or directory does not exist, the application will **create them automatically**.

### Course Object Structure

| Field       | Type   | Description                       |
| ----------- | ------ | --------------------------------- |
| id          | number | Auto-generated ID starting from 1 |
| name        | string | Course name                       |
| description | string | Course description                |
| target_date | string | Date in YYYY-MM-DD format         |
| status      | string | Course status                     |
| created_at  | string | ISO timestamp                     |

Allowed status values:

Not Started
In Progress
Completed

---

# Troubleshooting

## Server Not Starting on Port 5000

- Ensure **Node.js** is installed
- Verify no other process is using port **5000**
- Confirm `app.js` exists in the project directory

---

## Data File Not Created or Write Errors

Ensure the application has permission to create/write files in the project directory.

The application automatically creates:

courses.json

if it does not exist.

---

## Invalid Date Errors

Ensure `target_date` is formatted as:

YYYY-MM-DD

Example:

2026-05-01

---

## Invalid Status Errors

Allowed values:

Not Started
In Progress
Completed

---

## JSON Parsing Issues in courses.json

If `courses.json` becomes corrupted:

- The application attempts to reset it to an empty array
- You can manually edit or delete the file to reset the data

---

# File Structure

project-root/
│
├── app.js
├── courses.json
└── package.json

| File         | Description                      |
| ------------ | -------------------------------- |
| app.js       | Main server and API logic        |
| courses.json | Data storage file (auto-created) |
| package.json | Dependencies and start script    |

---
