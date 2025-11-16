---
title: API Documentation Best Practices
description: Write clear, comprehensive API documentation
order: 1
---

# API Documentation Best Practices

Guidelines for writing effective API documentation that developers love.

## Structure

Every API endpoint should include:

1. **Overview** - What does this endpoint do?
2. **Parameters** - What inputs does it accept?
3. **Response** - What does it return?
4. **Examples** - Real-world usage
5. **Errors** - What can go wrong?

## Endpoint Documentation Template

```markdown
## Create Document

Create a new document in a space.

### Endpoint

\`\`\`
POST /api/spaces/:spaceId/documents
\`\`\`

### Authentication

Requires Bearer token with \`write:documents\` scope.

### Parameters

| Name    | Type   | Required | Description      |
| ------- | ------ | -------- | ---------------- |
| title   | string | yes      | Document title   |
| content | string | yes      | Markdown content |
| slug    | string | no       | Custom URL slug  |

### Response

Returns a Document object:

\`\`\`json
{
"id": "doc_123",
"title": "My Document",
"slug": "my-document",
"createdAt": "2025-01-15T10:00:00Z"
}
\`\`\`

### Example

\`\`\`bash
curl -X POST https://api.docify.com/spaces/space_123/documents \\
-H "Authorization: Bearer sk_live_xxx" \\
-H "Content-Type: application/json" \\
-d '{
"title": "Getting Started",
"content": "# Welcome\\n..."
}'
\`\`\`

### Errors

| Code | Message                  | Solution                              |
| ---- | ------------------------ | ------------------------------------- |
| 400  | Missing required field   | Check all required parameters         |
| 401  | Unauthorized             | Verify your API token                 |
| 403  | Insufficient permissions | Token needs \`write:documents\` scope |
| 409  | Slug already exists      | Choose a different slug               |
```

## Code Examples

Always provide examples in multiple languages:

- JavaScript/TypeScript
- Python
- cURL/Bash

Show realistic, copy-paste-ready code:

```typescript
// ✅ Good: Complete, realistic example
const createDocument = async (spaceId: string, title: string, content: string) => {
  const response = await fetch(`https://api.docify.com/spaces/${spaceId}/documents`, {
    method: 'POST',
    headers: {
      Authorization: `Bearer ${process.env.DOCIFY_TOKEN}`,
      'Content-Type': 'application/json',
    },
    body: JSON.stringify({ title, content }),
  });

  if (!response.ok) {
    throw new Error(`Failed to create document: ${response.statusText}`);
  }

  return response.json();
};
```

## Error Documentation

Document every possible error:

```markdown
### Possible Errors

**400 Bad Request**

- Missing required field: \`title\`
- Invalid content: Must be valid Markdown
- Title too long: Maximum 255 characters

**401 Unauthorized**

- Token not provided
- Token expired
- Token revoked

**403 Forbidden**

- User doesn't have write access
- Space is archived
- Operation not allowed for your role
```

## Rate Limits

Document rate limiting clearly:

```markdown
## Rate Limiting

API requests are limited to:

- **200 requests per minute** for authenticated users
- **20 requests per minute** for unauthenticated requests

When rate limit is exceeded, you'll receive a **429 Too Many Requests** response with a \`Retry-After\` header.

\`\`\`
HTTP/1.1 429 Too Many Requests
Retry-After: 60
\`\`\`

**Tips:**

- Batch requests when possible
- Use webhooks instead of polling
- Cache responses on your end
```

## Best Practices Summary

✅ **Do:**

- Show real, working examples
- Document all parameters and types
- List all possible error codes
- Explain the "why" not just the "what"
- Keep examples short and focused

❌ **Don't:**

- Use placeholder examples that won't run
- Document only the "happy path"
- Leave error cases undocumented
- Assume developer knowledge
- Make examples too complex

---

**More:** [Documentation Standards](./documentation-standards.md)
