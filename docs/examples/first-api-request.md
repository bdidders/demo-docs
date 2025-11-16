---
title: First API Request
description: Make your first authenticated API request
order: 2
---

# Make Your First API Request

Let's make your first API call to Docify!

## Prerequisites

- [API Token](../api-reference/authentication.md) generated
- curl or your favorite HTTP client
- Text editor or IDE

## Using curl

### Step 1: Get Your Token

From your Docify settings, copy your API token. It looks like:

```
sk_live_xxxxxxxxxxxxxxxxxxxxxxxx
```

### Step 2: Query Your Spaces

```bash
curl -X POST https://api.docify.com/graphql \\
  -H "Authorization: Bearer sk_live_xxxxxxxxxxxxxxxxxxxxxxxx" \\
  -H "Content-Type: application/json" \\
  -d '{
    "query": "query { spaces { id name slug } }"
  }'
```

### Step 3: View the Response

You should see something like:

```json
{
  "data": {
    "spaces": [
      {
        "id": "space_abc123",
        "name": "API Documentation",
        "slug": "api-docs"
      }
    ]
  }
}
```

## Using JavaScript

```javascript
const token = 'sk_live_xxxxxxxxxxxxxxxxxxxxxxxx';

async function getSpaces() {
  const response = await fetch('https://api.docify.com/graphql', {
    method: 'POST',
    headers: {
      Authorization: `Bearer ${token}`,
      'Content-Type': 'application/json',
    },
    body: JSON.stringify({
      query: `
        query {
          spaces {
            id
            name
            slug
          }
        }
      `,
    }),
  });

  const data = await response.json();
  console.log(data);
  return data;
}

getSpaces();
```

## Using Python

```python
import requests

token = 'sk_live_xxxxxxxxxxxxxxxxxxxxxxxx'
url = 'https://api.docify.com/graphql'

headers = {
    'Authorization': f'Bearer {token}',
    'Content-Type': 'application/json',
}

query = '''
  query {
    spaces {
      id
      name
      slug
    }
  }
'''

response = requests.post(url, json={'query': query}, headers=headers)
print(response.json())
```

## Next Steps

- [Query Spaces in Detail](./query-spaces.md)
- [Search Documents](./search-documents.md)
- [API Reference](../api-reference/graphql-queries.md)

---

**Troubleshooting?** Check [Authentication Issues](../api-reference/authentication.md#troubleshooting)
