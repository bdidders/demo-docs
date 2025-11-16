---
title: Sync Troubleshooting
description: Solve common synchronization issues
order: 1
---

# Troubleshooting Sync Issues

Having problems syncing your documentation? Here are solutions to common issues.

## Sync Won't Start

### Symptoms

- Button is disabled
- Sync status shows "Pending"
- No recent sync timestamp

### Solutions

**Check Repository Access**

1. Verify the GitHub repository URL is correct
2. Confirm your token has access to the repository
3. If private repo, ensure GitHub token has `repo` scope

**Check API Rate Limits**

GitHub has rate limits:

- 60 requests/hour (unauthenticated)
- 5,000 requests/hour (authenticated)

If you're hitting limits, wait an hour and try again.

**Check Server Logs**

```bash
# View server logs
docker logs docify-server

# Or if running locally
tail -f ./server/logs/error.log
```

## Files Not Syncing

### Symptoms

- Some files appear but not all
- Specific folder is empty
- Count mismatch in UI

### Check Documentation Path

Verify your docs path setting:

```bash
# If docs path is "docs/", verify structure:
repo/
├── docs/           ✅ Should be here
│   ├── guide.md
│   └── api/
├── src/
└── README.md

# Common mistakes:
repo/
├── documentation/  ❌ But you set path to "docs/"
├── doc/            ❌ Missing 's'
```

### Check File Filters

Docify only processes:

- `.md` files (Markdown)
- `.mdx` files (optional MDX)

Files like `.txt`, `.pdf`, `.doc` are skipped.

### Check Frontmatter

If a file has invalid frontmatter, it might be skipped:

```yaml
# ✅ Valid
---
title: My Document
description: A test
order: 1
---
# ❌ Invalid - missing closing dashes
---
title: My Document
description: A test

# ❌ Invalid YAML syntax
---
title: My Document
description: A test
order: 'not-a-number'
---
```

## Sync Taking Too Long

### Symptoms

- Sync running for > 5 minutes
- Browser times out
- No visible progress

### Likely Causes

**Large Repository**

If your repo has many documents:

- Disable sync for other branches
- Move unrelated files outside docs folder
- Create `.docifyignore` file:

```
# .docifyignore
/docs/drafts/
/docs/archive/
*.tmp.md
```

**Slow Network**

If sync is over slow internet:

- Use a faster connection
- Try syncing during off-peak hours
- Check your GitHub API rate limit status

**Overloaded Server**

Multiple syncs happening simultaneously:

- Wait for other syncs to complete
- Set sync schedule to "manual" if automatic

## Incorrect Sidebar Navigation

### Symptoms

- Files not showing in sidebar
- Wrong folder structure
- Orphaned documents

### Solution: Rebuild Index

1. Go to Space Settings
2. Click **Rebuild Index**
3. Wait for rebuild to complete

### Check Naming

Ensure files are named correctly:

```
✅ Good names:
- getting-started.md
- api-reference.md
- 01-introduction.md

❌ Bad names (may be hidden):
- _draft.md (leading underscore)
- .hidden.md (hidden files)
- "spaces and special chars".md
```

## Links Broken After Sync

### Symptoms

- Internal links lead to 404
- Cross-references don't work
- Navigation is broken

### Fix Link Syntax

Use correct relative paths:

```markdown
# ✅ Correct - paths from docs folder

[Link](./subfolder/page.md)
[Link](../other-section/page.md)
[Link](/getting-started/overview.md)

# ❌ Wrong - absolute paths

[Link](/full/absolute/path/page.md)
[Link](C:\Windows\path\file.md)

# ❌ Wrong - .html extensions in source

[Link](./page.html) ← Don't add .html in markdown
```

## Search Not Finding Documents

### Symptoms

- Sync completed but search empty
- Older documents found but not new ones
- Search index missing

### Solution: Force Reindex

```bash
# Via admin API
curl -X POST https://api.docify.com/admin/reindex \\
  -H "Authorization: Bearer ADMIN_TOKEN"
```

## Common Error Messages

### "Repository not found"

- Check GitHub URL is correct: `https://github.com/owner/repo`
- Verify repository is public or token has access
- Ensure repository still exists

### "Invalid branch name"

- Verify branch name exists: `git branch -a`
- Check for typos in branch name
- Confirm default branch hasn't changed

### "No files found in docs path"

- Verify docs folder exists at the specified path
- Check for case sensitivity (Linux/Mac are case-sensitive)
- Ensure at least one `.md` file in the folder

### "Parse error in markdown"

- Check YAML frontmatter syntax
- Validate YAML using [yamllint.com](https://www.yamllint.com/)
- Ensure special characters are escaped

## Getting More Help

### Collect Debug Information

When reporting issues:

1. **Sync Log**
   - Go to Space Settings
   - Copy the sync log output

2. **File List**
   - Export list of documents in the space

3. **Configuration**
   - Screenshot or note:
     - Repository URL
     - Branch name
     - Docs path

4. **Error Details**
   - Full error message from UI
   - Browser console errors (F12)
   - Server logs if available

### Contact Support

[Contact us](mailto:support@docify.com) with:

- Your workspace URL
- Space slug
- Sync log output
- Steps to reproduce

---

**Still stuck?** Try the [Common Issues FAQ](./faq.md)
