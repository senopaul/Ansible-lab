# 🔧 Ansible Multi-Node Lab

> Automating infrastructure configuration across multiple CentOS servers using Ansible — built hands-on on Apple M3 silicon using UTM virtualization.

![Ansible](https://img.shields.io/badge/Ansible-EE0000?style=for-the-badge&logo=ansible&logoColor=white)
![Linux](https://img.shields.io/badge/Linux-FCC624?style=for-the-badge&logo=linux&logoColor=black)
![CentOS](https://img.shields.io/badge/CentOS-262577?style=for-the-badge&logo=centos&logoColor=white)
![Git](https://img.shields.io/badge/Git-F05032?style=for-the-badge&logo=git&logoColor=white)
![YAML](https://img.shields.io/badge/YAML-CB171E?style=for-the-badge&logo=yaml&logoColor=white)

---

## 🏗️ Lab Architecture

```
┌─────────────────────────────────────────────────────┐
│                   HOME LAB                          │
│                                                     │
│   ┌─────────────────────────┐                       │
│   │   AnsibleController     │                       │
│   │   192.168.189.106       │                       │
│   │   CentOS | SSH Keys     │                       │
│   └────────────┬────────────┘                       │
│                │                                    │
│       SSH Key Authentication                        │
│                │                                    │
│      ┌─────────┴──────────┐                         │
│      │                    │                         │
│  ┌───▼──────────┐  ┌──────▼────────┐                │
│  │   Target1    │  │   Target2     │                │
│  │ 192.168.189  │  │ 192.168.189   │                │
│  │    .205      │  │    .121       │                │
│  │   CentOS     │  │   CentOS      │                │
│  └──────────────┘  └───────────────┘                │
│                                                     │
│   Virtualization: UTM on Apple M3                   │
│   SSH Client: Termius                               │
└─────────────────────────────────────────────────────┘
```

---

## ✅ What This Lab Does

| Task | Status |
|------|--------|
| SSH key authentication between controller and nodes | ✅ Done |
| Ansible ping across all nodes | ✅ Done |
| Automated package updates across fleet | ✅ Done |
| Automated software installation on all nodes | ✅ Done |

---

## 📁 Repository Structure

```
ansible-lab/
├── inventory.txt        # Host definitions and connection config
├── demo-playbook.yml    # Main playbook — update and install
├── ansible.cfg          # Ansible configuration
└── README.md            # This file
```

---

## 🔐 Authentication Setup

This lab uses **SSH key-based authentication** — the production standard for Ansible deployments.

```bash
# Generate SSH key on controller
ssh-keygen -t rsa

# Copy public key to each target node
ssh-copy-id senopaul@192.168.189.205
ssh-copy-id senopaul@192.168.189.121
```

No passwords stored. No password prompts. Secure and automated.

---

## 📋 Inventory Configuration

```ini
Target1 ansible_host=192.168.189.205 ansible_user=senopaul
Target2 ansible_host=192.168.189.121 ansible_user=senopaul
```

---

## 📜 Playbook — Update & Install

```yaml
---
- name: Update and install VLC on servers
  hosts: all
  become: yes
  tasks:
    - name: Update all packages on hosts
      yum:
        name: "*"
        state: latest
      ignore_errors: yes

    - name: Install VLC player
      yum:
        name: vlc
        state: present
      ignore_errors: yes
```

---

## 🚀 Running the Lab

**Test connectivity across all nodes:**
```bash
ansible all -m ping -i inventory.txt
```

**Expected output:**
```
Target1 | SUCCESS => {"ping": "pong"}
Target2 | SUCCESS => {"ping": "pong"}
```

**Run the full playbook:**
```bash
ansible-playbook demo-playbook.yml -i inventory.txt
```

**Expected output:**
```
TASK [Update all packages on hosts]
changed: [Target1]
changed: [Target2]

TASK [Install VLC player]
changed: [Target1]
changed: [Target2]

Target1 : ok=3  changed=2  failed=0
Target2 : ok=3  changed=2  failed=0
```

---

## 🛠️ Tech Stack

| Tool | Purpose |
|------|---------|
| Ansible | Configuration management and automation |
| CentOS | Operating system on all nodes |
| UTM | Virtualization on Apple M3 silicon |
| Termius | SSH client for terminal access |
| Git | Version control |

---

## 🌍 About

Built by **Paul Ssenoga** — Software Engineer transitioning into DevOps.

This lab was built hands-on after a 10-hour workday. Every error is documented. Every fix earned.

Part of a broader DevOps journey covering:

![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white)
![Kubernetes](https://img.shields.io/badge/Kubernetes-326CE5?style=for-the-badge&logo=kubernetes&logoColor=white)
![Jenkins](https://img.shields.io/badge/Jenkins-D24939?style=for-the-badge&logo=jenkins&logoColor=white)
![Terraform](https://img.shields.io/badge/Terraform-7B42BC?style=for-the-badge&logo=terraform&logoColor=white)
![AWS](https://img.shields.io/badge/AWS-232F3E?style=for-the-badge&logo=amazon-aws&logoColor=white)

---

[![LinkedIn](https://img.shields.io/badge/LinkedIn-0077B5?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/senopaul/)
[![GitHub](https://img.shields.io/badge/GitHub-100000?style=for-the-badge&logo=github&logoColor=white)](https://github.com/senopaul)
