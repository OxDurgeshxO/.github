# Production Release Checklist

Use this checklist prior to cutting and deploying any major or minor release.

---

## 1. Pre-Flight Verification (Step 0)
- [ ] Working branch is fully synced with `main`.
- [ ] Git status is clean with no untracked local files.
- [ ] All local tests pass cleanly:
  ```bash
  pnpm install --frozen-lockfile
  pnpm typecheck
  pnpm lint
  pnpm test
  pnpm build
  ```
- [ ] No hardcoded secrets, test credentials, or private URLs in git history.
- [ ] `.env.example` is fully up to date with any newly introduced configuration variables.

---

## 2. CI/CD & Automated Gates
- [ ] GitHub Actions CI workflow passed on all matrix jobs (100% pass rate).
- [ ] Security audit passes with zero critical or high vulnerabilities (`pnpm audit --audit-level=high`).
- [ ] CodeQL SAST workflow passed with zero alerts.
- [ ] Test coverage meets the organization threshold (>=70% overall, >=85% core logic).
- [ ] Benchmark regression analysis shows <5% deviation from previous release baseline.

---

## 3. Documentation & Governance
- [ ] Changeset added or `CHANGELOG.md` updated with human-readable release notes.
- [ ] SemVer bump correctly categorized (MAJOR, MINOR, or PATCH).
- [ ] `README.md` and `docs/OVERVIEW.md` accurate and up to date.
- [ ] CODEOWNERS approval obtained for modified core subsystems.

---

## 4. Container & Artifact Publishing
- [ ] Multi-stage Docker image builds successfully and passes vulnerability scan.
- [ ] Image tagged with immutable semantic version tag (`:vX.Y.Z`) and short SHA (`:sha-xxxx`).
- [ ] Release artifacts uploaded to GitHub Release and package registry.

---

## 5. Post-Release & Verification
- [ ] Deployment health check endpoints return HTTP 200 OK (`/healthz`, `/metrics`).
- [ ] Smoke tests executed against live deployment.
- [ ] OpenTelemetry / Sentry error tracking dashboard monitored for 15 minutes post-deploy.

---

## 6. Rollback Readiness
- [ ] Previous known good container image tag identified: [`:vX.Y.Z-1`].
- [ ] Backward migration tested if schema changes were introduced.
- [ ] Incident response channel designated.
