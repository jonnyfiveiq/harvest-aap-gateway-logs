# AAP Gateway Log Harvest Playbook

This repository contains an Ansible playbook to harvest logs and configuration from an **Ansible Automation Platform 2.5 RPM Gateway server** and send them to a central location.

## Files

- `gateway-log-harvest.yml` — the playbook that collects logs, configs, and journals.

## Usage in Ansible Automation Platform

1. **Upload this repo to your Controller** (as a Project).
2. **Create a Job Template** with:
   - **Inventory**: The host(s) running the AAP Gateway RPM install.
   - **Execution Environment**: `ee-supported`.
   - **Playbook**: `gateway-log-harvest.yml`.
   - **Privilege Escalation**: Check *Enable privilege escalation* (`become: true`).
3. **Set Extra Vars** if desired:
   ```yaml
   log_days: 5
   ship_mode: "controller"   # or "remote"
   remote_host: "logs01.example.com"
   remote_path: "/srv/gateway-drops"
   ```
4. Run the job.  
   - With `ship_mode: controller`, the logs are fetched to Controller artifacts.  
   - With `ship_mode: remote`, they’re copied to the specified `remote_host` path.

## Requirements

- Ansible Automation Platform 2.5+ (RPM install target).  
- Systemd-based logging (journald).  
- SSH access from Controller to remote log collector (if using `ship_mode: remote`).

