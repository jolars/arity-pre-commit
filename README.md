# arity-pre-commit

[![CI](https://github.com/jolars/arity-pre-commit/actions/workflows/ci.yml/badge.svg)](https://github.com/jolars/arity-pre-commit/actions/workflows/ci.yml)

A [pre-commit](https://pre-commit.com) hook for
[arity](https://github.com/jolars/arity), a language server, formatter, and
linter for the R language.

Distributed as a thin Python package that depends on the
[`arity` PyPI package](https://pypi.org/project/arity/), so pre-commit
installs a prebuilt binary wheel—no Rust toolchain or R installation
required. Wheels are available for Linux, macOS, and Windows on both x64 and
ARM64.

## Usage

Add this to your `.pre-commit-config.yaml`:

```yaml
repos:
  - repo: https://github.com/jolars/arity-pre-commit
    # arity version
    rev: v0.22.0
    hooks:
      # Lint .R files
      - id: arity-lint
      # Format the same files in place
      - id: arity-format
```

To apply safe lint autofixes before formatting (arity's fix-then-format
pipeline), pass `--fix`:

```yaml
- id: arity-lint
  args: [--fix]
- id: arity-format
```

To check formatting without rewriting files:

```yaml
- id: arity-format
  args: [--check]
```

Both hooks pass `--force-exclude`, so files matched by `exclude` or
`extend-exclude` in your `arity.toml` are skipped even though pre-commit
names staged files explicitly.

## Versioning

Tags mirror arity releases: installing at tag `vX.Y.Z` gives you arity X.Y.Z.
New tags are created automatically when a new arity version is published to
PyPI.

## License

MIT
