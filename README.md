# 💽 Ansible Linux Automation
<p align="center"> <img src="https://img.shields.io/badge/ansible-automation-blue?style=for-the-badge" /> <img src="https://img.shields.io/badge/idempotent-yes-success?style=for-the-badge" /> <img src="https://img.shields.io/badge/security-hardening-critical?style=for-the-badge" /> <img src="https://img.shields.io/badge/linux-automation-orange?style=for-the-badge" /> <img src="https://img.shields.io/badge/CI-GitHub%20Actions-blue?style=for-the-badge" /></p>

Production-style Ansible automation for Linux configuration, idempotent deployments, and baseline security hardening.

## 📔 Overview

This repository contains production-style Ansible playbooks designed to automate Linux server configuration and apply baseline security hardening.

The project focuses on demonstrating practical Infrastructure as Code (IaC) principles used by modern DevOps and Platform Engineering teams.

Two primary automation workflows are included:

### 🤖 Webserver Automation

A modular Ansible role that installs and configures Nginx using:

- Role-based architecture
- Jinja2 configuration templates
- Handlers for controlled service restarts
- Fully idempotent task execution

### Linux Hardening Automation

A security-focused playbook implementing baseline server hardening controls commonly used in cloud environments.

The goal is to make Linux infrastructure *secure by default* through repeatable automation.

## ⚙️ Why Idempotency Matters

A core principle of configuration management is idempotency.

An idempotent playbook ensures that running automation multiple times results in the *same final system state*.

This provides several critical benefits:

- Predictable deployments
- Elimination of configuration drift
- Safe re-execution during failures
- Reliable automation pipelines
- Consistent server rebuilds

In production environments this means automation can be safely run:

- During CI/CD deployments
- After partial infrastructure failures
- During incident recovery
- Across large server fleets
- The webserver role in this repository is designed to be fully idempotent.

### 🔁 Idempotency Verification

After the initial deployment, running the playbook again should produce zero changes, confirming configuration stability.

Example output from a second run:

```
PLAY RECAP *****************************************************************

server1 : ok=12  changed=0  unreachable=0  failed=0
```

This confirms:

The system configuration is already correct
    No unnecessary changes are applied
    Automation can safely be re-run
    This behaviour is critical for reliable infrastructure automation.

## 🔐 Linux Hardening Controls

Cloud servers are constantly exposed to automated scanning, probing, and brute-force attacks.
Hardening is therefore a baseline security requirement, not an optional step.
This playbook implements several fundamental controls aligned with practices found in:

- CIS Benchmarks
- AWS security recommendations
- Enterprise Linux hardening guidelines

### Implemented Security Controls
#### Disable Root SSH Login
Prevents attackers from targeting the most privileged account directly.
#### Enforce Password Policies
Applies password complexity requirements to reduce credential-based attacks.
#### Configure UFW Firewall
Limits inbound network access to only required ports:

- SSH
- HTTP

Reducing the exposed attack surface.

#### Install and Enable Fail2ban

Protects the system against repeated authentication attempts by automatically banning offending IP addresses.

#### Remove Unnecessary Packages

Minimizes attack surface by removing outdated or unused utilities.

## 🌍 Real-World Applicability

This project reflects how modern infrastructure teams manage systems at scale.

### Infrastructure as Code

Instead of manually configuring servers, infrastructure becomes:

- Version controlled
- Repeatable
- Auditable
- Automated

### Cloud-Ready Automation

These playbooks can be applied to:

- AWS EC2 instances
- On-premise virtual machines
- Container environments
- CI/CD pipelines
- Image build workflows (Golden AMIs)

### Security as Code

Hardening becomes:

- Enforced automatically
- Version controlled
- Reproducible
- Testable

This approach allows security policies to scale across infrastructure environments.

```
:classical_building: Project Structure
ansible-linux-automation/
├── inventory/
│   └── hosts.ini
├── roles/
│   └── webserver/
│       ├── tasks/
│       │   └── main.yml
│       ├── handlers/
│       │   └── main.yml
│       ├── templates/
│       │   └── nginx.conf.j2
│       └── defaults/
│           └── main.yml
├── playbooks/
│   ├── site.yml
│   └── hardening.yml
├── ansible.cfg
└── README.md
```
## 📦 Requirements

To run these playbooks you will need:

- A Linux target host (*WSL* Ubuntu or Debian recommended)
- Ansible 2.12+ 
- Python 3
- SSH access with sudo privileges

Install Ansible on your control node:

```
sudo apt update
sudo apt install ansible
```
Verify installation:

`ansible --version`

## ▶️ Running the Playbooks
Dry Run (Check Mode)

Preview changes without applying them.

`ansible-playbook playbooks/site.yml --check`

Apply Webserver Configuration
`ansible-playbook playbooks/site.yml`

Apply Linux Hardening

`ansible-playbook playbooks/hardening.yml`

If Privilege Escalation Requires a Password
Some systems require a password for sudo access.

`ansible-playbook playbooks/site.yml --ask-become-pass`

## 🚀 Future Improvements

Possible enhancements for this project include:

- Adding Molecule tests for role validation
- Integrating Ansible linting via GitHub Actions
- Expanding hardening to align with CIS benchmarks
- Supporting multi-environment inventories

Implementing:

- SSH key-only authentication
- automatic security updates
- centralized logging
- auditd monitoring

Infrastructure automation evolves continuously, and this repository will grow as additional best practices are explored.

## 🎯 Learning Focus

This repository is part of an ongoing exploration of:

- Infrastructure as Code
- Configuration management
- Linux security hardening
- Reliable automation practices
- Reproducible infrastructure

The aim is not only to **automate configuration**, but to understand why modern infrastructure is designed this way.

Automation should be:

- Predictable
- Secure
- Repeatable
- Explainable
