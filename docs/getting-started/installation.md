---
title: Installation & Setup
description: Set up Docify on your machine
order: 2
---

# Installation & Setup

This guide covers the installation and initial configuration of Docify.

## System Requirements

- **Node.js** 20.0 or higher
- **pnpm** 8.0 or higher (or npm/yarn)
- **MongoDB** 5.0 or higher (local or cloud)
- **Git** 2.30 or higher

## Installation Steps

### Step 1: Clone the Repository

```bash
git clone https://github.com/your-org/docify.git
cd docify
```

### Step 2: Install Dependencies

Using pnpm (recommended):

```bash
pnpm install
```

Or using npm:

```bash
npm install
```

### Step 3: Configure Environment Variables

Create a `.env` file in the `server/` directory:

```env
# MongoDB
MONGODB_URI=mongodb://localhost:27017/docify

# JWT
JWT_SECRET=your-secret-key-minimum-32-characters-long
JWT_EXPIRES_IN=7d

# Server
PORT=4000
NODE_ENV=development

# Client
VITE_GRAPHQL_URL=http://localhost:4000/graphql
```

### Step 4: Start Development Servers

**Build the shared package first:**

```bash
pnpm --filter @docs/shared build
```

**Start both server and client:**

```bash
pnpm dev
```

Or run them separately:

```bash
# Terminal 1: Server
pnpm dev:server

# Terminal 2: Client
pnpm dev:client
```

### Step 5: Verify Installation

1. Open your browser to `http://localhost:5173`
2. You should see the Docify login page
3. Create your first account or log in

## Troubleshooting

### Port Already in Use

If port 4000 or 5173 is already in use, you can change them:

```bash
# Server
PORT=5000 pnpm dev:server

# Client (in vite.config.ts)
# Modify server.port in the Vite config
```

### MongoDB Connection Issues

Ensure MongoDB is running:

```bash
# macOS with Homebrew
brew services start mongodb-community

# Docker
docker run -d -p 27017:27017 mongo
```

### Build Errors

Clear your dependencies and reinstall:

```bash
rm -rf node_modules pnpm-lock.yaml
pnpm install
pnpm --filter @docs/shared build
```

## Next Steps

- [Configure Your First Space](./configure-space.md)
- [Connect a GitHub Repository](../guides/repository-config.md)
- [Understanding the Architecture](../advanced/architecture.md)
