---
title: Common Questions & Answers
description: Quick answers to frequently asked questions
order: 2
---

# Common Questions & Answers

## General Questions

### Q: What's the difference between a Space and a Document?

**A:**

- **Space** = A collection of documentation synced from one GitHub repository
- **Document** = An individual markdown file within a space

Think of it like:

- Space = Book
- Document = Chapter

### Q: Can I use Docify for public documentation?

**A:**
Yes! You can:

1. Create a public space (visible without login)
2. Generate shareable links with expiration dates
3. Set default permissions for new members

### Q: How often does Docify sync with GitHub?

**A:**
Depends on your space configuration:

- Real-time: Instant (via webhook)
- Hourly: Check every hour
- Daily: Check once per day
- Manual: Only when you trigger

## Technical Questions

### Q: Does Docify modify my GitHub repository?

**A:**
No, Docify is **read-only**. It:

- Clones your repository
- Reads documentation files
- **Never** pushes changes to your repo

All changes must be made in GitHub.

### Q: What markdown syntax does Docify support?

**A:**
Standard Markdown plus:

- GitHub Flavored Markdown (GFM)
- Tables
- Strikethrough
- Task lists
- Code syntax highlighting

Optional:

- MDX (if enabled)
- Custom components

### Q: Can I use images in my documentation?

**A:**
Yes! Use relative paths:

```markdown
![Alt text](./images/screenshot.png)
![Alt text](../images/diagram.png)
```

Store images in your `docs/images/` folder in GitHub.

### Q: What's the maximum file size for documents?

**A:**

- Individual file: 10 MB
- Per sync: 100 MB total
- Repository: No hard limit

For very large repos, use `.docifyignore` to exclude archives.

## Permissions & Access

### Q: Can I make documentation private?

**A:**
Yes, spaces are private by default. Only invited members can access them. To:

- **Keep private:** Don't enable public access
- **Share with specific people:** Invite them as Viewers
- **Make public:** Enable public access in space settings

### Q: What happens when someone leaves the team?

**A:**
Their access is revoked immediately. They:

- Can no longer view the documentation
- All their draft documents are preserved
- Their comments remain visible

Admins can reassign documents to other editors.

### Q: Can I set read-only access?

**A:**
Yes. Set user role to **Viewer**:

- Can read all documents
- Cannot edit or create
- Cannot access settings

## Troubleshooting

### Q: My documentation disappeared after sync

**A:**
This usually means:

1. Docs path is incorrect (check space settings)
2. GitHub branch was changed
3. Markdown files were deleted in GitHub
4. Files don't match `.md` extension

**Solution:** Check the [Sync Troubleshooting Guide](./sync-issues.md)

### Q: Search isn't finding my documents

**A:**
Search indexes documents during sync. If missing:

1. Try triggering a manual sync
2. Check if all files synced correctly
3. Force reindex in admin settings

### Q: Code blocks aren't highlighting

**A:**
Ensure code blocks have language tags:

```markdown
# ✅ Correct

\`\`\`javascript
console.log('Hello');
\`\`\`

# ❌ Wrong - no language

\`\`\`
console.log('Hello');
\`\`\`
```

## Performance & Scaling

### Q: How many documents can a space have?

**A:**
Docify handles spaces with:

- 100 documents - No issues
- 1,000+ documents - Works well
- 10,000+ documents - May need optimization

For very large spaces, consider:

- Splitting into multiple spaces
- Using `.docifyignore` to exclude files

### Q: How do I keep documentation up-to-date?

**A:**
Best practices:

1. Update docs **before** merging code changes
2. Use branches: `docs/feature-name`
3. Require PR reviews for documentation
4. Add reminders to keep docs current

### Q: Can multiple teams share one space?

**A:**
Not recommended. Instead:

1. Create separate spaces per team
2. One admin per space
3. Share read-only links if needed

## Getting Help

### Where can I find more documentation?

- [Getting Started](../getting-started/) - Start here
- [Guides](../guides/) - How-to articles
- [API Reference](../api-reference/) - For developers
- [Troubleshooting](./sync-issues.md) - Problem solving

### How do I report a bug?

Email [support@docify.com](mailto:support@docify.com) with:

- What you were doing
- What happened
- What you expected
- Screenshots/logs if possible

### Can I request a feature?

Yes! Submit feature requests via:

- [GitHub Issues](https://github.com/docify/docify/issues)
- [Feedback Form](https://docify.com/feedback)
- Email [product@docify.com](mailto:product@docify.com)

---

**Still have questions?** Contact support via [Help Center](https://support.docify.com)
