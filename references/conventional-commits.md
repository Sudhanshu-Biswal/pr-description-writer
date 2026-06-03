# Conventional Commits — Type Detection Reference

## Commit prefix → PR type mapping

| Prefix | PR Type | Emoji |
|---|---|---|
| `feat:` / `feature:` | Feature | ✨ |
| `fix:` / `bugfix:` | Bug Fix | 🐛 |
| `refactor:` / `ref:` | Refactor | ♻️ |
| `chore:` / `build:` | Chore | 🔧 |
| `ci:` / `cd:` | CI/CD | 🔧 |
| `docs:` / `doc:` | Documentation | 📝 |
| `perf:` / `optim:` | Performance | ⚡ |
| `test:` / `tests:` | Tests | 🧪 |
| `style:` | Style / Formatting | 🎨 |
| `revert:` | Revert | ⏪ |
| `security:` / `sec:` | Security | 🔒 |

## Fallback: file-path heuristics

| Files changed | Likely type |
|---|---|
| `*.test.*`, `*.spec.*`, `__tests__/` | Tests |
| `*.md`, `docs/`, `README` | Docs |
| `.github/`, `*.yml`, `*.yaml`, `Dockerfile` | CI/Config |
| `src/`, `lib/`, `app/` with logic changes | Feature or Fix |
| Same files, lines moved not added | Refactor |

## Breaking changes

Flag as breaking if:
- Commit message contains `BREAKING CHANGE:` footer
- `!` after type: `feat!:` or `fix(api)!:`
- Diff removes or renames exported functions/classes/endpoints
- Diff changes function signatures in public interfaces
