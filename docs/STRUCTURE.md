# Mock Documentation Structure

Complete folder and file organization for testing Docify.

```
docs/
├── demo-docs.md                          # Original demo file
├── mock-doc.md                           # Welcome & overview
│
├── getting-started/                      # Onboarding section
│   ├── overview.md                       # Getting started overview
│   ├── installation.md                   # Setup & installation guide
│   └── configure-space.md                # Create first space
│
├── guides/                               # How-to guides
│   ├── writing-documentation.md          # Writing best practices
│   ├── repository-config.md              # GitHub repo setup
│   └── permissions.md                    # Access control
│
├── api-reference/                        # API documentation
│   ├── overview.md                       # API intro
│   ├── graphql-queries.md                # GraphQL query examples
│   └── authentication.md                 # API authentication
│
├── advanced/                             # Advanced topics
│   ├── architecture.md                   # System architecture
│   └── best-practices/                   # Best practices subsection
│       └── api-docs.md                   # API documentation standards
│
├── troubleshooting/                      # Problem-solving
│   ├── sync-issues.md                    # Sync troubleshooting
│   └── faq.md                            # Frequently asked questions
│
├── examples/                             # Real-world examples
│   ├── overview.md                       # Examples intro
│   ├── first-api-request.md              # First API call
│   ├── query-spaces.md                   # Query spaces
│   ├── search-documents.md               # Search implementation
│   └── integrations/                     # Integration examples
│       └── github-actions.md             # GitHub Actions setup
│
└── folder/                               # Nested folder test
    └── mock-doc.md                       # Nested file test
```

## File Statistics

- **Total Files:** 21 markdown files
- **Main Sections:** 7 (getting-started, guides, api-reference, advanced, troubleshooting, examples, folder)
- **Subsections:** 2 (best-practices, integrations)
- **Nested Depth:** Up to 3 levels

## Content Coverage

### Getting Started (3 files)
- Overview & introduction
- Installation & setup
- Creating first space

### Guides (3 files)
- Writing documentation
- Repository configuration
- Permission management

### API Reference (3 files)
- API overview
- GraphQL queries
- Authentication

### Advanced (2 files)
- System architecture
- API documentation best practices

### Troubleshooting (2 files)
- Sync issues guide
- FAQ

### Examples (5 files)
- Overview
- First API request
- Query spaces
- Search documents
- GitHub Actions integration

### Other
- Root welcome file
- Nested folder test

## Features Demonstrated

✅ Multiple folder levels
✅ Nested folder structure (examples/integrations/)
✅ Frontmatter with title, description, order
✅ Cross-file linking
✅ Code examples (multiple languages)
✅ Tables and formatting
✅ Real-world scenarios
✅ GraphQL queries and mutations
✅ REST API documentation
✅ Component/hook examples
✅ Best practices guides
✅ Q&A format
✅ Step-by-step tutorials

## Testing Opportunities

This structure allows testing of:

1. **Navigation** - Multiple levels of folder nesting
2. **Sidebar Generation** - Folder hierarchy display
3. **Table of Contents** - Multi-level heading detection
4. **Search** - Full-text search across all documents
5. **Code Highlighting** - Multiple language syntax highlighting
6. **Cross-linking** - Internal document references
7. **Frontmatter** - Metadata parsing and ordering
8. **Large Sets** - 21 files to test performance

---

Generated: November 2025
