---
tags:
  - technologies
date: 2023-09-1
---
- Open source [[APIs (Application Programming Interface)|API]] query language/runtime.
- Allows clients to specify exactly what data they need.
- Strong alternative to REST APIs.
- Single endpoint (`/graphql`) for all operations.
- Supports queries, mutations and subscriptions.
# Components

- `Schema`: defines types and structure of API
- `Query`: read data
- `Mutation`: modify data (create, update, delete).
- `Resolver`: backend function that returns data.
- `Type`: custom data structures (e.g. `User`, `Post`)
- `Subscription`: real-time updates ([[WebSocket]] based)
# Query

- Example query:

```graphql
query {
  user(id: "123") {
    name
    email
    posts {
      title
      published
    }
  }
}
```
# Mutation

- Example mutation:

```graphql
mutation {
  createPost(title: "Hello", content: "GraphQL is cool!") {
    id
    title
  }
}
```
# Sample Schema (DSL)

- Example schema:

```graphql
type User {
  id: ID!
  name: String!
  email: String!
  posts: [Post]
}

type Post {
  id: ID!
  title: String!
  content: String
  published: Boolean!
}

type Query {
  user(id: ID!): User
  allPosts: [Post]
}

type Mutation {
  createPost(title: String!, content: String): Post
}
```