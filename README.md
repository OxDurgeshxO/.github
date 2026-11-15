# .github — Organization Engineering Operating System

[![CI](https://github.com/OxDurgeshxO/.github/actions/workflows/demo-heartbeat.yml/badge.svg)](https://github.com/OxDurgeshxO/.github/actions/workflows/demo-heartbeat.yml)
[![Security](https://img.shields.io/badge/Security-CodeQL%20%7C%20Secret%20Scan-brightgreen.svg)](./SECURITY.md)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](./LICENSE)
[![Health Score](https://img.shields.io/badge/Health_Score-Grade_A-brightgreen.svg)](./REPOSITORY_HEALTH.md)

This repository serves as the central engineering operating system, community health hub, and reusable automation registry for all public and private repositories under [@OxDurgeshxO](https://github.com/OxDurgeshxO).

---

## 🏛️ Governance, Policies & Standards

- **[ENGINEERING_STANDARDS.md](./ENGINEERING_STANDARDS.md)**: Organization-wide development, strict typing, schema validation, testing, and branching rules.
- **[AI_USAGE_POLICY.md](./AI_USAGE_POLICY.md)**: Guidelines for AI models, prompt versioning, structured outputs, medical/fitness safety boundaries, and red-teaming.
- **[RELEASE_PROCESS.md](./RELEASE_PROCESS.md)**: Semantic Versioning, Changesets workflow, container tagging, and hotfix/rollback protocols.
- **[GOVERNANCE.md](./GOVERNANCE.md)**: Technical leadership, RFC/ADR decision framework, and conflict escalation paths.
- **[SUPPORT.md](./SUPPORT.md)**: Support channels, bug filing instructions, and contact SLAs.
- **[CODEOWNERS](./CODEOWNERS)**: Default code ownership and automated PR reviewer assignments.
- **[REPOSITORY_HEALTH.md](./REPOSITORY_HEALTH.md)**: Objective health metrics (test coverage >=70%, 100% CI pass rate, 0 vulnerabilities).
- **[SECURITY.md](./SECURITY.md)**: Vulnerability disclosure and severity thresholds.
- **[CONTRIBUTING.md](./CONTRIBUTING.md)**: Contributor lifecycle and PR requirements.
- **[CODE_OF_CONDUCT.md](./CODE_OF_CONDUCT.md)**: Contributor Covenant Code of Conduct.

---

## 🔄 Reusable Workflows (`.github/workflows/`)

Repositories across the organization invoke these centralized workflows via GitHub Actions `workflow_call`:

| Reusable Workflow | Purpose & Capabilities |
|---|---|
| **[`reusable-ci.yml`](./.github/workflows/reusable-ci.yml)** | Matrix Node/TypeScript installs, frozen lockfile, linting, typechecking, tests, and build. |
| **[`reusable-security.yml`](./.github/workflows/reusable-security.yml)** | Dependency audit, CodeQL static analysis, and Gitleaks secret scanning. |
| **[`reusable-release.yml`](./.github/workflows/reusable-release.yml)** | Changesets versioning, automated Version PRs, GitHub Releases, and npm publishing. |
| **[`reusable-docker.yml`](./.github/workflows/reusable-docker.yml)** | Multi-platform Docker builds, Trivy vulnerability scanning, and GHCR registry publishing. |
| **[`reusable-docs.yml`](./.github/workflows/reusable-docs.yml)** | Markdownlint and Lychee broken hyperlink validation. |
| **[`reusable-performance.yml`](./.github/workflows/reusable-performance.yml)** | Continuous benchmark execution, regression comparisons, and artifact preservation. |
| **[`reusable-ai-eval.yml`](./.github/workflows/reusable-ai-eval.yml)** | Automated prompt regression testing and AI safety guardrail verification. |
| **[`reusable-node.yml`](./.github/workflows/reusable-node.yml)** | Multi-version Node.js matrix validation. |
| **[`reusable-python.yml`](./.github/workflows/reusable-python.yml)** | Ruff linting/formatting, Mypy strict typechecking, and Pytest coverage suites. |

---

## 📋 Reusable Documentation Templates (`templates/`)

Consistent documentation formats across repositories:
- **[ADR_TEMPLATE.md](./templates/ADR_TEMPLATE.md)**: Architecture Decision Records.
- **[RFC_TEMPLATE.md](./templates/RFC_TEMPLATE.md)**: Technical design proposals.
- **[POSTMORTEM_TEMPLATE.md](./templates/POSTMORTEM_TEMPLATE.md)**: Incident root-cause analysis (5 Whys).
- **[TEST_PLAN_TEMPLATE.md](./templates/TEST_PLAN_TEMPLATE.md)**: Verification scope and acceptance criteria.
- **[SECURITY_REVIEW_TEMPLATE.md](./templates/SECURITY_REVIEW_TEMPLATE.md)**: Threat modeling and OWASP ASVS verification.
- **[AI_FEATURE_REVIEW_TEMPLATE.md](./templates/AI_FEATURE_REVIEW_TEMPLATE.md)**: Prompt and model safety audit.
- **[RELEASE_CHECKLIST.md](./templates/RELEASE_CHECKLIST.md)**: Pre-flight release verification gates.
- **[ONBOARDING_TEMPLATE.md](./templates/ONBOARDING_TEMPLATE.md)**: Contributor onboarding and local environment setup.

---

## 🏷️ Issue & PR Automation

- **Structured YAML Forms**:
  - [Bug Report (`bug_report.yml`)](./.github/ISSUE_TEMPLATE/bug_report.yml)
  - [Feature Request (`feature_request.yml`)](./.github/ISSUE_TEMPLATE/feature_request.yml)
  - [Engineering Task (`task.yml`)](./.github/ISSUE_TEMPLATE/task.yml)
  - [Documentation (`documentation.yml`)](./.github/ISSUE_TEMPLATE/documentation.yml)
- **Pull Request Template**: Comprehensive verification and security checklist ([`pull_request_template.md`](./.github/pull_request_template.md)).
- **Dependabot**: Automated weekly updates for GitHub Actions, npm, and pip ([`dependabot.yml`](./.github/dependabot.yml)).
- **Label Taxonomy**: Unified color-coded issue labels ([`labels.yml`](./labels.yml)).

---

## 📄 License
This repository is licensed under the [MIT License](./LICENSE).
