---
title: Querying Spaces
description: Retrieve and work with documentation spaces
order: 3
---

# Querying Spaces

Learn how to retrieve detailed information about your documentation spaces.

## Get All Spaces

Retrieve a list of all spaces you have access to:

```graphql
query {
  spaces {
    id
    name
    slug
    description
    createdAt
    documentCount
    repository {
      url
      branch
    }
  }
}
```

## Get Space by Slug

Query a specific space by its URL slug:

```graphql
query GetSpaceBySlug($slug: String!) {
  spaceBySlug(slug: $slug) {
    id
    name
    slug
    description
    documents {
      id
      title
      slug
    }
  }
}
```

Variables:

```json
{
  "slug": "api-docs"
}
```

## Get Space with Documents

Retrieve a space with all its documents and metadata:

```graphql
query GetSpaceWithDocs($id: ID!) {
  space(id: $id) {
    id
    name
    description
    createdAt
    updatedAt
    documents {
      id
      title
      slug
      path
      createdAt
      updatedAt
    }
    members {
      id
      email
      role
    }
  }
}
```

## Get Space Navigation Tree

Retrieve the hierarchical document structure:

```graphql
query GetSpaceNav($id: ID!) {
  spaceNavigation(id: $id) {
    id
    title
    slug
    children {
      id
      title
      slug
      children {
        id
        title
        slug
      }
    }
  }
}
```

## Real-World Example: React Hook

Fetch space data in a React component:

```typescript
import { useQuery, gql } from '@apollo/client';

const GET_SPACE = gql`
  query GetSpace($id: ID!) {
    space(id: $id) {
      id
      name
      description
      documents {
        id
        title
        slug
      }
    }
  }
`;

export function SpaceDetail({ spaceId }: { spaceId: string }) {
  const { data, loading, error } = useQuery(GET_SPACE, {
    variables: { id: spaceId }
  });

  if (loading) return <p>Loading...</p>;
  if (error) return <p>Error: {error.message}</p>;

  return (
    <div>
      <h1>{data.space.name}</h1>
      <p>{data.space.description}</p>
      <ul>
        {data.space.documents.map(doc => (
          <li key={doc.id}>{doc.title}</li>
        ))}
      </ul>
    </div>
  );
}
```

---

**Next:** [Search Documents](./search-documents.md)
