# Role: setup_role

Installs DevOps and Kubernetes tools on macOS workstations via Homebrew.

## Requirements

- macOS
- Homebrew installed
- Ansible >=2.15.3
- `community.general` collection (for `homebrew` module)

## Default Packages

The role installs four categories of tools. Customize via `vars` in your playbook.

| Category | Packages |
|----------|----------|
| **Kubernetes** | k9s, flux, helm, kubectx, kubectl, kustomize, minikube, sops, argocd, kind, velero |
| **Cloud** | awscli, azure-cli, google-cloud-sdk |
| **Development** | go, mysql-client, protobuf |
| **Utilities** | grep, jq, netcat, opentofu, tree, wget, yamllint, jsonlint, yq |

See [defaults/main.yml](defaults/main.yml) for exact package lists.

## Role Variables

All variables support comma-separated package names (Homebrew format):

```yaml
k8s_pkg_list: "derailed/k9s/k9s,fluxcd/tap/flux,helm,..."
cloud_pkg_list: "awscli,azure-cli,google-cloud-sdk"
dev_pkg_list: "go,mysql-client,protobuf"
tools_pkg_list: "grep,jq,netcat,opentofu,..."
```

Override any variable to customize:

```yaml
---
- hosts: localhost
  vars:
    k8s_pkg_list: "helm,kubectl,kustomize"  # Minimal K8s
    tools_pkg_list: "jq,yq"                 # Minimal tools
  roles:
    - daurrutia.devtooling_collx.setup_role
```

Skip entire categories with booleans (default: true):

```yaml
install_k8s: false
install_cloud: true
install_dev: false
install_tools: true
```

## Example Playbook

Minimal:

```yaml
---
- hosts: localhost
  roles:
    - daurrutia.devtooling_collx.setup_role
```

With custom packages:

```yaml
---
- hosts: localhost
  vars:
    cloud_pkg_list: "awscli"  # AWS only
    dev_pkg_list: "go,node"   # Go + Node
  roles:
    - daurrutia.devtooling_collx.setup_role
```

## License

GPL-2.0-or-later

## Author

David Urrutia <daurrutia@gmail.com>
