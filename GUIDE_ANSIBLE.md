# Ansible Validator Application Layer Guide

This repository provides Ansible playbooks and roles to **install and configure a Polkadot or Kusama validator node** on supported Linux systems.  
**Focus:** Application-layer automation only (no infrastructure or cloud provisioning).

---

## Supported OS (Phase 1)

- Debian 12
- Ubuntu 22.04 LTS
- Ubuntu 24.04 LTS

> _Support for AlmaLinux 10 and RHEL 10 will be added in future phases._

---

## Prerequisites

- [Ansible](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html) (v2.8+)

  Install on your control node (Linux, WSL2, or compatible VM):

  ```bash
  sudo apt install ansible
  ```

- At least one Linux server/VM with:
  - SSH access
  - A non-root user with `sudo` privileges (SSH key authentication recommended)
  - Python installed (default on most modern distributions)

_Note: Remote users must have `sudo` rights. Passwordless sudo is optional but recommended for automation._

---

## Inventory Setup

Create an inventory file (e.g., `inventory.yml`).  
You can place this anywhere in your repo.

**Add your validator nodes:**  
Example (`inventory.yml`):

```ini
[validator_0]
147.75.76.65 ansible_user=alice

[validator_1]
162.12.35.55 ansible_user=bob

[validator:children]
validator_0
validator_1

[all:vars]
project=alice-in-wonderland
polkadot_binary_url='https://github.com/paritytech/polkadot/releases/download/vX.Y.Z/polkadot'
polkadot_binary_checksum='sha256:...'
chain=polkadot
polkadot_network_id=polkadot
node_exporter_enabled='false'
```

`ansible_user` should **not** be `root` for security.  
For additional variables, see the sample inventory and role documentation.

---

## Running the Playbook

Clone your repo and run the main playbook:

```bash
git clone https://github.com/SafeStakeIo/polkadot-validator-ansible.git
cd polkadot-validator-ansible/ansible
ansible-playbook -i inventory.yml main.yml --become --ask-become-pass
```

`--become` and `--ask-become-pass` allow `sudo` tasks on remote hosts.

---

## Updating Polkadot/Kusama

To upgrade the validator:

Update `polkadot_binary_url` and `polkadot_binary_checksum` in your inventory.  
Re-run the playbook as above.

---

## Notes & Recommendations

- Telemetry URL is optional and may expose validator IP; consider using a private telemetry server.
- You can group multiple validators under `[validator:children]` for batch management.
- This playbook is **idempotent**—safe to run multiple times.
- All setup and configuration is done via Ansible; no manual steps required on remote nodes after SSH is configured.

---

## Project Roadmap (WIP)

- Automatic OS detection (phase-in support for additional OSes)
- WireGuard VPN provisioning and configuration
- SMT (Simultaneous Multithreading) disablement for optimized performance

_See [README.md](../README.md) for the most current roadmap and feature status._

---

## Support and Contributions

For questions, support, or to contribute, see the [issue tracker](https://github.com/SafeStakeIo/polkadot-validator-ansible/issues) or submit a pull request.

---

**End of Guide**
