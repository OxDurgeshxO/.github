# Repository Health Scorecard

This scorecard defines objective quality, security, documentation, and operational benchmarks across all repositories in the organization.

---

## 1. Objective Target Metrics

| Area | Metric | Target Threshold | Audit Mechanism |
|---|---|---|---|
| **Activity** | Commits in last 30 days | At least 5 commits | Git history / GitHub Activity API |
| **Quality** | CI pass rate | 100% on `main` branch | GitHub Actions run telemetry |
| **Testing** | Automated Code Coverage | 70% minimum overall; 85% core logic | Vitest / Jest / Pytest + Codecov / LCOV |
| **Documentation** | README Completeness | Setup, architecture, usage, contribution, license | Automated markdown audit & docs review |
| **Security** | Critical/High Vulnerabilities | 0 findings | Dependabot, `pnpm audit`, Snyk |
| **Security** | Secret Scan Findings | 0 leaked secrets | GitHub Secret Scanning & TruffleHog |
| **Maintenance** | Open Stale Issues | Under 10 issues | Stale action bot & weekly triage |
| **Release** | Latest Tagged Release | Within 90 days | Git tags & GitHub Releases |
| **Observability** | Health Checks & Metrics | Present in all server/API projects | Prometheus `/metrics`, `/healthz`, OpenTelemetry |
| **Deployment** | Live Demo or Preview | Present for user-facing projects | Vercel / Railway / Docker preview URL |

---

## 2. Standard Repository Status Badges

Every public repository README must include the standard verified status badge header:

```markdown
[![CI](https://github.com/OxDurgeshxO/REPO/actions/workflows/ci.yml/badge.svg)](https://github.com/OxDurgeshxO/REPO/actions/workflows/ci.yml)
[![Security](https://github.com/OxDurgeshxO/REPO/actions/workflows/security.yml/badge.svg)](https://github.com/OxDurgeshxO/REPO/actions/workflows/security.yml)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](./LICENSE)
[![Health Score](https://img.shields.io/badge/Health_Score-Grade_A-brightgreen.svg)](./REPOSITORY_HEALTH.md)
```

---

## 3. Self-Assessment Checklist

Before promoting a repository to public production or requesting portfolio review, verify:

- [ ] Repository has a clean, up-to-date `.env.example`
- [ ] No hardcoded secrets, test credentials, or private URLs in git history
- [ ] Automated CI workflow passes on all supported Node/Python matrix versions
- [ ] Dependabot is enabled and active for packages and GitHub Actions
- [ ] `docs/OVERVIEW.md` exists with clear problem, architecture, metrics, and learnings
- [ ] CODEOWNERS file is present with valid reviewer assignments
- [ ] Standard issue templates and PR template are active
- [ ] Branch protection rules are active requiring linear history and green CI
