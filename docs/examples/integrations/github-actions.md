---
title: GitHub Actions Integration
description: Automate documentation sync with GitHub Actions
order: 1
---

# GitHub Actions Integration

Use GitHub Actions to automate your documentation workflow.

## Trigger Docify Sync

Automatically trigger a sync when docs are updated:

```yaml
name: Sync Documentation

on:
  push:
    branches: [main]
    paths:
      - 'docs/**'

jobs:
  sync-docs:
    runs-on: ubuntu-latest
    steps:
      - name: Trigger Docify Sync
        run: |
          curl -X POST https://api.docify.com/graphql \\
            -H "Authorization: Bearer ${{ secrets.DOCIFY_TOKEN }}" \\
            -H "Content-Type: application/json" \\
            -d '{
              "query": "mutation { syncSpace(id: \"space_abc123\") { id status } }"
            }'
```

## Validate Documentation

Check documentation before merge:

```yaml
name: Validate Docs

on:
  pull_request:
    paths:
      - 'docs/**'

jobs:
  validate:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3

      - name: Check Markdown
        run: |
          npm install -g markdownlint-cli
          markdownlint 'docs/**/*.md'

      - name: Validate Frontmatter
        run: |
          npm install yaml
          node .github/scripts/validate-frontmatter.js
```

## Automatic Changelog

Generate changelog from commits:

```yaml
name: Update Changelog

on:
  push:
    branches: [main]

jobs:
  changelog:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
        with:
          fetch-depth: 0

      - name: Generate Changelog
        uses: github-changelog-generator/github-changelog-generator@master
        with:
          token: ${{ secrets.GITHUB_TOKEN }}
          output: docs/changelog.md

      - name: Commit Changes
        run: |
          git config user.name "GitHub Actions"
          git config user.email "actions@github.com"
          git add docs/changelog.md
          git commit -m "Update changelog"
          git push
```

---

**Related:** [Custom Scripts](../custom-scripts.md)
