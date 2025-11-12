# Arbeidstilsynet/action-dotnet-get-csproj-metadata

Action to extract the package name and version from csproj

## Requirements

- The action must run on a runner with `bash` and `find` available (e.g., Ubuntu runners).
- The `working-directory` must contain exactly one `.csproj` file, or the first found will be used.
- The `.csproj` file should contain `<PackageId>` or `<AssemblyName>`, and `<Version>` elements.

## Inputs

| Name                | Description                       | Required | Default |
|---------------------|-----------------------------------|----------|---------|
| `working-directory` | The path to the project directory | Yes      |         |

## Outputs

| Name      | Description         |
|-----------|---------------------|
| `name`    | The package name    |
| `version` | The package version |

## Usage

```yaml
jobs:
  get-csproj-metadata:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4

      - uses: Arbeidstilsynet/action-dotnet-get-csproj-metadata@v1
        id: csproj-metadata
        with:
          working-directory: ./src/MyProject

      - name: Show package metadata
        run: |
          echo "Package name: ${{ steps.csproj-metadata.outputs.name }}"
          echo "Package version: ${{ steps.csproj-metadata.outputs.version }}"
```

## Versioning

This repository uses a simple versioning system based on the `VERSION` file.
When you update the `VERSION` file and push to `main`, a Git tag with that version is created or updated automatically by the workflow.
If you make breaking changes to the action, bump the version and update `CHANGELOG.md`.
