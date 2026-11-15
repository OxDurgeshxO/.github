# Organization Engineering Standards

This document defines the baseline technical principles, development workflows, quality gates, and architectural conventions across all repositories under `@OxDurgeshxO`.

---

## 1. Core Engineering Principles

1. **Deterministic Quality & Zero Silent Failures**: All code must fail fast and loudly on invalid inputs. No swallow-and-ignore exception patterns.
2. **Strict Typing Everywhere**: TypeScript projects must enforce strict compiler settings (`noImplicitAny`, `strictNullChecks`, `noUncheckedIndexedAccess`). Python projects must pass `mypy --strict`.
3. **Runtime Schema Validation**: All external boundaries (HTTP requests, WebSocket messages, environment variables, database records) must be validated at runtime using Zod (TypeScript) or Pydantic (Python).
4. **Secret Zero-Tolerance**: No API keys, credentials, private certificates, or internal tokens may ever be committed. All configuration flows through `.env.example` templates and encrypted environment secrets.
5. **Least-Privilege Security**: GitHub Actions workflows run with explicit read-only `permissions` blocks by default, elevating only the specific scopes required for release or publishing.

---

## 2. Standard Tech Stack

| Layer | Primary Standard | Secondary / Alternative |
|---|---|---|
| **Package Manager** | `pnpm` (lockfile frozen in CI) | `npm` / `uv` / `poetry` |
| **Language Runtime** | Node.js 22+ LTS / Python 3.12+ | TypeScript 5.7+ / PyPy |
| **API Architecture** | RESTful OpenAPI 3.1 & Typed RPC | WebSockets / SSE for streaming |
| **Database & ORM** | PostgreSQL + Drizzle ORM | SQLite / DuckDB for local/analytical |
| **Validation** | Zod (TS) / Pydantic v2 (Py) | Standard Schema specifications |
| **Testing Harness** | Vitest / Node Test Runner / Pytest | Playwright (E2E) / fast-check (Fuzz) |
| **Linting & Formatting** | Biome / ESLint + Prettier / Ruff | Pre-commit hooks |
| **Observability** | OpenTelemetry + Structured JSON logging | Prometheus metrics & Sentry |
| **Containers** | Multi-stage Docker (distroless / alpine) | Docker Compose for local development |

---

## 3. Git Workflow & Branching Strategy

- **Default Branch**: `main`. Direct pushes to `main` are strictly prohibited.
- **Branch Naming Convention**:
  - `feat/<short-description>`: New functionality
  - `fix/<short-description>`: Bug remediation
  - `refactor/<short-description>`: Code restructuring without feature alteration
  - `perf/<short-description>`: Performance optimization
  - `docs/<short-description>`: Documentation changes only
  - `chore/<short-description>`: Tooling, dependency updates, maintenance
- **Commit Message Convention (Conventional Commits)**:
  - Format: `<type>(<scope>): <subject>`
  - Types: `feat`, `fix`, `docs`, `style`, `refactor`, `perf`, `test`, `build`, `ci`, `chore`, `revert`
  - Examples:
    - `feat(protocol): implement full RESP2 bulk string parser`
    - `fix(pose): handle null landmarks when body exits camera frame`
    - `ci(workflows): pin actions to commit SHAs and set minimal token permissions`
- **Pull Request Lifecycle**:
  - PR branches must be kept rebased or updated against current `main`.
  - Linear history is enforced on `main` via Squash & Merge or Rebase & Merge.
  - Branches are automatically deleted upon merge.

---

## 4. Testing & Code Coverage Thresholds

All production repositories must achieve the following verified test thresholds:
- **Overall Code Coverage**: Minimum **70%** line coverage.
- **Core Domain Logic**: Minimum **85%** branch and statement coverage (parsers, state machines, billing, auth).
- **Test Categories**:
  - **Unit Tests**: Isolated logic, mathematical calculations, pure functions.
  - **Integration Tests**: Database transactions, external service mocking, API endpoints.
  - **Property-based Fuzz Tests**: Input boundary validation using `fast-check` or `hypothesis`.
  - **Regression Benchmarks**: Continuous latency/throughput assertions on critical paths.
  - **End-to-End (E2E)**: Playwright smoke tests for browser and web workflows.

---

## 5. Security Gates & Vulnerability Management

Every repository must integrate automated checks on every pull request and push to `main`:
1. **Dependency Vulnerability Scans**: Zero critical or high vulnerabilities allowed (`pnpm audit --audit-level=high` or Dependabot security alerts).
2. **Static Application Security Testing (SAST)**: GitHub CodeQL analysis on push and weekly schedule.
3. **Secret Scanning**: Push protection enabled and TruffleHog / GitGuardian scanners.
4. **Third-Party Action Pinning**: GitHub Actions must be pinned to full 40-character commit SHAs (not floating `@v1` tags).
5. **OWASP ASVS Compliance**: Web applications and APIs follow OWASP Application Security Verification Standard Level 2 guidelines.

---

## 6. Documentation Standards

- Every repository must provide:
  - `README.md` with problem statement, quick start, architecture overview, status badges, and license.
  - `REPOSITORY_HEALTH.md` tracking objective operational and quality metrics.
  - `docs/OVERVIEW.md` summarizing the project, portfolio value, architecture, and learnings.
  - `docs/` folder containing relevant Architecture Decision Records (`ADR`), API contracts, and system designs.
- Documentation must pass markdown linting and contain no dead internal or external links.
