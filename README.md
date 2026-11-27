# Official Pre-Commit Hooks for Yamlr

[![Pre-Commit](https://img.shields.io/badge/pre--commit-enabled-brightgreen?logo=pre-commit&logoColor=white&style=flat-square)](https://pre-commit.com)
[![Yamlr Version](https://img.shields.io/github/v/release/yamlr/yamlr?style=flat-square&color=blue)](https://github.com/yamlr/yamlr/releases)
[![License: Proprietary](https://img.shields.io/badge/License-Proprietary-orange?style=flat-square)](https://github.com/yamlr/yamlr/blob/main/LICENSE)

Integrate [**Yamlr**](https://github.com/yamlr/yamlr) directly into your local Git pre-commit workflow. Automatically detect and heal broken Kubernetes manifests, invalid API deprecations, schema mismatches, and broken cross-resource links before committing code.

---

## 🚀 Quick Setup

Add the following block to your repository's `.pre-commit-config.yaml`:

```yaml
repos:
  - repo: https://github.com/yamlr/yamlr
    rev: v0.1.4
    hooks:
      # Option A: Canonical formatter (aligns spec keys to standard K8s schema order)
      - id: yamlr-fmt

      # Option B: Manifest auto-repair (upgrades deprecated APIs and fixes syntax)
      - id: yamlr-fix

      # Option C: Read-only heal preview (fails with diff if repairs are needed)
      - id: yamlr-heal

      # Option D: Read-only schema and relational validator gate
      - id: yamlr-scan
```

Install the pre-commit hook in your local Git repository:
```bash
pre-commit install
```

---

## 🛠 Available Hooks

| Hook ID | Description | Mode |
| :--- | :--- | :--- |
| `yamlr-scan` | Performs a read-only audit across all staged manifests against official OpenAPI schemas. Exits with non-zero code on errors. | Read-Only |
| `yamlr-fmt` | Formats manifest indentation and key ordering to Kubernetes OpenAPI schema conventions (`-w`). | In-Place Write |
| `yamlr-fix` | Auto-heals deprecated API versions, broken selector ports, and missing specs in-place. | In-Place Write |
| `yamlr-heal` | Preview proposed multi-resource repairs with unified color diff without modifying files. | Read-Only |

---

## ⚙️ Advanced Configuration

Pass custom flags to target specific Kubernetes versions or strictness levels:

```yaml
  - repo: https://github.com/yamlr/yamlr
    rev: v0.1.4
    hooks:
      - id: yamlr-scan
        args: ["--k8s-version", "1.36", "--fail-on", "error"]
```

---

## 📚 Documentation & Issues

- **Main Repository**: [github.com/yamlr/yamlr](https://github.com/yamlr/yamlr)
- **Documentation**: [yamlr.dev/docs](https://yamlr.dev/docs)
- **File an Issue**: [github.com/yamlr/yamlr/issues](https://github.com/yamlr/yamlr/issues)