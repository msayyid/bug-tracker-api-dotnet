# Bug Tracker API

A simple REST API for managing bug tickets, built with **C#**, **ASP.NET Core**, and **.NET 10**.

This project was created to practise controller-based API development, routing, CRUD operations, filtering, validation, and HTTP status handling.

## Features

- Get all bug tickets
- Get a bug ticket by ID
- Filter bugs by:
  - Severity
  - Resolution status
- Create new bug tickets
- Fully update existing bug tickets
- Update only the resolution status of a bug
- Delete bug tickets
- Request validation
- Appropriate HTTP status codes

## Tech Stack

- C#
- .NET 10
- ASP.NET Core
- ASP.NET Core Controllers
- LINQ

## Bug Model

Each bug ticket contains:

```json
{
  "id": 1,
  "title": "Login button not working",
  "severity": "High",
  "isResolved": false
}
```

Supported severity values:

- Low
- Medium
- High
- Critical

## API Endpoints

| Method | Endpoint | Description |
|---|---|---|
| GET | `/bugs` | Get all bugs |
| GET | `/bugs/{id}` | Get a bug by ID |
| POST | `/bugs` | Create a new bug |
| PUT | `/bugs/{id}` | Fully update a bug |
| PATCH | `/bugs/{id}` | Update the resolution status |
| DELETE | `/bugs/{id}` | Delete a bug |

## Filtering

Filter by severity:

```http
GET /bugs?severity=High
```

Filter by resolution status:

```http
GET /bugs?isResolved=false
```

Combine filters:

```http
GET /bugs?severity=Critical&isResolved=false
```

## Example POST Request

```http
POST /bugs
Content-Type: application/json
```

```json
{
  "id": 5,
  "title": "Search button not working",
  "severity": "High",
  "isResolved": false
}
```

A successful creation returns:

```text
201 Created
```

along with the created bug ticket and a location pointing to its GET-by-ID endpoint.

## Example PATCH Request

```http
PATCH /bugs/3
Content-Type: application/json
```

```json
{
  "isResolved": true
}
```

This updates only the `isResolved` property while keeping the rest of the bug ticket unchanged.

## Validation

The API currently validates that:

- Title is not empty
- Severity is not empty
- Severity is one of:
  - Low
  - Medium
  - High
  - Critical

Invalid requests return:

```text
400 Bad Request
```

Missing resources return:

```text
404 Not Found
```

Successful deletions return:

```text
204 No Content
```

## Running the Project

Make sure the .NET SDK is installed.

Clone the repository:

```bash
git clone <repository-url>
```

Move into the project directory:

```bash
cd BugTrackerApi
```

Run the application:

```bash
dotnet run
```

The terminal will display the local URL where the API is running.

## Testing

A `requests.http` file is included in the project and can be used from IDEs such as JetBrains Rider to test the API endpoints.

## Current Limitation

The project currently uses an **in-memory list** for data storage.

This means any created, updated, or deleted data is reset when the application restarts.

Database persistence will be added in future projects as I continue learning ASP.NET Core and Entity Framework Core.

## Project Purpose

This project was built as part of my C# and ASP.NET Core learning path, focusing on:

- REST API design
- ASP.NET Core Controllers
- Routing
- Model binding
- LINQ
- CRUD operations
- HTTP status codes
- Validation
- Controller response types
