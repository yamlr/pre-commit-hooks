# Yamlr Pre-Commit Hooks

Official pre-commit hooks for [Yamlr](https://yamlr.dev) — the autonomous Kubernetes manifest resolution and auto-healing engine.

## Prerequisites

Yamlr pre-commit hooks run the native `yamlr` CLI directly on your developer workstation. Ensure `yamlr` is installed:

### macOS & Linux
```bash
curl -fsSL https://get.yamlr.dev/install.sh | bash
# or via Homebrew:
brew install yamlr/tap/yamlr
```

### Windows (PowerShell)
```powershell
irm https://get.yamlr.dev/install.ps1 | iex
```

---

## Configuration

Add the following to your `.pre-commit-config.yaml`:

```yaml
repos:
  - repo: https://github.com/yamlr/pre-commit-hooks
    rev: v0.1.0
    hooks:
      # Automatically fix broken selectors, typo fields, ports, and schema deviations
      - id: yamlr-heal
        args: ["--apply"]

      # Strict offline audit against official Kubernetes OpenAPI schemas
      - id: yamlr-scan
        args: ["--fail-on", "error"]
```

---

## Available Hooks

| Hook ID | Description | Default Arguments |
| :--- | :--- | :--- |
| `yamlr-heal` | Lossless, comment-preserving auto-repair of Kubernetes manifests. | `["--apply"]` |
| `yamlr-scan` | Read-only forensic audit against official Kubernetes OpenAPI schemas. | `["--fail-on", "error"]` |
| `yamlr-fmt` | Canonical Kubernetes manifest formatter. Normalizes indentation and hierarchy. | `["-w"]` |
| `yamlr-diff` | Previews color unified diff of proposed repairs without modifying files. | `["--unified"]` |

---

## License

Yamlr is proprietary software owned by Timonel Labs. See [yamlr.dev](https://yamlr.dev) for documentation and terms.
