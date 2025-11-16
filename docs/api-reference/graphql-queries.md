---
title: GraphQL Queries
description: Query spaces, documents, and content
order: 2
---

# GraphQL Queries

Learn how to query your documentation data using GraphQL.

## Common Queries

### List All Spaces

```graphql
query {
  spaces {
    id
    name
    slug
    description
    createdAt
    documentCount
  }
}
```

**Response:**

```json
{
  "data": {
    "spaces": [
      {
        "id": "space_abc123",
        "name": "API Documentation",
        "slug": "api-docs",
        "description": "Complete API reference",
        "createdAt": "2025-01-15T10:00:00Z",
        "documentCount": 42
      }
    ]
  }
}
```

### Get Space Details

```graphql
query GetSpace($id: ID!) {
  space(id: $id) {
    id
    name
    slug
    repository {
      url
      branch
      docsPath
    }
    documents {
      id
      title
      slug
      path
    }
  }
}
```

**Variables:**

```json
{
  "id": "space_abc123"
}
```

### Search Documents

```graphql
query SearchDocs($query: String!, $spaceId: ID!) {
  search(query: $query, spaceId: $spaceId) {
    total
    results {
      id
      title
      slug
      excerpt
      score
    }
  }
}
```

### Get Document Content

```graphql
query GetDocument($id: ID!) {
  document(id: $id) {
    id
    title
    slug
    content
    htmlContent
    frontmatter {
      title
      description
      tags
    }
    tableOfContents {
      level
      title
      id
    }
  }
}
```

## Query Variables

GraphQL supports variables to make queries dynamic:

```graphql
query GetSpaceBySlug($slug: String!) {
  spaceBySlug(slug: $slug) {
    id
    name
    documents {
      id
      title
    }
  }
}
```

Pass variables:

```bash
curl -X POST https://api.docify.com/graphql \\
  -H "Authorization: Bearer TOKEN" \\
  -H "Content-Type: application/json" \\
  -d '{
    "query": "...",
    "variables": { "slug": "api-docs" }
  }'
```

## Pagination

For large result sets, use pagination:

```graphql
query ListDocuments($spaceId: ID!, $limit: Int, $offset: Int) {
  documents(spaceId: $spaceId, limit: $limit, offset: $offset) {
    total
    hasMore
    items {
      id
      title
    }
  }
}
```

---

**Next:** Learn about [GraphQL Mutations](./graphql-mutations.md)
