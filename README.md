# Shared Workflows

Reusable GitHub Actions workflows for Capibara-Corp projects.

## Available Workflows

### 🐦 Flutter CI (`ci-flutter.yml`)

Complete CI/CD workflow for Flutter applications including analysis, testing, and multi-platform builds.

#### Basic Usage

```yaml
name: CI

on:
  push:
    branches: [main, develop]
  pull_request:
    branches: [main, develop]

jobs:
  ci:
    uses: Capibara-Corp/shared-workflows/.github/workflows/ci-flutter.yml@main
```

#### Full Example with All Options

```yaml
name: CI

on:
  push:
    branches: [main]
  pull_request:
    branches: [main]

jobs:
  ci:
    uses: Capibara-Corp/shared-workflows/.github/workflows/ci-flutter.yml@main
    with:
      flutter-version: '3.24.0'      # Specific version or 'stable'
      flutter-channel: 'stable'       # stable, beta, dev, master
      working-directory: '.'          # For monorepos
      run-analyze: true               # Run flutter analyze
      run-test: true                  # Run flutter test
      run-build-web: true             # Build web release
      run-build-apk: true             # Build Android APK
      run-build-ios: false            # Build iOS (requires macOS)
      java-version: '17'              # Java version for Android
      test-coverage: true             # Generate coverage report
```

#### Inputs

| Input | Description | Default |
|-------|-------------|---------|
| `flutter-version` | Flutter version (e.g., `3.24.0`, `stable`) | `stable` |
| `flutter-channel` | Release channel (`stable`, `beta`, `dev`, `master`) | `stable` |
| `working-directory` | Working directory for commands | `.` |
| `run-analyze` | Run `flutter analyze` | `true` |
| `run-test` | Run `flutter test` | `true` |
| `run-build-web` | Build for web | `false` |
| `run-build-apk` | Build APK for Android | `false` |
| `run-build-ios` | Build for iOS (macOS runner) | `false` |
| `java-version` | Java version for Android builds | `17` |
| `test-coverage` | Generate coverage report | `false` |

#### Jobs

1. **Analyze** - Code analysis and formatting check
2. **Test** - Run unit and widget tests
3. **Build Web** - Create web release build (optional)
4. **Build APK** - Create Android release APK (optional)
5. **Build iOS** - Create iOS build without codesign (optional)

#### Features

- ✅ Flutter SDK caching for faster builds
- ✅ Pub dependencies caching
- ✅ Artifact uploads for builds
- ✅ Coverage report generation
- ✅ Monorepo support via `working-directory`
- ✅ Configurable Flutter version and channel

---

### 📦 Node.js CI (`ci-node.yml`)

Complete CI workflow for Node.js backend projects (Express, Fastify, NestJS, etc.). Supports npm, pnpm, and yarn.

#### Basic Usage

```yaml
name: CI

on:
  push:
    branches: [main, develop]
  pull_request:
    branches: [main, develop]

jobs:
  ci:
    uses: Capibara-Corp/shared-workflows/.github/workflows/ci-node.yml@main
```

#### Full Example with All Options

```yaml
name: CI

on:
  push:
    branches: [main]
  pull_request:
    branches: [main]

jobs:
  ci:
    uses: Capibara-Corp/shared-workflows/.github/workflows/ci-node.yml@main
    with:
      node-version: '20'              # Node.js version
      package-manager: 'pnpm'         # npm, pnpm, or yarn
      pnpm-version: '9'               # pnpm version (if using pnpm)
      working-directory: '.'          # For monorepos
      run-lint: true                  # Run ESLint
      run-tests: true                 # Run tests
      run-build: true                 # Run build script
      test-coverage: true             # Generate coverage report
      lint-script: 'lint'             # Custom lint script name
      test-script: 'test'             # Custom test script name
      build-script: 'build'           # Custom build script name
```

#### Inputs

| Input | Description | Default |
|-------|-------------|---------|
| `node-version` | Node.js version | `20` |
| `package-manager` | Package manager (`npm`, `pnpm`, `yarn`) | `npm` |
| `pnpm-version` | pnpm version (if using pnpm) | `9` |
| `working-directory` | Working directory for commands | `.` |
| `run-lint` | Run ESLint | `true` |
| `run-tests` | Run tests | `true` |
| `run-build` | Run build script | `true` |
| `test-coverage` | Generate coverage report | `false` |
| `lint-script` | Custom lint script name | `lint` |
| `test-script` | Custom test script name | `test` |
| `build-script` | Custom build script name | `build` |

#### Jobs

1. **Lint** - Run ESLint (skips if no lint script found)
2. **Test** - Run tests with Jest/Vitest/etc. (skips if no test script found)
3. **Build** - Build the project (skips if no build script found)

#### Features

- ✅ Multi-package manager support (npm, pnpm, yarn)
- ✅ Automatic dependency caching
- ✅ Smart script detection (skips if script doesn't exist)
- ✅ Coverage report generation and upload
- ✅ Build artifact uploads (dist/, build/, out/)
- ✅ Monorepo support via `working-directory`
- ✅ Custom script names for flexibility

---

### ⚡ Vite + React SPA CI (`ci-vite-react.yml`)

Complete CI workflow for Vite + React SPA applications. Includes linting, type checking, testing with Vitest, E2E tests, and production builds.

#### Basic Usage

```yaml
name: CI

on:
  push:
    branches: [main, develop]
  pull_request:
    branches: [main, develop]

jobs:
  ci:
    uses: Capibara-Corp/shared-workflows/.github/workflows/ci-vite-react.yml@v1
```

#### Full Example with All Options

```yaml
name: CI

on:
  push:
    branches: [main]
  pull_request:
    branches: [main]

jobs:
  ci:
    uses: Capibara-Corp/shared-workflows/.github/workflows/ci-vite-react.yml@v1
    with:
      node-version: '20'              # Node.js version
      package-manager: 'pnpm'         # npm, pnpm, or yarn
      pnpm-version: '9'               # pnpm version (if using pnpm)
      working-directory: '.'          # For monorepos
      run-lint: true                  # Run ESLint
      run-type-check: true            # Run tsc --noEmit
      run-tests: true                 # Run Vitest tests
      run-e2e: false                  # Run E2E tests (Playwright)
      run-build: true                 # Build with Vite
      upload-artifact: true           # Upload dist/ as artifact
      artifact-name: 'dist'           # Name for the artifact
      artifact-retention-days: 7      # Days to retain artifact
      test-coverage: true             # Generate coverage report
```

#### Inputs

| Input | Description | Default |
|-------|-------------|---------|
| `node-version` | Node.js version | `20` |
| `package-manager` | Package manager (`npm`, `pnpm`, `yarn`) | `npm` |
| `pnpm-version` | pnpm version (if using pnpm) | `9` |
| `working-directory` | Working directory for commands | `.` |
| `run-lint` | Run ESLint | `true` |
| `run-type-check` | Run TypeScript type checking | `true` |
| `run-tests` | Run Vitest tests | `true` |
| `run-e2e` | Run E2E tests (Playwright/Cypress) | `false` |
| `run-build` | Run Vite build | `true` |
| `upload-artifact` | Upload dist/ as artifact | `true` |
| `artifact-name` | Name for the build artifact | `dist` |
| `artifact-retention-days` | Days to retain build artifact | `7` |
| `lint-script` | Custom lint script name | `lint` |
| `test-script` | Custom test script name | `test` |
| `e2e-script` | Custom e2e script name | `test:e2e` |
| `build-script` | Custom build script name | `build` |
| `test-coverage` | Generate test coverage report | `false` |

#### Jobs

1. **Lint** - Run ESLint (skips if no lint script found)
2. **Type Check** - Run `tsc --noEmit` (skips if no tsconfig.json)
3. **Test** - Run Vitest tests (skips if no test script found)
4. **E2E** - Run Playwright/Cypress E2E tests (optional)
5. **Build** - Build production bundle with Vite

#### Features

- ✅ Multi-package manager support (npm, pnpm, yarn)
- ✅ Automatic dependency caching
- ✅ Smart script detection (skips if script doesn't exist)
- ✅ TypeScript support with type checking
- ✅ Vitest integration with coverage reports
- ✅ E2E testing support (Playwright)
- ✅ Production build with artifact upload
- ✅ Monorepo support via `working-directory`
- ✅ Configurable artifact retention

#### Downloading Build Artifacts

The `dist/` artifact can be used for deployment:

```yaml
jobs:
  ci:
    uses: Capibara-Corp/shared-workflows/.github/workflows/ci-vite-react.yml@v1
    with:
      upload-artifact: true
      artifact-name: 'production-build'

  deploy:
    needs: ci
    runs-on: ubuntu-latest
    steps:
      - uses: actions/download-artifact@v4
        with:
          name: production-build
          path: dist/
      
      # Deploy dist/ to your hosting provider
      - name: Deploy to hosting
        run: # your deploy command here
```

---

## Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Submit a pull request

## License

MIT License - see [LICENSE](LICENSE) for details.
