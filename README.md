# Test Rest API

A simple REST API built with Flask for managing companies and their employees.

## Project Structure

```
Test-Rest-API/
├── app.py              # Flask application with API endpoints
├── database.py         # SQLAlchemy database models
├── requirements.txt    # Python dependencies
├── company_db.sqlite   # SQLite database (auto-generated)
└── README.md          # This file
```

## Features

- **Company Management**: Create and retrieve companies
- **Employee Management**: Add and retrieve employees for each company
- **SQLite Database**: Two tables - Company and Employee with relationships
- **RESTful API**: Standard HTTP methods (GET, POST)
- **Error Handling**: Comprehensive error responses with status codes

## Installation

1. Clone the repository:
```bash
git clone https://github.com/peter-j-r-mendozaAccenture/Test-Rest-API.git
cd Test-Rest-API
```

2. Create a virtual environment:
```bash
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
```

3. Install dependencies:
```bash
pip install -r requirements.txt
```

## Running the API

```bash
python app.py
```

The API will be available at `http://localhost:5000`

## API Endpoints

### Health Check
- **GET** `/api/health` - Check if API is running

### Company Endpoints

- **GET** `/api/companies` - Get all companies
  ```bash
  curl http://localhost:5000/api/companies
  ```

- **GET** `/api/companies/<id>` - Get a specific company with all employees
  ```bash
  curl http://localhost:5000/api/companies/1
  ```

- **POST** `/api/companies` - Create a new company
  ```bash
  curl -X POST http://localhost:5000/api/companies \
    -H "Content-Type: application/json" \
    -d '{
      "name": "Tech Corp",
      "industry": "Technology",
      "founded_year": 2020
    }'
  ```

### Employee Endpoints

- **GET** `/api/companies/<company_id>/employees` - Get all employees for a company
  ```bash
  curl http://localhost:5000/api/companies/1/employees
  ```

- **GET** `/api/employees/<id>` - Get a specific employee
  ```bash
  curl http://localhost:5000/api/employees/1
  ```

- **POST** `/api/companies/<company_id>/employees` - Add employee to a company
  ```bash
  curl -X POST http://localhost:5000/api/companies/1/employees \
    -H "Content-Type: application/json" \
    -d '{
      "name": "John Doe",
      "position": "Software Engineer",
      "email": "john@techcorp.com"
    }'
  ```

## Database Schema

### Company Table
- `id` (Integer, Primary Key)
- `name` (String, Unique)
- `industry` (String)
- `founded_year` (Integer)
- `created_at` (DateTime)

### Employee Table
- `id` (Integer, Primary Key)
- `name` (String)
- `position` (String)
- `email` (String, Unique)
- `company_id` (Integer, Foreign Key)
- `created_at` (DateTime)

## Response Format

All endpoints return JSON responses with the following structure:

**Success Response:**
```json
{
  "status": "success",
  "message": "Operation description",
  "data": { /* ... */ },
  "count": 1
}
```

**Error Response:**
```json
{
  "status": "error",
  "message": "Error description"
}
```

## HTTP Status Codes

- `200 OK` - Successful GET request
- `201 Created` - Successful POST request
- `400 Bad Request` - Missing or invalid fields
- `404 Not Found` - Resource not found
- `409 Conflict` - Resource already exists
- `500 Internal Server Error` - Server error

## Example Workflow

1. Create a company:
```bash
curl -X POST http://localhost:5000/api/companies \
  -H "Content-Type: application/json" \
  -d '{"name": "Accenture", "industry": "Consulting", "founded_year": 1989}'
```

2. Add employees to the company:
```bash
curl -X POST http://localhost:5000/api/companies/1/employees \
  -H "Content-Type: application/json" \
  -d '{"name": "Alice Johnson", "position": "Manager", "email": "alice@accenture.com"}'

curl -X POST http://localhost:5000/api/companies/1/employees \
  -H "Content-Type: application/json" \
  -d '{"name": "Bob Smith", "position": "Developer", "email": "bob@accenture.com"}'
```

3. Get company with all employees:
```bash
curl http://localhost:5000/api/companies/1
```

## License

MIT License
