---
title: Create Your First Space
description: Set up your first documentation space
order: 3
---

# Create Your First Documentation Space

A Documentation Space is your collection of docs synced from a GitHub repository. Let's create one!

## What is a Space?

A Space represents:

- One GitHub repository
- A specific folder within that repository (usually `docs/`)
- A team's documentation
- Specific access permissions

## Creating a Space

### Method 1: Using the Admin Dashboard

1. Log in to Docify with an admin account
2. Navigate to the **Admin Dashboard**
3. Click **Create New Space**
4. Fill in the form:

| Field          | Description                                           |
| -------------- | ----------------------------------------------------- |
| **Space Name** | Display name (e.g., "API Documentation")              |
| **Repository** | GitHub repo URL (e.g., `https://github.com/org/repo`) |
| **Branch**     | Main branch to sync from (default: `main`)            |
| **Docs Path**  | Folder containing docs (default: `docs/`)             |

5. Click **Create**

### Method 2: Using GraphQL Mutation

```graphql
mutation CreateSpace {
  createSpace(
    input: {
      name: "API Documentation"
      repositoryUrl: "https://github.com/org/repo"
      branch: "main"
      docsPath: "docs/"
    }
  ) {
    id
    name
    slug
    createdAt
  }
}
```

## Space Configuration

### Basic Settings

- **Name** - Display name in the sidebar
- **Description** - Optional summary of the space's purpose
- **Icon** - Optional emoji or icon for visual identification

### Repository Settings

- **URL** - GitHub repository URL
- **Branch** - Which branch to sync from
- **Docs Path** - Subdirectory containing documentation
- **Sync Interval** - How often to check for updates

### Access Control

- **Viewers** - Can read all documents
- **Editors** - Can create and modify documents (in Docify UI)
- **Admins** - Full control over space settings

## After Creating Your Space

Your space will automatically:

1. Clone the repository
2. Scan the docs folder
3. Extract frontmatter and content
4. Build the navigation tree
5. Index documents for search

This typically takes 30-60 seconds depending on repository size.

## Verifying Your Space

1. Go to **Spaces** in the main navigation
2. Click your new space
3. Verify:
   - [ ] Sidebar shows correct folder structure
   - [ ] Documents rendered correctly
   - [ ] Code blocks highlighted properly
   - [ ] Table of contents generated
   - [ ] Search finds documents

## Next Steps

- [Write Documentation](../guides/writing-documentation.md)
- [Manage Permissions](../guides/permissions.md)
- [Configure GitHub Sync](../guides/repository-config.md)

---

**Need help?** Check the [Troubleshooting Guide](../troubleshooting/sync-issues.md)
