# Contributing

## Development Workflow

1. **Branch** - Create feature branch from `main`
2. **Develop** - Make changes with tests
3. **PR** - Open pull request with CI checks
4. **Review** - Address feedback
5. **Merge** - Squash merge to `main`

## Standards

- **Commits**: [Conventional Commits](https://www.conventionalcommits.org/) (`feat:`, `fix:`, `docs:`, etc.)
- **Branching**: Trunk-based development
- **CI**: All checks must pass before merge
- **Reviews**: Required for all changes

## CI Checks

PRs automatically run:
- Linting (Ruff, Black)
- Security scanning (Bandit, Gitleaks)
- Documentation checks (Markdownlint)

## Getting Started

```bash
# Clone
git clone <repo-url>
cd <repo>

# Install dependencies
pip install -e ".[dev]"

# Run checks locally
ruff check .
black --check .
```
