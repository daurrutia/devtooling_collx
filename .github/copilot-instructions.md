# GitHub Copilot Instructions for devtooling_collx

## Project Context

This is an Ansible collection for macOS development workstation setup. It automates the installation of development tools via Homebrew.

## Key Conventions

### File Structure
- **Collection metadata**: `galaxy.yml`
- **Role location**: `roles/setup_role/`
- **Package definitions**: `roles/setup_role/defaults/main.yml`
- **Tasks**: `roles/setup_role/tasks/main.yml`
- **Testing**: `extensions/molecule/`

### Coding Standards

**YAML Formatting**:
- Use 2 spaces for indentation
- Always include `---` document start marker
- Use full FQCN (Fully Qualified Collection Names) for modules: `community.general.homebrew`, `ansible.builtin.include_role`

**Variable Naming**:
- Package lists end with `_pkg_list` (e.g., `k8s_pkg_list`, `dev_pkg_list`)
- Use comma-separated strings for Homebrew package lists

**Task Naming**:
- Start with action verb: "Install", "Configure", "Ensure"
- Be descriptive about what's being installed/configured
- Example: "Install K8s packages" not "Install packages"

### Module Usage

**Homebrew Module** (`community.general.homebrew`):
- Always use `state: present` for installation
- Package names can be comma-separated strings
- Support tap notation: `derailed/k9s/k9s`

### Version Management

When suggesting version bumps:
- Update `version` in `galaxy.yml`
- Follow semantic versioning
- Update `CHANGELOG.md` with changes
- Patch: bug fixes, documentation
- Minor: new packages, non-breaking features
- Major: breaking changes

### Testing

- Use Molecule for testing
- Test location: `extensions/molecule/default/`
- Run from `extensions/` directory: `molecule test`

### Platform Specifics

- **Target OS**: macOS only
- **Package Manager**: Homebrew exclusively
- **Ansible Version**: >=2.15.3
- **Required Collection**: `community.general` >=8.0.0
- **IaC**: OpenTofu (formerly Terraform)

## Common Tasks

### Adding a new package
1. Add to appropriate variable in `roles/setup_role/defaults/main.yml`
2. Ensure task exists in `roles/setup_role/tasks/main.yml` for that category
3. Test with Molecule
4. Update version and CHANGELOG

### Adding a new package category
1. Create new variable in `defaults/main.yml`: `category_pkg_list`
2. Add task in `tasks/main.yml`:
   ```yaml
   - name: Install category packages
     community.general.homebrew:
       name: "{{ category_pkg_list }}"
       state: present
   ```
3. Document in README.md

## Don't Suggest

- Installing packages without Homebrew
- Linux-specific tools or configurations
- Docker-based testing (Molecule uses local execution)
- Removing existing packages
- System-level changes outside package management

## Custom Instructions

### General Principles

- Prioritize truth, accuracy, and humility over confidence.
- Distinguish established facts, reasonable inference, lived or traditional experience, and speculation.
- Challenge assumptions when they affect conclusions.
- State uncertainty, evidence limits, and risks explicitly instead of guessing.
- Evaluate claims with integrity; avoid overstating effectiveness where evidence is weak or mixed.
- Communicate plainly and respectfully; explain technical terms when first introduced.
- Focus on methods, reasoning, and practical consequences; avoid implicit praise. Emphasize failure modes, constraints, and truthfulness.

### Technical

- Provide guidance that is complete, syntactically correct, contextually relevant, and aligned with repo conventions or best practices.
- When uncertain about conventions, call out the uncertainty and suggest checking documentation or teammates.
- When multiple approaches exist, outline pros and cons before recommending one.
- Reference external resources only when current and relevant.
- Document clearly using structured formats where helpful; use emphasis sparingly.
