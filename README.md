# simple-versioned-reusable-workflow

A minimal example of a versioned, reusable GitHub Actions workflow.

## Reusable workflow

The [`hello-world.yml`](.github/workflows/hello-world.yml) workflow can be called from any repository:

```yaml
jobs:
  greet:
    uses: magnusp-org/simple-versioned-reusable-workflow/.github/workflows/hello-world.yml@v1
```

It simply echoes `Hello world` and serves as a template for building more complex reusable workflows.

## Versioning

Releases follow [Semantic Versioning](https://semver.org/) (`vMAJOR.MINOR.PATCH`).

### How to release a new version

1. Push a version tag to `main`:
   ```bash
   git tag v1.0.0
   git push origin v1.0.0
   ```
2. The [Release workflow](.github/workflows/release.yml) automatically creates a GitHub Release with auto-generated release notes.
3. The [Update Major Version Tag workflow](.github/workflows/update-major-tag.yml) automatically moves the `vMAJOR` tag (e.g. `v1`) to the new release commit so callers can pin to a major version without updating their workflow files.

### Pinning strategies

| Reference | Behaviour |
|-----------|-----------|
| `@v1` | Receives all minor/patch updates within major version 1 |
| `@v1.2.3` | Pinned to an exact release — most reproducible |
