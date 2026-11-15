# Release Process & Versioning Policy

This document details the release management, automated versioning, changelog generation, tagging, hotfix protocols, and rollback strategies across all repositories under `@OxDurgeshxO`.

---

## 1. Versioning Standard (Semantic Versioning 2.0.0)

All packages, services, libraries, and container images adhere to [Semantic Versioning (SemVer)](https://semver.org/):
- **MAJOR (`X.0.0`)**: Incompatible API changes, breaking database migrations, protocol changes.
- **MINOR (`0.X.0`)**: Backwards-compatible new features, added commands, additive schema migrations.
- **PATCH (`0.0.X`)**: Backwards-compatible bug fixes, security patches, performance optimizations.

---

## 2. Automated Release Workflow with Changesets

We use [Changesets](https://github.com/changesets/changesets) for monorepos and npm libraries to automate version bumps and changelog compilation.

### The Changeset Lifecycle
1. **Authoring Changeset**:
   When opening a PR with user-facing impact, contributor runs:
   ```bash
   pnpm changeset
   ```
   Select packages to bump (patch, minor, major) and write a markdown summary. Commit the generated `.changeset/*.md` file to the branch.
2. **Review & Merge**:
   Changeset is reviewed alongside the code. When merged to `main`, the `reusable-release.yml` workflow triggers.
3. **Release Pull Request (Version PR)**:
   The workflow runs `changeset version`, bumping versions in `package.json` files and generating `CHANGELOG.md` updates into an automated `Version Packages` PR.
4. **Publishing**:
   When the Version PR is merged to `main`, the release workflow runs `changeset publish`, creating Git tags (`vX.Y.Z`), GitHub Releases, and publishing to GitHub Packages / npm / GHCR.

---

## 3. Container & Artifact Publishing

- **Docker Images**: Published to GitHub Container Registry (`ghcr.io/oxdurgeshxo/<image>`).
- **Tagging Strategy**:
  - `ghcr.io/oxdurgeshxo/<image>:latest` (Points to latest release on `main`)
  - `ghcr.io/oxdurgeshxo/<image>:vX.Y.Z` (Immutable semantic release tag)
  - `ghcr.io/oxdurgeshxo/<image>:sha-<short-sha>` (Ephemeral per-commit build tag)
- **Provenance & Attestation**: Release builds include GitHub Action SBOM (Software Bill of Materials) and SLSA provenance attestations.

---

## 4. Hotfix Procedure

When a critical vulnerability or high-severity production bug occurs:
1. Branch directly from the tagged release on `main`:
   ```bash
   git checkout -b hotfix/vX.Y.Z+1 vX.Y.Z
   ```
2. Apply minimal targeted fix and write regression tests proving the fix.
3. Open a PR with title `[HOTFIX]: <description>` targeting `main`.
4. Run full security and CI test suites.
5. Obtain emergency approval from CODEOWNERS.
6. Merge, tag immediately, and deploy patched container or library.
7. Post-mortem review filed using `POSTMORTEM_TEMPLATE.md` within 48 hours.

---

## 5. Rollback Strategy

1. **Application Containers**:
   Deployments should be declarative and blue-green or rolling. Rollback consists of pointing Kubernetes deployment or runner to the previous immutable release tag (`:vX.Y.(Z-1)`).
2. **Database Migrations**:
   - Every forward migration must have an idempotent backward migration or be backwards-compatible (expand-contract pattern).
   - Never perform destructive schema changes (dropping columns/tables) in the same release as application code changes.
3. **Package Unpublishing Policy**:
   Never unpublish public packages unless legally required. Instead, immediately publish a patched bump (`vX.Y.Z+1`) deprecating the broken version.
