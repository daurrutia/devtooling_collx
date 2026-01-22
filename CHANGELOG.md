# Changelog

All notable changes to this project will be documented in this file.

## [1.3.0] - 2026-01-22

### Added

- Category install toggles (`install_k8s`, `install_cloud`, `install_dev`, `install_tools`)
- Documentation updates: main README, role README, CONTRIBUTING, Copilot instructions
- CHANGELOG initialized

### Changed

- Clarified package customization and category skipping guidance

## [1.2.0] - 2026-01-22

### Added

- DevOps/K8s tools: argocd, kind, velero
- Validation utilities: yamllint, jsonlint, yq
- OpenTofu replaces Terraform tooling
- Simplified Molecule test sequence (syntax, converge, idempotence)

### Removed

- Terraform-specific tools: terragrunt, tfenv
- Unused scaffolding (vars/handlers/tests, extra Molecule playbooks)

## [1.1.0] - 2026-01-21

### Added

- Initial DevOps workstation package sets (K8s, cloud, dev, utilities)
- Molecule testing setup
- Documentation baseline
