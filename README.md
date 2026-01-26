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

## Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Submit a pull request

## License

MIT License - see [LICENSE](LICENSE) for details.
