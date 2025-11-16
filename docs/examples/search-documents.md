---
title: Search Documents
description: Implement full-text search across documentation
order: 4
---

# Searching Documents

Implement full-text search functionality to help users find documentation quickly.

## Basic Search Query

```graphql
query SearchDocuments($query: String!, $spaceId: ID!) {
  search(query: $query, spaceId: $spaceId, limit: 10) {
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

Variables:

```json
{
  "query": "authentication",
  "spaceId": "space_abc123"
}
```

## Search with Pagination

```graphql
query SearchDocuments($query: String!, $spaceId: ID!, $limit: Int!, $offset: Int!) {
  search(query: $query, spaceId: $spaceId, limit: $limit, offset: $offset) {
    total
    hasMore
    results {
      id
      title
      slug
      excerpt
      score
      tags
    }
  }
}
```

Variables:

```json
{
  "query": "API",
  "spaceId": "space_abc123",
  "limit": 20,
  "offset": 0
}
```

## React Search Component

```typescript
import { useState } from 'react';
import { useQuery, gql } from '@apollo/client';
import { Input, Stack, Box, Text, Link } from '@chakra-ui/react';

const SEARCH_DOCS = gql`
  query SearchDocuments(
    $query: String!
    $spaceId: ID!
  ) {
    search(query: $query, spaceId: $spaceId, limit: 10) {
      total
      results {
        id
        title
        slug
        excerpt
      }
    }
  }
`;

export function SearchBar({ spaceId }: { spaceId: string }) {
  const [searchTerm, setSearchTerm] = useState('');

  const { data, loading } = useQuery(SEARCH_DOCS, {
    variables: {
      query: searchTerm,
      spaceId
    },
    skip: searchTerm.length < 2
  });

  const results = data?.search?.results || [];

  return (
    <Box>
      <Input
        placeholder="Search documentation..."
        value={searchTerm}
        onChange={(e) => setSearchTerm(e.target.value)}
      />

      {loading && <Text>Searching...</Text>}

      <Stack spacing={2} mt={4}>
        {results.map(doc => (
          <Box key={doc.id} p={2} borderBottom="1px solid #eee">
            <Link href={`/docs/${doc.slug}`} fontWeight="bold">
              {doc.title}
            </Link>
            <Text fontSize="sm" color="gray.600">
              {doc.excerpt}
            </Text>
          </Box>
        ))}
      </Stack>

      {!loading && results.length === 0 && searchTerm && (
        <Text color="gray.500">No results found</Text>
      )}
    </Box>
  );
}
```

## Search Suggestions

Add auto-complete suggestions as user types:

```graphql
query SearchSuggestions($query: String!, $spaceId: ID!) {
  searchSuggestions(query: $query, spaceId: $spaceId, limit: 5) {
    title
    slug
  }
}
```

## Highlighting Search Results

Use Apollo Client cache to highlight matching terms:

```typescript
function highlightSearchTerm(text: string, term: string) {
  const regex = new RegExp(`(${term})`, 'gi');
  return text.replace(regex, '<mark>$1</mark>');
}
```

---

**More examples:** [Creating Documents](./create-document.md)
