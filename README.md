# Ansible Collection: daurrutia.devtooling_collx

Automated setup for macOS development workstations. Installs Kubernetes, cloud, and development tools via Homebrew.

**Status**: Production-ready | **License**: GPL-2.0-or-later

## Table of Contents

- [What's Included](#whats-included)
- [Quick Start](#quick-start)
- [Customizing Packages](#customizing-packages)
- [Development](#development)
- [Contributing](#contributing)

## What's Included

This collection installs curated DevOps and Kubernetes tooling:

- **Kubernetes**: k9s, flux, helm, kubectx, kubectl, kustomize, minikube, sops, argocd, kind, velero
- **Cloud**: AWS CLI, Azure CLI, Google Cloud SDK
- **Development**: Go, MySQL client, Protocol Buffers
- **Utilities**: grep, jq, netcat, opentofu, tree, wget, yamllint, jsonlint, yq

## Requirements

- macOS (M1/M2/Intel)
- [Homebrew](https://brew.sh)
- Ansible >=2.15.3

## Quick Start

Install from Galaxy:

```bash
ansible-galaxy collection install daurrutia.devtooling_collx
```

Create `setup.yml`:

```yaml
---
- name: Setup my workstation
  hosts: localhost
  roles:
    - daurrutia.devtooling_collx.setup_role
```

Run:

```bash
ansible-playbook setup.yml
```

Verify idempotence (re-run—should show no changes):

```bash
ansible-playbook setup.yml
```

## Customizing Packages

Override package lists in your playbook:

```yaml
---
- name: Setup my workstation
  hosts: localhost
  vars:
    k8s_pkg_list: helm,kubectl,kustomize  # Minimal K8s
    cloud_pkg_list: awscli                # AWS only
    tools_pkg_list: jq,yq,yamllint        # Validation tools
  roles:
    - daurrutia.devtooling_collx.setup_role
```

Available variables (see [defaults/main.yml](roles/setup_role/defaults/main.yml)):

- `k8s_pkg_list` — Kubernetes tools
- `cloud_pkg_list` — Cloud provider CLIs
- `dev_pkg_list` — Development runtimes
- `tools_pkg_list` — Utilities and validation

Skip categories entirely (defaults: all true):

```yaml
install_k8s: false
install_cloud: true
install_dev: false
install_tools: true
```

## Development

### Setup

Molecule is separate from Ansible; install both:

Option 1: Homebrew + pipx (recommended)

```bash
brew install ansible pipx
pipx ensurepath
pipx install molecule molecule-plugins ansible-lint
source ~/.zshrc
```

Option 2: pip

```bash
python3 -m pip install --upgrade pip
pip install ansible molecule molecule-plugins ansible-lint
```

### Testing

```bash
cd extensions
molecule test
```

Expected output: syntax check, converge (install packages), idempotence test.

### Adding Packages

1. Edit `roles/setup_role/defaults/main.yml` → add to appropriate list
2. Test: `cd extensions && molecule test`
3. Update version in `galaxy.yml` (follow semver)
4. Document in [CHANGELOG.md](CHANGELOG.md)

For new categories, add a task in `roles/setup_role/tasks/main.yml`:

```yaml
- name: Install category packages
  community.general.homebrew:
    name: "{{ category_pkg_list }}"
    state: present
```

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

For project conventions and coding standards, see [.github/copilot-instructions.md](.github/copilot-instructions.md).

## Release

Documented steps to push code, build the collection artifact, and publish to Ansible Galaxy.

### Prerequisites

- Tests pass: `cd extensions && molecule test`
- Version updated in [galaxy.yml](galaxy.yml) following semver
- Changes noted in [CHANGELOG.md](CHANGELOG.md)
- Ansible >= 2.15.3 and `community.general` installed
- Galaxy token available (set `ANSIBLE_GALAXY_TOKEN` or pass `--token`)

### Push, Build, Publish

```bash
# From repo root

# 1) Push code (optional but recommended)
git add -A
git commit -m "release: vX.Y.Z"
git tag vX.Y.Z
git push origin main --tags

# 2) Build the collection artifact
ansible-galaxy collection build
# Produces daurrutia-devtooling_collx-X.Y.Z.tar.gz

# 3) Publish to Galaxy (choose one)
# a) Using env var
export ANSIBLE_GALAXY_TOKEN=YOUR_TOKEN
ansible-galaxy collection publish daurrutia-devtooling_collx-X.Y.Z.tar.gz

# b) Passing token explicitly
ansible-galaxy collection publish daurrutia-devtooling_collx-X.Y.Z.tar.gz \
  --token YOUR_TOKEN
```

Verification: check the release on Galaxy and install locally:

```bash
ansible-galaxy collection install daurrutia.devtooling_collx:X.Y.Z --force
```

## License

GPL-2.0-or-later

## Author

David Urrutia
