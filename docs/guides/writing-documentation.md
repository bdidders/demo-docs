---
title: Writing Documentation
description: Best practices for writing clear documentation
order: 1
---

# Writing Great Documentation

Documentation is a reflection of your project. Here's how to write clear, helpful, and maintainable docs.

## Writing Principles

### 1. Know Your Audience

Write for your primary users:

- New team members learning the system
- Experienced developers using references
- Non-technical stakeholders
- Future you, reviewing six months from now

### 2. Start with Clarity

Clear writing is **kind** writing. Your documentation should:

- Use simple, direct language
- Explain complex concepts gradually
- Provide examples before edge cases
- Anticipate common questions

### 3. Structure for Scannability

Readers don't read top-to-bottom; they scan. Make it easy:

```markdown
# Main heading (page topic)

## Subsection headings (major areas)

### Specific topics (details)

- Use bullet points
- For lists of 3+ items
- Short, scannable format

> Use blockquotes for important points
```

## Document Structure Template

Every documentation page should follow this structure:

```markdown
---
title: Your Page Title
description: One-line summary
order: 10
---

# Your Page Title

## Quick Overview

Paragraph explaining what this page covers and why someone should care.

## Prerequisites

- What they should know before reading
- Tools they need installed
- Related pages to read first

## Main Content Section 1

Step-by-step instructions or conceptual explanation.

### Code Example

Show, don't just tell. Include realistic code samples.

## Main Content Section 2

Continue with logical progression.

## Common Issues

Anticipate problems and provide solutions.

## Related Pages

- [Link to related topic](./related-page.md)
- [Another useful page](./another-page.md)
```

## Code Examples

### Show Realistic Examples

```typescript
// ✅ Good: Real-world code that users can copy
import { Space } from '@docs/shared';

async function createDocumentationSpace(name: string): Promise<Space> {
  const response = await fetch('/api/spaces', {
    method: 'POST',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify({ name }),
  });

  return response.json();
}
```

### Use Language Tags

Every code block should specify its language:

````markdown
```typescript
// TypeScript code
```

```bash
# Shell commands
```

```json
// Configuration
```
````

## Tables for Comparisons

| Feature        | Free      | Pro       | Enterprise |
| -------------- | --------- | --------- | ---------- |
| Docs Spaces    | 1         | Unlimited | Unlimited  |
| Team Members   | 3         | 10        | Unlimited  |
| Sync Frequency | Daily     | Hourly    | Real-time  |
| Support        | Community | Email     | Dedicated  |

## Links and References

### Internal Links

Link to other pages in your docs:

```markdown
[Getting Started](../getting-started/overview.md)
[API Reference](../api-reference/authentication.md)
```

### External Links

Use descriptive anchor text:

```markdown
✅ Read more in the [GitHub API docs](https://docs.github.com/en/rest)

❌ Click [here](https://docs.github.com/en/rest) for more info
```

## Tips, Notes, and Warnings

Use emphasis to highlight important information:

> **Note:** This feature requires admin access to your space.

> **Tip:** You can speed up sync by using a specific branch instead of scanning all branches.

> **Warning:** Deleting a space is permanent and cannot be undone.

## Revision and Review

Before publishing:

1. **Read it aloud** - Catch awkward phrasing
2. **Check links** - Verify all cross-references work
3. **Test code samples** - Actually run them
4. **Peer review** - Have someone from your audience read it
5. **Update metadata** - Set correct `order` value

---

Happy writing! Clear docs make for happy users.
