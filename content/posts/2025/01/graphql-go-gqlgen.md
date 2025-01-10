---
title: "Setting Up a GraphQL API with Golang and GQLGen"
date: 2025-01-10
draft: false
---

GraphQL is a powerful query language for APIs, and GQLGen makes it easy to build a GraphQL server in Go. In this tutorial, we'll go through the steps to set up a simple GraphQL API using Golang and GQLGen.

### Prerequisites

Before we start, make sure you have the following installed:

- [Go](https://golang.org/dl/)
- [Git](https://git-scm.com/)

### Step 1: Create a New Go Module

Start by creating a new Go module:

```bash
mkdir gqlgen-example
cd gqlgen-example
go mod init gqlgen-example
```

### Step 2: Install GQLGen

Install the GQLGen tool and dependencies:

```bash
go install github.com/99designs/gqlgen@latest
go get github.com/99designs/gqlgen/graphql-go
```

Run the `gqlgen` command to initialize your project:

```bash
gqlgen init
```

This command generates a basic GraphQL setup, including a `schema.graphqls` file and boilerplate code.

### Step 3: Define Your Schema

Edit the `schema.graphqls` file to define your GraphQL schema. For example:

```graphql
type Query {
  hello: String!
}
```

### Step 4: Implement Resolvers

GQLGen generates resolver interfaces based on your schema. Implement the `Query` resolver in `resolver.go`:

```go
package gqlgen_example

func (r *queryResolver) Hello() (string, error) {
    return "Hello, world!", nil
}
```

### Step 5: Run the Server

Start your GraphQL server by running:

```bash
go run server.go
```

You can now access the GraphQL playground at `http://localhost:8080/` to test your API.

### Step 6: Test Your API

In the GraphQL playground, run the following query:

```graphql
query {
  hello
}
```

You should see the response:

```json
{
  "data": {
    "hello": "Hello, world!"
  }
}
```

### Conclusion

That's it! You've successfully set up a basic GraphQL API using Golang and GQLGen. From here, you can expand your schema and resolvers to build a more complex API.