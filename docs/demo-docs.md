# demo-docs

Welcome to **demo-docs**, a sample documentation space designed to be used with **Docify** – an internal, GitBook-style documentation platform that syncs content directly from a GitHub repository.

This repo is intentionally structured and written to:

- Exercise Docify’s **Git sync** behavior
- Demonstrate a clean, opinionated **docs structure**
- Provide realistic, end-to-end **demo content** for development, testing, and onboarding

If you’re reading this inside Docify, this README is your **landing page** for the demo docs space.

---

## 1. What is this repo?

This repository is a **demo documentation space**. It is not the Docify application itself – it’s a **content repo**:

- **Owned by Docify admins**
- **Connected** to Docify during setup
- **Synced** into a Docify “Space” to render a beautiful documentation site

You can use it to:

- Validate that GitHub → Docify sync works
- Test navigation, TOC, search, and code blocks
- Showcase “good” doc patterns for your own teams

---

## 2. Repository structure

Docify typically points at a specific folder within a repo (e.g. `docs/`). In this demo, we’ll use the root folder and the `docs/` directory.

```text
demo-docs/
├─ README.md               # You are here (landing page)
├─ docs/
│  ├─ getting-started/
│  │  ├─ overview.md
│  │  ├─ installation.md
│  │  └─ first-doc-space.md
│  ├─ authoring/
│  │  ├─ writing-style.md
│  │  ├─ markdown-cheatsheet.md
│  │  └─ mdx-examples.md
│  ├─ platform/
│  │  ├─ architecture.md
│  │  ├─ spaces-and-docs.md
│  │  └─ permissions-and-roles.md
│  ├─ workflows/
│  │  ├─ create-new-space.md
│  │  ├─ update-existing-docs.md
│  │  └─ review-and-approval.md
│  └─ reference/
│     ├─ glossary.md
│     ├─ api-notes.md
│     └─ changelog-demo.md
└─ .gitbook.yml / .docify.yml (optional future config)
````

> **Tip:** In a Docify space, `docs/getting-started/overview.md` is a perfect candidate for the default “Home” page.

---

## 3. How Docify uses this repo

Docify’s backend does roughly the following:

1. **Clones** this repository (or pulls latest changes).
2. Scans a configured **docs path** (e.g. `docs/`).
3. For each `*.md` or `*.mdx` file:

   * Parses frontmatter (if any)
   * Extracts headings
   * Builds a **TOC tree** from folder paths
4. Stores:

   * A `Node` (navigation entry)
   * A `Content` record (the raw Markdown/MDX)
5. The frontend:

   * Displays a **sidebar** based on the folder/Node tree
   * Renders the content using **Chakra UI** + Markdown/MDX

Practically, that means:

* Directory structure ≈ **navigation structure**
* Filenames and headings ≈ **page titles**
* Frontmatter (optional) can tweak ordering, labels, or visibility

---

## 4. Basic authoring model

Every Markdown file in `docs/` should follow a simple pattern:

```markdown
---
title: Getting Started with Docify
description: A quick overview of how to use Docify with your first documentation repo.
order: 10
---

# Getting Started with Docify

Welcome to your first Docify-powered documentation space!
```

**Frontmatter fields (recommended):**

* `title` – Overrides the page title / sidebar label
* `description` – Short summary for search or cards
* `order` – Controls ordering within a folder (lower = earlier)
* `tags` – Optional array for search or filters

> Docify can still render docs without frontmatter; it will fall back to filenames and headings.

---

## 5. Getting started (for people using this demo space)

If you’re just exploring Docify, here’s a suggested path:

1. **Read this README** to understand the structure.

2. Open:

   * `docs/getting-started/overview.md`
   * `docs/getting-started/installation.md`
   * `docs/getting-started/first-doc-space.md`

3. Explore the **Authoring** section to see writing guidelines and Markdown/MDX examples.

4. Visit **Workflows** to understand typical day-to-day usage patterns for writers and reviewers.

5. Use **Reference** → `changelog-demo` and `glossary` to test TOC, headings, and long-form content.

---

## 6. Writing guidelines (short version)

We keep full guidelines in `docs/authoring/writing-style.md`, but here’s the quick version:

### 6.1 Voice and tone

* Friendly, clear, and **practical**
* No marketing fluff; docs should reduce cognitive load
* Prefer:

  * “You can configure the space…”
    over
  * “One might configure the space…”

### 6.2 Structure per page

A good doc page usually has:

1. **Frontmatter** (title, description, order, tags)
2. **H1** that matches the title
3. **Short intro paragraph** explaining why the page exists
4. **Task-oriented sections** (H2/H3):

   * “Before you begin”
   * “Step-by-step”
   * “Troubleshooting”
5. **Examples** (code blocks, screenshots, tips)
6. **Links** to related pages

### 6.3 Short, focused topics

Prefer multiple small pages over one giant one:

* ✅ `create-new-space.md`, `update-existing-docs.md`, `review-and-approval.md`
* ❌ `everything-about-docify-workflows.md` with 20 sections

---

## 7. Markdown & MDX patterns

This repo can include both **plain Markdown** and **MDX** (if Docify is configured for MDX).

### 7.1 Basic Markdown examples

#### Headings

```markdown
# H1 – Page title
## H2 – Major section
### H3 – Subsection
```

#### Lists

```markdown
- Bullet item
- Another item
  - Nested item

1. First step
2. Second step
3. Third step
```

#### Code blocks

```bash
# Shell example
pnpm dev
```

```ts
// TypeScript example
import { Space } from '@docs/shared';

const space: Space = {
  id: 'demo',
  name: 'Demo Docs',
  // ...
};
```

### 7.2 MDX-style patterns (if enabled)

You might have MDX pages such as:

````mdx
---
title: Callouts and Components
description: How Docify renders custom components in docs.
order: 40
---

# Callouts and Components

<Callout status="info" title="Heads up!">
  MDX pages support custom components. This page exists to test those components.
</Callout>

<CodeTabs>
  <CodeTab label="TypeScript">

```ts
export function hello(name: string) {
  return `Hello, ${name}!`;
}
````

  </CodeTab>
  <CodeTab label="JavaScript">

```js
export function hello(name) {
  return `Hello, ${name}!`;
}
```

  </CodeTab>
</CodeTabs>
```

Even if the **actual MDX components** differ in your real project, this repo gives you a place to experiment safely.

---

## 8. How to test Docify with this repo

If you’re developing or testing Docify locally, a typical workflow might look like:

1. **Clone this repo**

   ```bash
   git clone https://github.com/your-org/demo-docs.git
   cd demo-docs
   ```

2. **Connect it in Docify**

   In the Docify admin dashboard (when implemented):

   * Connect GitHub
   * Select `your-org/demo-docs`
   * Set:

     * `docsPath` → `docs`
     * `defaultBranch` → `main`
   * Create the space (e.g. **Demo Docs**)

3. **Trigger a sync**

   Use the Docify UI or a GraphQL mutation (`syncSpace`) to sync the space.

4. **Browse the docs**

   Navigate to:

   * `/spaces/demo-docs` (or whatever slug you chose)
   * Verify:

     * Sidebar structure matches the folder structure
     * TOC is built from headings
     * Changelog, glossary, and workflows look correct

---

## 9. Suggested documentation sections (within `docs/`)

Below is a suggested outline for the demo content. You don’t have to implement every file exactly like this, but using this pattern will make the demo feel “real”.

### 9.1 Getting Started (`docs/getting-started/`)

* `overview.md`
  High-level overview of Docify and this demo space.

* `installation.md`
  How to run Docify internally (or at least a mock flow).

* `first-doc-space.md`
  “Create your first doc space” walkthrough using `demo-docs`.

### 9.2 Authoring (`docs/authoring/`)

* `writing-style.md`
  Style guide: tone, tense, inclusive language, etc.

* `markdown-cheatsheet.md`
  Quick reference for headings, lists, tables, code blocks.

* `mdx-examples.md`
  Examples of any custom components (callouts, tabs, badges, etc.).

### 9.3 Platform (`docs/platform/`)

* `architecture.md`
  High-level view of Docify’s architecture (client, server, shared, Git sync).

* `spaces-and-docs.md`
  How spaces map to Git repos and folders; how nodes/content are created.

* `permissions-and-roles.md`
  Overview of roles (Viewer, Editor, Admin) and how they interact with docs.

### 9.4 Workflows (`docs/workflows/`)

* `create-new-space.md`
  Step-by-step instructions to create a new documentation space.

* `update-existing-docs.md`
  How to update and preview docs (local dev, commit, sync).

* `review-and-approval.md`
  Suggested review process: PRs, approvals, release notes.

### 9.5 Reference (`docs/reference/`)

* `glossary.md`
  Definitions of Docify-specific terms.

* `api-notes.md`
  Any API-related notes the platform might expose (for demo, fake endpoints are fine).

* `changelog-demo.md`
  A fictitious changelog to exercise chronological lists, anchors, and headings.

---

## 10. Example frontmatter & ordering

Docify can use `order` from frontmatter to sort pages. For example:

```markdown
---
title: Overview
description: Start here to understand how this documentation space is organized.
order: 1
---

# Overview

Welcome to the demo-docs space…
```

```markdown
---
title: Installation
description: How to run Docify with this demo-docs repository.
order: 2
---

# Installation

To get started, you’ll need…
```

If you omit `order`, Docify can fall back to alphabetical or filesystem ordering – but explicitly setting it gives you more control.

---

## 11. FAQ (for this demo repo)

**Q: Is this the real Docify codebase?**
**A:** No. This repository is **content only**. Docify itself lives in a separate application repo.

---

**Q: Can I safely break things here?**
**A:** Yes – that’s the point. This is a demo space intended for experimentation. Feel free to:

* Add new folders/pages
* Rename things
* Introduce MDX features
* Test long, complex pages

Just keep the overall structure somewhat coherent so it remains useful for testing.

---

**Q: Do I need frontmatter everywhere?**
**A:** No, but it helps. Docify will try to infer titles/headings without it, but frontmatter provides better control over ordering, labels, and metadata.

---

## 12. Contributing to this demo space

Even though this is “just” a demo, we still treat it like a real docs repo:

1. Create a feature branch:

   ```bash
   git checkout -b docs/update-getting-started
   ```

2. Edit or add Markdown/MDX files under `docs/`.

3. Run your normal tooling (linting/formatting) if configured.

4. Open a PR and have another teammate skim it for clarity.

5. Merge and trigger a Docify sync to see the results in the UI.

---

## 13. Next steps

If you’re using this as part of Docify development:

* ✅ **Already done:** clone & connect `demo-docs` as a space.
* 🔍 Next:

  * Navigate through all sections to verify TOC, headings, and search.
  * Experiment with MDX components, if supported.
  * Add edge-case content (very long pages, deep nested headings, lots of code blocks).

If you’re using this as a blueprint for your **own** docs repo:

* Copy the `docs/` structure
* Replace content with your real domain docs
* Keep the same **patterns**:

  * Small, focused pages
  * Clear frontmatter
  * Logical folder hierarchy

---

Happy documenting! ✨
*This repo exists to help you ship better internal docs with less friction.*
