# Shared Workflows

Reusable GitHub Actions workflows for Capibara-Corp projects.

## Available Workflows

### `ci-nextjs.yml` - Next.js CI Pipeline

A complete CI workflow for Next.js projects with lint, type-check, tests, and build.

## Usage

Create a workflow file in your repo (e.g., `.github/workflows/ci.yml`):

```yaml
name: CI

on:
  pull_request:
    branches: [main, develop]
  push:
    branches: [main, develop]

jobs:
  ci:
    uses: Capibara-Corp/shared-workflows/.github/workflows/ci-nextjs.yml@v1
```

### With Custom Options

```yaml
name: CI

on:
  pull_request:
    branches: [main, develop]
  push:
    branches: [main, develop]

jobs:
  ci:
    uses: Capibara-Corp/shared-workflows/.github/workflows/ci-nextjs.yml@v1
    with:
      node-version: '22'
      run-e2e: true
      e2e-grep: '@smoke'
      run-unit-tests: false
```

### For Monorepos

```yaml
jobs:
  ci:
    uses: Capibara-Corp/shared-workflows/.github/workflows/ci-nextjs.yml@v1
    with:
      working-directory: 'apps/web'
```

## Inputs

| Input | Description | Default |
|-------|-------------|---------|
| `node-version` | Node.js version | `20` |
| `run-lint` | Run ESLint | `true` |
| `run-type-check` | Run TypeScript type check | `true` |
| `run-unit-tests` | Run Jest unit tests | `true` |
| `run-e2e` | Run Playwright E2E tests | `false` |
| `e2e-grep` | Playwright grep filter | `''` |
| `run-build` | Run Next.js build | `true` |
| `working-directory` | Working directory for monorepos | `.` |

## Jobs

The workflow runs these jobs (when enabled):

1. **Lint** - ESLint checks
2. **Type Check** - TypeScript `tsc --noEmit`
3. **Unit Tests** - Jest (skips if no test script exists)
4. **E2E Tests** - Playwright (optional, includes browser caching)
5. **Build** - Next.js production build with `.next/cache` caching

## Versioning

- `@v1` - Floating tag (recommended) - always points to latest v1.x.x
- `@v1.0.0` - Specific version (for pinning)

## Setup for Organization Access

> ⚠️ **Required:** For this workflow to be accessible from other repos in the organization, an admin must enable it:
>
> 1. Go to **Settings → Actions → General** in this repo
> 2. Under "Access", select **"Accessible from repositories in the 'Capibara-Corp' organization"**
> 3. Save

## License

Internal use only - Capibara-Corp
