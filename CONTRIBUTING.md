# Contributing

Thanks for helping improve `daurrutia.devtooling_collx`!

## Requirements

- Ansible >= 2.15.3
- macOS with Homebrew
- `community.general` collection
- Molecule + plugins + ansible-lint (see README Development section)

## Setup

```bash
brew install ansible pipx
pipx ensurepath
pipx install molecule molecule-plugins ansible-lint
source ~/.zshrc
```

## Workflow

1. Create a branch from `main`.
2. Make changes with tests:

   ```bash
   cd extensions
   molecule test
   ```

3. Update docs as needed (README, role README).
4. Bump version in `galaxy.yml` (semver) and add an entry to `CHANGELOG.md`.
5. Commit with a clear message.
6. Open a PR.

## Versioning

- Patch: bug fixes / docs
- Minor: new packages / features (backward compatible)
- Major: breaking changes

## PR Checklist

- [ ] Tests: `cd extensions && molecule test`
- [ ] Docs updated (README/role README if needed)
- [ ] Version bumped in `galaxy.yml`
- [ ] `CHANGELOG.md` updated

## Reporting Issues

- Include Ansible version (`ansible --version`)
- macOS version and chip (Intel/Apple Silicon)
- Command output and logs if possible
