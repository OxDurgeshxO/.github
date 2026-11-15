# Contributor Onboarding Guide: [Repository Name]

Welcome to the project! This guide walks you through setting up your local development environment, running tests, and submitting your first pull request.

---

## 1. System Requirements & Prerequisites
- **Operating System**: macOS, Linux (Ubuntu 22.04+), or Windows 11 with WSL2 / PowerShell.
- **Node.js**: v22 LTS or newer (`node -v`).
- **Package Manager**: `pnpm` v9+ (`corepack enable` or `npm install -g pnpm`).
- **Python** (if applicable): Python 3.12+ (`python --version`).
- **Docker**: Docker Engine & Docker Compose v2+.
- **Git**: Git 2.40+ configured with your name and email.

---

## 2. Quickstart Clone & Setup

```bash
# 1. Clone repository
git clone https://github.com/OxDurgeshxO/<REPO_NAME>.git
cd <REPO_NAME>

# 2. Configure environment variables
cp .env.example .env

# 3. Install dependencies
pnpm install

# 4. Verify system build & typecheck
pnpm typecheck
pnpm build

# 5. Run test suite
pnpm test
```

---

## 3. Starting Local Development Services

```bash
# Start background database and cache dependencies via Docker Compose
docker compose up -d postgres redis

# Run database migrations
pnpm run db:migrate

# Seed development data
pnpm run db:seed

# Start hot-reloading dev server
pnpm run dev
```

---

## 4. Development Standards & Pre-Commit Checks

Before opening a pull request, always run:
```bash
pnpm typecheck    # Must pass with 0 errors
pnpm lint         # Must pass with 0 warnings
pnpm test         # All unit and integration tests must pass
```

---

## 5. Submitting Your First Contribution
1. Create a feature branch: `git checkout -b feat/my-new-feature`
2. Follow Conventional Commits: `feat(scope): add new feature`
3. If public API or package behavior changed, run `pnpm changeset`
4. Push branch and open a PR using the provided `PULL_REQUEST_TEMPLATE.md`
5. Ensure all automated CI checks turn green!
