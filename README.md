# MTV AAP Test Playbooks

Simple Ansible playbooks for testing MTV (Migration Toolkit for Virtualization) integration with Ansible Automation Platform (AAP).

## Playbooks

### pre_hook_integration_example.yml
A simple pre-migration hook that prints a success message and displays migration context variables.

### post_hook_integration_example.yml
A simple post-migration hook that prints a success message and displays migration context variables.

## Usage in AAP

1. Create a Project in AAP pointing to this repository
2. Create Job Templates for each playbook
3. Use the Job Template IDs in MTV Hook configuration

## Expected Variables

MTV will automatically pass these variables:
- `vm_name` - Name of the VM being migrated
- `vm_id` - Internal VM ID
- `vm_source_id` - Source system VM ID
- `plan_name` - Migration plan name
- `plan_namespace` - Kubernetes namespace
- `migration_phase` - "PreHook" or "PostHook"
