# OptiReduce Deployment 🚀

![Ansible](https://img.shields.io/badge/Ansible-EE0000?style=flat&logo=ansible&logoColor=white)
![License](https://img.shields.io/badge/License-MIT-blue)
![CUDA](https://img.shields.io/badge/CUDA-11.7-green)

This directory contains Ansible playbooks for deploying OptiReduce and its dependencies. For detailed information, visit our [official documentation](http://optireduce.github.io/).

---

## 📋 Table of Contents
- [📥 Download](#download)
- [🔑 Prerequisites](#prerequisites)
- [📂 Directory Structure](#directory-structure)
- [⚙️ Configuration](#configuration)
- [🚀 Deployment Options](#deployment-options)
- [🧩 Available Components](#available-components)
- [🌍 Environment Variables](#environment-variables)
- [⚠️ Troubleshooting](#common-issues-and-troubleshooting)
- [📚 Additional Resources](#additional-resources)
- [🆘 Support](#support)
- [📜 License](#license)

---

## 📥 Download
Clone the Ansible repository:
```bash
git clone https://github.com/OptiReduce/ansible.git
cd ansible
```

---

## 🔑 Prerequisites

### 1. Install Ansible
**Ubuntu/Debian**:
```bash
sudo apt update
sudo apt install software-properties-common
sudo apt-add-repository --yes --update ppa:ansible/ansible
sudo apt install ansible
```

**RHEL/CentOS**:
```bash
sudo yum install epel-release
sudo yum install ansible
```

Verify:
```bash
ansible --version
```

### 2. SSH Setup 🔐
#### SSH Installation Script
```bash
#!/bin/bash
sudo apt update && sudo apt install -y openssh-server
sudo systemctl enable ssh
sudo systemctl start ssh
sudo systemctl status ssh --no-pager
```

#### Password-less Authentication
```bash
#!/bin/bash
# Usage: ./ssh_setup.sh <user> <host>
if [ "$#" -ne 2 ]; then
    echo "Usage: $0 <target_username> <target_host>"
    exit 1
fi
TARGET_USER="$1"
TARGET_HOST="$2"
SSH_KEY="$HOME/.ssh/id_rsa"

[ ! -f "$SSH_KEY" ] && ssh-keygen -t rsa -b 4096 -N "" -f "$SSH_KEY"
ssh-copy-id "$TARGET_USER@$TARGET_HOST"
ssh -o BatchMode=yes "$TARGET_USER@$TARGET_HOST" "echo 'SSH success on $(hostname)!'"
```

---

## 📂 Directory Structure
```
optireduce/
├── ansible.cfg
├── inventory/
│   └── hosts
├── group_vars/
│   └── all.yml
├── optireduce_deploy.yml
├── Makefile
└── roles/
    ├── cuda/       # CUDA 11.7
    ├── mellanox/   # Mellanox OFED
    ├── anaconda/   # Python 3.9
    ├── optireduce/ # Core
    └── benchmark/  # Tests
```

---

## ⚙️ Configuration

### Inventory Setup (`inventory/hosts`)
```ini
[gpu_nodes]
node1 ansible_host=192.168.1.101 ansible_user=test
node2 ansible_host=192.168.1.102 ansible_user=test
```

### Variables (`group_vars/all.yml`)
```yaml
cuda_version: "11.7.0-1"
nvidia_version: "515"
cudnn_version: "8.5.0.96-1+cuda11.7"
python_version: "3.9.19"
dpdk_version: "v20.11"
```

---

## 🚀 Deployment Options

| Command                  | Description                          |
|--------------------------|--------------------------------------|
| `make optireduce-full`   | Full installation                    |
| `make cuda-only`         | Install CUDA only                    |
| `make benchmark-only`    | Install benchmarks                   |
| `make check`             | Validate configuration               |

---

## 🧩 Available Components
- **CUDA 11.7** with cuDNN 8.5
- **Mellanox OFED** Drivers
- **Anaconda** (Python 3.9.19)
- **DPDK v20.11**
- OptiReduce Core
- Benchmarking Tools

---

## 🌍 Environment Variables
```bash
# Toggle components during deployment
INSTALL_CUDA=true/false
INSTALL_MELLANOX=true/false
INSTALL_ANACONDA=true/false
INSTALL_OPTIREDUCE=true/false
INSTALL_BENCHMARK=true/false
```

---

## ⚠️ Troubleshooting
| Issue                     | Solution                              |
|---------------------------|---------------------------------------|
| **SSH Connection**        | Verify keys and network connectivity |
| **CUDA Failures**         | Check NVIDIA repo access and space   |
| **OFED Errors**           | Confirm kernel compatibility         |

---

## 📚 Additional Resources
- [OptiReduce Documentation](http://optireduce.github.io/)

---

## 🆘 Support
Open an issue in the [GitHub repository](https://github.com/OptiReduce/ansible/issues).

---

## 📜 License
This project is licensed under the MIT License. See the [project page](http://optireduce.github.io/) for details.
```

### Key Enhancements:
1. **Badges**: Added colorful badges for Ansible, CUDA, and License.
2. **Emojis**: Used emojis in headers for visual appeal.
3. **Syntax Highlighting**: All code blocks have language tags (e.g., `bash`, `yaml`).
4. **Tables**: Structured deployment options and troubleshooting as tables.
5. **Consistent Formatting**: Clear section separation with `---` lines.
6. **Directory Structure**: Added comments for clarity.

