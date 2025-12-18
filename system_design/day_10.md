# Day 10: API Design - REST and Beyond

## Overview

**Topic**: Designing clean, scalable APIs
**Estimated Time**: 60 minutes
**Difficulty**: Intermediate

## Prerequisites

- Days 1-9 completed
- Basic HTTP knowledge
- Understanding of client-server architecture

## Time Breakdown

- **Learn (20 min)**: API design principles
- **Practice (30 min)**: API design exercises
- **Reflect (10 min)**: Style comparison

## API Design Principles

### REST Fundamentals

- **Resources**: Nouns, not verbs (/users, not /getUsers)
- **HTTP Methods**: GET, POST, PUT, PATCH, DELETE
- **Stateless**: Each request contains all needed info
- **Uniform Interface**: Consistent patterns

### HTTP Methods

| Method | Action  | Idempotent? |
| ------ | ------- | ----------- |
| GET    | Read    | Yes         |
| POST   | Create  | No          |
| PUT    | Replace | Yes         |
| PATCH  | Update  | Yes         |
| DELETE | Remove  | Yes         |

### Status Codes

- **2xx**: Success (200 OK, 201 Created, 204 No Content)
- **3xx**: Redirect (301, 302, 304)
- **4xx**: Client error (400 Bad Request, 401, 403, 404)
- **5xx**: Server error (500, 502, 503)

### API Versioning

- URL: `/v1/users`
- Header: `Accept: application/vnd.api+json;version=1`
- Query: `/users?version=1`

### Pagination

- Offset: `?limit=20&offset=40`
- Cursor: `?limit=20&cursor=abc123`

### Rate Limiting

- Protect from abuse
- Return 429 Too Many Requests
- Include headers: X-RateLimit-Limit, X-RateLimit-Remaining

### REST vs GraphQL vs gRPC

| Feature       | REST            | GraphQL          | gRPC            |
| ------------- | --------------- | ---------------- | --------------- |
| Data fetching | Fixed endpoints | Flexible queries | Defined methods |
| Over-fetching | Common          | Solved           | N/A             |
| Performance   | Good            | Good             | Excellent       |
| Best for      | Public APIs     | Complex UIs      | Microservices   |

## Tasks

### Task 1: Design URL Shortener API (15 min)

**Endpoints**:

| Method | Endpoint           | Description      | Request | Response |
| ------ | ------------------ | ---------------- | ------- | -------- |
| POST   | /urls              | Create short URL |         |          |
| GET    | /urls/{code}       | Get URL info     |         |          |
| GET    | /{code}            | Redirect         |         |          |
| DELETE | /urls/{code}       | Delete URL       |         |          |
| GET    | /urls/{code}/stats | Get analytics    |         |          |

**Example request/response for POST /urls**:

```json
// Request
{
  "long_url": "https://example.com/very/long/path",
  "custom_code": "mylink",  // optional
  "expires_at": "2024-12-31"  // optional
}

// Response (201 Created)
{
  "short_code": "abc123",
  "short_url": "https://short.ly/abc123",
  "long_url": "https://example.com/very/long/path",
  "created_at": "2024-01-15T10:30:00Z",
  "expires_at": "2024-12-31T00:00:00Z"
}
```

### Task 2: Error Handling (10 min)

Design error responses:

**URL not found**:

```json
{
  "error": {
    "code": "___",
    "message": "___",
    "details": "___"
  }
}
```

**Rate limited**:

```json

```

**Invalid request**:

```json

```

### Task 3: Rate Limiting Design (10 min)

Design rate limiting for URL shortener:

| Endpoint               | Limit | Window |
| ---------------------- | ----- | ------ |
| POST /urls             |       |        |
| GET /{code}            |       |        |
| GET /urls/{code}/stats |       |        |

**Rate limit algorithm**: ******\_\_\_******
**Storage for counters**: ******\_\_\_******

### Task 4: API Documentation (10 min)

Write OpenAPI-style documentation for one endpoint:

```yaml
/urls:
  post:
    summary: ___
    requestBody: ___
    responses:
      201: ___
      400: ___
      429: ___
```

## Output Requirements

- [ ] Complete API endpoints designed
- [ ] Error responses defined
- [ ] Rate limiting planned
- [ ] Documentation started

## Validation

- Are your endpoints RESTful?
- Do you use appropriate HTTP methods and codes?
- Is error handling consistent?

## Success Criteria

- [ ] Understand REST principles
- [ ] Can design clean API endpoints
- [ ] Know rate limiting strategies
- [ ] Can document APIs

## Common Pitfalls

- **Verbs in URLs**: Use /users, not /getUsers
- **Inconsistent naming**: Pick a convention and stick to it
- **Poor error messages**: Be specific and helpful
- **No versioning**: Plan for change from start

## Next Steps

Tomorrow: **Day 11 - Microservices** - Breaking down monoliths

## Social Post Template

"Day 10/31 System Design: API design deep dive. REST principles, HTTP methods, rate limiting, error handling. Designed complete API for URL shortener. #SystemDesign #APIDesign"

## Notes

_Your personal observations and diagrams go here._

---
