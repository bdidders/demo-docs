---
title: Repository Configuration
description: Configure your GitHub repository for Docify
order: 2
---

# Repository Configuration

Docify syncs documentation from your GitHub repository. This guide covers the configuration process.

## Prerequisites

- Admin access to your GitHub repository
- A Docify account with admin privileges
- GitHub Personal Access Token (optional, for private repos)

## Step 1: Connect GitHub

### In Docify Admin Panel

1. Navigate to **Settings** → **Integrations**
2. Click **Connect GitHub**
3. Authorize Docify to access your GitHub account
4. Select the repositories to allow access

## Step 2: Configure Repository Sync

### Basic Configuration

For each repository connected to Docify:

**Repository URL**

```
https://github.com/your-org/your-repo
```

**Branch**

```
main (or your default branch)
```

**Documentation Path**

```
docs/
```

Choose where your documentation files are located. Common patterns:

- `docs/` - Root documentation folder
- `./docs/` - Relative path
- `documentation/` - Alternative naming

## Step 3: Set Up Files

### Repository Structure

Recommended organization:

```
your-repo/
├── docs/
│   ├── README.md
│   ├── getting-started/
│   │   ├── overview.md
│   │   └── installation.md
│   ├── guides/
│   │   ├── setup.md
│   │   └── usage.md
│   ├── api/
│   │   ├── endpoints.md
│   │   └── authentication.md
│   └── reference/
│       └── changelog.md
├── src/
├── README.md
└── package.json
```

### Documentation Entry Point

The root `README.md` in your docs folder becomes the space's home page:

```markdown
---
title: Documentation Home
description: Main entry point for our documentation
---

# Our Documentation

Welcome! Choose a topic to get started:

- [Getting Started](./getting-started/overview.md)
- [API Reference](./api/endpoints.md)
- [Guides](./guides/setup.md)
```

## Step 4: Frontmatter (Optional but Recommended)

Add frontmatter to your Markdown files for better control:

```markdown
---
title: Page Title
description: Brief summary for search results
order: 10
tags: [setup, configuration]
---

# Page Title

Your content here...
```

**Frontmatter Fields:**

| Field         | Type     | Purpose              |
| ------------- | -------- | -------------------- |
| `title`       | string   | Override page title  |
| `description` | string   | Search summary       |
| `order`       | number   | Sort order in folder |
| `tags`        | string[] | Categorization       |
| `hidden`      | boolean  | Hide from navigation |

## Step 5: Sync Settings

### Automatic Sync Schedule

Choose how often Docify syncs your repository:

- **Real-time** - Sync on every push to the selected branch
- **Hourly** - Check every hour for changes
- **Daily** - Check once per day
- **Manual** - Sync only when triggered manually

### Branch Configuration

**Single Branch** (Recommended)

```
Sync from: main
```

**Multiple Branches**

```
Sync from: main, develop, staging
```

## Step 6: Test the Sync

### Trigger Manual Sync

1. In the Space settings, click **Sync Now**
2. Wait for the sync to complete (usually 30-60 seconds)
3. Check the **Sync Log** for any errors

### Verify Content

After syncing:

- [ ] All folders appear in the sidebar
- [ ] Documents display correctly
- [ ] Code blocks are highlighted
- [ ] Links work properly
- [ ] Search indexes files

## Troubleshooting

### Sync Not Starting

**Cause:** Repository not accessible
**Solution:** Verify URL and GitHub token permissions

### Files Not Appearing

**Cause:** Incorrect docs path
**Solution:** Double-check the documentation path setting

### Links Broken

**Cause:** Incorrect relative paths
**Solution:** Use paths relative to the docs folder

### Slow Sync

**Cause:** Large repository
**Solution:** Move to subdirectory or use `.docifyignore`

## Best Practices

### .docifyignore

Create a `.docifyignore` file in your docs folder to exclude files:

```
# .docifyignore
**/drafts/**
**/temp/**
*.tmp.md
```

### Branch Strategy

- **Main branch** - Use for stable, published docs
- **Development** - Use for previewing changes
- **Feature branches** - Test before merging to main

### Documentation Workflow

1. Create a feature branch: `docs/add-auth-guide`
2. Add/edit documentation files
3. Push and open a PR
4. Review with your team
5. Merge to main
6. Docify automatically syncs

## Next Steps

- [Create Your First Space](../getting-started/configure-space.md)
- [Writing Documentation](./writing-documentation.md)
- [Managing Permissions](./permissions.md)

---

**Questions?** Check [Troubleshooting](../troubleshooting/sync-issues.md)
