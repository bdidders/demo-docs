---
title: API Reference Overview
description: Complete API reference for Docify
order: 1
---

# API Reference

Docify provides both GraphQL and REST APIs for programmatic access to your documentation.

## Available Endpoints

### GraphQL

**Endpoint:** `POST /graphql`

Full-featured GraphQL API for querying and mutating spaces, documents, and content.

### REST API

**Base URL:** `https://api.docify.com/v1`

RESTful endpoints for file uploads, webhooks, and legacy integrations.

## Authentication

All API requests require authentication via JWT token:

```bash
curl -H "Authorization: Bearer YOUR_TOKEN" \\
  -X POST https://api.docify.com/graphql \\
  -H "Content-Type: application/json" \\
  -d '{"query": "query { spaces { id name } }"}'
```

## Quick Links

- [GraphQL Queries](./graphql-queries.md) - Query data from Docify
- [GraphQL Mutations](./graphql-mutations.md) - Modify spaces and documents
- [REST Endpoints](./rest-api.md) - RESTful operations
- [Authentication](./authentication.md) - API authentication methods
- [Rate Limiting](./rate-limiting.md) - Request rate limits
- [Error Handling](./error-handling.md) - Error responses and codes

## Getting Started

1. [Create an API Token](./authentication.md)
2. [Make Your First Request](./authentication.md#making-requests)
3. [Explore the Schema](./graphql-queries.md)

---

See a specific example? Check the [Examples](../examples/) section.
