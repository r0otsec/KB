---
tags:
  - technologies
date: 2023-09-1
---
- Structured interface.
- Allows software/systems to communicate with each other using rules.
- Expose data and functions from one app to another.
- Common in web apps, cloud, mobile apps and microservices.
# Types of APIs

| Type                | Description                                                    |
| ------------------- | -------------------------------------------------------------- |
| Web API (HTTP/REST) | Most common types, uses HTTP verbs.                            |
| SOAP                | XML-based, heavier and more strict.                            |
| GraphQL             | Flexible query based API from Facebook.                        |
| Internal API        | Meant for use within an organization.                          |
| External API        | Public-facing APIs, (e.g. Twitter API).                        |
| Hardware/Native API | Interface to operating system or hardware (e.g. WinAPI, POSIX) |
# REST API Example

- `GET` - retrieves resource.
- `POST` - creates resouce.
- `PUT/PATCH` - updates resource.
- `DELETE` - remove resource.

- An example:

```http
GET /api/v1/users/123 HTTP/1.1
Host: example.com
Authorization: Bearer eyJhbGci...
```

```json
{
  "id": 123,
  "username": "jdoe",
  "email": "jdoe@example.com"
}
```
# Authentication Methods

- API Keys (simple token).
- Basic Auth (`Authorization: Basic base64(user:pass)`)
- OAuth2 (Google, GitHub, etc..).
- [[JSON Web Tokens (JWT)]] - signed tokens that carry identity/permissions.
# API Documentation & Standards

- OpenAPI (Swagger) - standard for REST APIs.
- Postman - tool to interact with and test APIs.
- GraphQL Schema - used to define allowed query structure.
# Design Principles

- Use proper HTTP methods.
- Use nouns for resource names: `/users`, `/posts/45`.
- Include versioning: `/api/v1/`
- Return appropriate HTTP status codes.