<div align="center">

# Ansible Role: Angie

[![Ansible Core Version](https://img.shields.io/badge/ansible->=2.12-EE0000.svg?style=for-the-badge&logo=ansible)](https://galaxy.ansible.com/)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg?style=for-the-badge)](https://opensource.org/licenses/MIT)
[![Angie Web Server](https://img.shields.io/badge/Angie-Web%20Server-00A98F.svg?style=for-the-badge)](https://angie.software/)

An Ansible role that installs and configures the **Angie** web server across all popular Linux distributions.

[Official Website](https://angie.software/) • [Documentation](https://angie.software/docs/) • [Ansible Galaxy](https://galaxy.ansible.com/)

</div>

---

## 🌟 Features

* **Cross-platform**: Native support for Debian, Ubuntu, RHEL, CentOS Stream, Rocky Linux, AlmaLinux, Fedora, openSUSE, and SLES.
* **Official Repositories**: Automatically configures official GPG keys and YUM/APT/Zypper repositories.
* **Idempotent**: Safe to run repeatedly — changes are only applied when required.
* **Air-gapped Ready**: Repository management can be disabled (`angie_manage_repo: false`) for enterprise environments with internal mirrors.

---

## 💻 Supported Operating Systems

| OS Family | Supported Distributions |
| :--- | :--- |
| **Debian** | Ubuntu (20.04, 22.04, 24.04+), Debian (11, 12+) |
| **Red Hat (EL)** | RHEL, CentOS Stream, Rocky Linux, AlmaLinux (8, 9+), Oracle Linux |
| **Fedora** | Fedora (39, 40+) |
| **SUSE** | openSUSE (Leap, Tumbleweed), SLES (15+) |

---

## 📦 Installation

Install the role via `ansible-galaxy`:

```bash
ansible-galaxy role install halif.angie

```

Or add it to your project's `requirements.yml`:

```yaml
roles:
  - name: halif.angie
```

## ⚙️ Role Variables

| Variable | Type | Default | Description |
| :--- | :---: | :---: | :--- |
| `angie_package_state` | `string` | `present` | Target package state (`present`, `latest`). |
| `angie_manage_repo` | `bool` | `true` | Whether to add official Angie repositories. Set to `false` for air-gapped environments. |
| `angie_repo_channel` | `string` | `main` | Repository channel (`main`). |
| `angie_service_state` | `string` | `started` | Systemd service target state (`started`, `stopped`). |
| `angie_service_enabled` | `bool` | `true` | Enable service autostart on boot. |


## 🚀 Example Playbooks
### Basic Installation

```yaml
- hosts: webservers
  become: true
  roles:
    - role: halif.angie
```

Upgrade Package to Latest Version

```yaml
- hosts: webservers
  become: true
  roles:
    - role: halif.angie
      vars:
        angie_package_state: latest
```

### Air-gapped / Isolated Network Setup

```yaml
- hosts: isolated_hosts
  become: true
  roles:
    - role: halif.angie
      vars:
        angie_manage_repo: false
```

### License
MIT