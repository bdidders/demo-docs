---
title: Architecture Overview
description: Understanding Docify's system architecture
order: 1
---

# Architecture Overview

Docify is built as a modern, scalable monorepo with a GraphQL API backend and React frontend.

## High-Level Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                       Client (React)                        │
│  - Chakra UI Components                                     │
│  - Apollo Client (GraphQL)                                  │
│  - Authentication Context                                   │
└────────────────────────┬────────────────────────────────────┘
                         │ GraphQL Queries/Mutations
                         │ (via Apollo Client)
┌────────────────────────▼────────────────────────────────────┐
│               GraphQL API (Apollo Server)                   │
│  - Authentication & JWT                                    │
│  - Resolvers (Queries, Mutations)                          │
│  - MongoDB Data Layer                                      │
└────────────────────────┬────────────────────────────────────┘
                         │
        ┌────────────────┼────────────────┐
        │                │                │
┌───────▼────────┐  ┌────▼──────────┐  ┌─▼──────────────────┐
│   MongoDB      │  │ GitHub Repos  │  │ Environment Config │
│   - Spaces     │  │ - Source Sync │  │ - JWT Keys         │
│   - Documents  │  │ - Git History │  │ - Database URI     │
│   - Users      │  └───────────────┘  └────────────────────┘
└────────────────┘
```

## Core Components

### Frontend (React + Vite)

**Location:** `client/`

```
client/
├── src/
│   ├── components/        # Reusable UI components
│   ├── sections/         # Composed page sections
│   ├── pages/            # Full-page views
│   ├── contexts/         # React contexts (auth, admin)
│   ├── graphql/          # Apollo queries & mutations
│   ├── hooks/            # Custom React hooks
│   └── lib/              # Utilities (Apollo Client setup)
└── vite.config.ts        # Vite build configuration
```

**Stack:**

- React 18 - Component library
- Chakra UI v3 - UI components
- Apollo Client - GraphQL client
- TypeScript - Type safety
- Vite - Build tool

### Backend (Node.js + Express)

**Location:** `server/`

```
server/
├── src/
│   ├── index.ts          # Server entry point
│   ├── schema.ts         # GraphQL schema definitions
│   ├── resolvers.ts      # GraphQL resolver logic
│   ├── mongo.ts          # MongoDB connection
│   ├── auth/             # Authentication utilities
│   ├── repos/            # Git repository handling
│   ├── routes/           # REST API endpoints
│   └── utils/            # Helper functions
└── package.json
```

**Stack:**

- Express - Web framework
- Apollo Server 4 - GraphQL server
- MongoDB (native) - Database
- jsonwebtoken - JWT handling
- sharp - Image processing

### Shared Types

**Location:** `shared/`

```
shared/
└── src/
    ├── types/            # TypeScript interfaces
    └── enums/            # Enum definitions
```

All types defined once, used by both server and client.

## Data Flow

### User Authentication Flow

```
1. User submits credentials (login form)
                    │
2. Client sends GraphQL mutation (login)
                    │
3. Server validates password against bcrypt hash
                    │
4. Server generates JWT token
                    │
5. Token returned to client
                    │
6. Client stores in localStorage
                    │
7. Apollo Client adds token to subsequent requests
                    │
8. Server validates token in middleware
                    │
9. User context injected into GraphQL context
```

### Document Sync Flow

```
1. GitHub webhook triggers (on push)
                    │
2. Server clones/pulls repository
                    │
3. Scans configured docs folder
                    │
4. For each markdown file:
   - Parses frontmatter
   - Extracts headings
   - Generates HTML
                    │
5. Stores in MongoDB:
   - Document metadata
   - Content (markdown + HTML)
   - TOC entries
                    │
6. Client queries updated documents
                    │
7. Frontend renders with syntax highlighting
```

## Database Schema

### Collections

**users**

- `_id` - MongoDB ObjectId
- `email` - Unique email
- `passwordHash` - bcrypted password
- `role` - 'admin', 'editor', 'viewer'
- `createdAt` - Timestamp

**documents**

- `_id` - MongoDB ObjectId
- `spaceId` - Reference to space
- `title` - Document title
- `slug` - URL-safe identifier
- `path` - File path in repo
- `content` - Raw markdown
- `htmlContent` - Rendered HTML
- `frontmatter` - Parsed metadata
- `createdAt`, `updatedAt` - Timestamps

**spaces**

- `_id` - MongoDB ObjectId
- `name` - Space display name
- `slug` - URL identifier
- `repositoryUrl` - GitHub repo URL
- `branch` - Default branch
- `docsPath` - Docs folder path
- `lastSyncAt` - Last sync timestamp

## API Communication

### GraphQL

All data operations go through GraphQL:

```
POST /graphql
Content-Type: application/json
Authorization: Bearer <JWT>

{
  "query": "...",
  "variables": { ... }
}
```

### REST (File Upload)

File uploads use REST:

```
POST /api/upload
Authorization: Bearer <JWT>
Content-Type: multipart/form-data
```

## Performance Optimizations

### Frontend

- Code splitting with Vite
- Apollo Client caching
- Image optimization (Chakra UI)
- Lazy loading for routes

### Backend

- MongoDB indexing on frequently queried fields
- GraphQL DataLoader for N+1 prevention
- Redis caching (future)
- Database connection pooling

## Security Layers

1. **JWT Authentication** - All requests verified
2. **Role-Based Access Control** - Permissions enforced
3. **Input Validation** - Zod/runtime validation
4. **MongoDB Injection Prevention** - Parameterized queries
5. **CORS** - Cross-origin request control

---

See [Advanced Topics](../advanced/scaling.md) for deployment and scaling information.
