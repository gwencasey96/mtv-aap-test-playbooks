# MTV AAP Test Playbooks

Small Ansible playbooks to try **MTV (Migration Toolkit for Virtualization)** talking to **Ansible Automation Platform (AAP)**.

## What is real vs sample?

- **`pre_hook_integration_example.yml`** and **`post_hook_integration_example.yml`** use the **same variable names MTV sends to AAP** when you use a hook with a job template (`vm_name`, `plan_name`, `migration_phase`, and so on). The `default('N/A')` bits are only so the playbook still runs if you run it by hand without MTV.
- The files under **`examples/`** are **made-up examples** (dummy values and shortened YAML). They show the **kind of data** MTV uses for the older style hook that runs a playbook **on the cluster** with files next to the playbook—not a copy of a real migration.

## Playbooks

- **`pre_hook_integration_example.yml`** — runs before migration; prints a short message and the context vars.
- **`post_hook_integration_example.yml`** — runs after migration; same idea.

## Try it in AAP

1. Add this repo as an **AAP Project**.
2. Create a **Job Template** for each playbook (or one template per hook you need).
3. In MTV, point the hook at the **job template ID** from AAP.

## Two ways MTV gives your playbook context

**1. AAP job template (what these two playbooks target)**  
MTV starts a job on AAP and passes **extra variables** only. There is no `plan.yml` or `workload.yml` file from MTV for this path. Typical names:

`vm_name`, `vm_id`, `vm_source_id`, `plan_name`, `plan_namespace`, `migration_phase`

**2. Inline playbook on the cluster (older flow)**  
MTV runs Ansible in a pod and mounts a folder (often `/tmp/hook/`) with files such as **`plan.yml`**, **`workload.yml`**, and your **`playbook.yml`**. Your playbook can load the YAML files with `include_vars`. The real `workload.yml` shape depends on the **source** (VMware, oVirt, etc.).

The **`examples/`** folder holds short sample YAML so you can see what those files *look like* for flow (1) vs (2). **`examples/vm.yml`** is just those AAP extra vars written in one file for reading—it is **not** a file MTV drops on disk for AAP.

More detail: [Forklift hooks doc](https://github.com/kubev2v/forklift/blob/main/docs/hooks.md).
