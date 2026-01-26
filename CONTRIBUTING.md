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

## Release Process

Follow these steps to create and publish a new release of the collection:

1. Ensure tests pass:

   ```bash
   cd extensions
   molecule test
   ```

2. Bump the version in [galaxy.yml](galaxy.yml) using semantic versioning.
3. Add a corresponding entry to [CHANGELOG.md](CHANGELOG.md).
4. Commit and tag the release:

   ```bash
   git add -A
   git commit -m "release: vX.Y.Z"
   git tag vX.Y.Z
   git push origin main --tags
   ```

5. Build the collection artifact from repo root:

   ```bash
   ansible-galaxy collection build
   # Produces daurrutia-devtooling_collx-X.Y.Z.tar.gz
   ```

6. Publish to Galaxy (use an env var or pass token):

   ```bash
   # Option A: Env var
   export ANSIBLE_GALAXY_TOKEN=YOUR_TOKEN
   ansible-galaxy collection publish daurrutia-devtooling_collx-X.Y.Z.tar.gz

   # Option B: CLI token
   ansible-galaxy collection publish daurrutia-devtooling_collx-X.Y.Z.tar.gz \
     --token YOUR_TOKEN
   ```

7. Verify on Ansible Galaxy and optionally test install locally:

   ```bash
   ansible-galaxy collection install daurrutia.devtooling_collx:X.Y.Z --force
   ```

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
