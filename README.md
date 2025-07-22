# polkadot-validator-ansible

> **Note:** This repository only covers application-layer configuration. Platform provisioning and cloud infrastructure automation (as found in the original source) are not included. You must supply a pre-installed Linux system.

**Modern Ansible automation for Polkadot/Kusama validator deployment on Linux.**

This project provides application-layer Ansible playbooks and roles for installing and configuring a Polkadot or Kusama validator node on bare-metal or cloud-based Linux systems.

## What This Repo Is

- **Purpose:** Simplifies and modernizes the validator setup process.
- **Scope:** _Application layer only_ (no infrastructure/platform automation).
- **OS Support (Phased):**
  - **Phase 1:** Debian 12, Ubuntu 22.04, Ubuntu 24.04
  - **Phase 2:** AlmaLinux 10, RHEL 10

## Features

- Automatic OS detection (runs the right playbook/roles for your OS)
- Polkadot/Kusama binary download & installation (version easily updatable)
- SMT (Hyperthreading) disablement for single-threaded operation
- WireGuard VPN provisioning & setup (future)
- Idempotent: can be run multiple times without side effects
- Designed for modern Linux (systemd-based) environments

## What This Repo Is NOT

- **Does NOT provision servers, VMs, or cloud instances.**
- **Does NOT manage networking, firewalls, or storage at the infrastructure level.**
- If you need full-stack (infrastructure + application) automation, see the [original project](https://github.com/w3f/polkadot-validator-setup).

## Requirements

- You must provide a clean, supported Linux environment with root or sudo access.
- See [Supported OS](#os-support-phased) for current phase support.

## Usage

```bash
# Example coming soon: Run Ansible playbook after editing inventory file
ansible-playbook -i inventory.yml site.yml
```
