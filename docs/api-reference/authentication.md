---
title: Authentication
description: Authenticate with the Docify API
order: 4
---

# Authentication

All Docify API requests require authentication using JSON Web Tokens (JWT).

## Getting an API Token

### Step 1: Access Settings

1. Log in to Docify
2. Go to **Settings** → **API**
3. Click **Generate Token**

### Step 2: Configure Token

**Token Name** (optional): Describe where you'll use this token

**Expiration:** Choose an expiration date

- 30 days
- 90 days
- 1 year
- Never expires (not recommended)

**Scope:** Select permissions

- `read:spaces` - Read-only access to spaces
- `read:documents` - Read-only access to documents
- `write:documents` - Create/edit documents
- `admin` - Full access (use with caution)

### Step 3: Copy Token

**⚠️ Important:** Save your token somewhere safe. You won't be able to see it again!

## Using Your Token

### Authorization Header

Include your token in the `Authorization` header:

```bash
Authorization: Bearer sk_live_xxxxxxxxxxxxxxxxxxxxxxxx
```

### Example Request

```bash
curl -X POST https://api.docify.com/graphql \\
  -H "Authorization: Bearer sk_live_xxxxxxxxxxxxxxxxxxxxxxxx" \\
  -H "Content-Type: application/json" \\
  -d '{
    "query": "query { spaces { id name } }"
  }'
```

### JavaScript/Node.js

```typescript
const response = await fetch('https://api.docify.com/graphql', {
  method: 'POST',
  headers: {
    Authorization: 'Bearer sk_live_xxxxxxxxxxxxxxxxxxxxxxxx',
    'Content-Type': 'application/json',
  },
  body: JSON.stringify({
    query: `query { spaces { id name } }`,
  }),
});

const data = await response.json();
console.log(data);
```

### Python

```python
import requests

url = "https://api.docify.com/graphql"
headers = {
    "Authorization": "Bearer sk_live_xxxxxxxxxxxxxxxxxxxxxxxx",
    "Content-Type": "application/json",
}
query = """
  query {
    spaces {
      id
      name
    }
  }
"""

response = requests.post(url, json={"query": query}, headers=headers)
print(response.json())
```

## Token Management

### View Active Tokens

1. Go to **Settings** → **API**
2. See all generated tokens and their expiration dates

### Revoke a Token

1. Click the token in the list
2. Click **Revoke**
3. Confirm deletion

### Token Rotation

For security, rotate your tokens regularly:

1. Generate a new token
2. Update your applications to use the new token
3. Wait 24 hours for applications to stabilize
4. Revoke the old token

## Best Practices

✅ **Do:**

- Store tokens securely (environment variables, secrets manager)
- Use tokens with minimal required scope
- Rotate tokens regularly
- Set reasonable expiration dates
- Use different tokens for different applications

❌ **Don't:**

- Commit tokens to version control
- Share tokens via email or Slack
- Use the same token for multiple applications
- Set expiration to "never expires" unless necessary
- Display tokens in logs or error messages

## Troubleshooting

### 401 Unauthorized

Token is invalid or expired. Check:

- Token is correctly included in `Authorization` header
- Token hasn't been revoked
- Token hasn't expired

### 403 Forbidden

Token exists but doesn't have required permissions:

- Verify token scope includes the action
- Generate a new token with broader scope

---

**Next:** Make your [first API request](../examples/first-api-request.md)
