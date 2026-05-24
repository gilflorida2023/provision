# Ansible Provisioning

Infrastructure automation for managing multiple Linux hosts.

## Inventory

- `inventory.yml` - Hosts: scout (control), ryzen, speedy, fast

## Playbooks

### Installation Playbooks

| Playbook | Description | Command |
|----------|-------------|---------|
| `install_ollama.yml` | Install/update Ollama LLM runtime with AMD ROCm GPU support. Downloads to control node, then deploys to managed nodes. | `ansible-playbook -i inventory.yml install_ollama.yml --ask-become-pass` |
| `basic_packages.yml` | Install git, htop, terminator, vim, gawk, jq, vlc, xclip, rustc | `ansible-playbook -i inventory.yml basic_packages.yml --ask-become-pass` |
| `install_brave.yml` | Install Brave Origin (beta/nightly). Channel controlled by `brave_channel` variable. | `ansible-playbook -i inventory.yml install_brave.yml --ask-become-pass` |
| `install_docker.yml` | Install Docker and Docker Compose | `ansible-playbook -i inventory.yml install_docker.yml --ask-become-pass` |
| `install_newsboat.yml` | Install Newsboat RSS reader | `ansible-playbook -i inventory.yml install_newsboat.yml --ask-become-pass` |
| `install_vagrant.yml` | Install Vagrant | `ansible-playbook -i inventory.yml install_vagrant.yml --ask-become-pass` |
| `install_virtualbox.yml` | Install VirtualBox | `ansible-playbook -i inventory.yml install_virtualbox.yml --ask-become-pass` |
| `install_vscode.yml` | Install Visual Studio Code | `ansible-playbook -i inventory.yml install_vscode.yml --ask-become-pass` |
| `install_yt-dlp.yml` | Install yt-dlp video downloader | `ansible-playbook -i inventory.yml install_yt-dlp.yml --ask-become-pass` |
| `install_moosefs.yml` | Install MooseFS distributed filesystem (deprecated) | `ansible-playbook -i inventory.yml install_moosefs.yml --ask-become-pass` |

> **Brave Origin channels**: `-e brave_channel=beta` (default) or `-e brave_channel=nightly`. Installs via direct `.deb` from GitHub releases — no APT repo added.

### Configuration Playbooks

| Playbook | Description | Command |
|----------|-------------|---------|
| `configure_ufw.yml` | Configure UFW firewall rules based on inventory | `ansible-playbook -i inventory.yml configure_ufw.yml --ask-become-pass` |
| `git_config.yml` | Configure git settings | `ansible-playbook -i inventory.yml git_config.yml --ask-become-pass` |
| `setup_pass.yml` | Setup pass password manager | `ansible-playbook -i inventory.yml setup_pass.yml --ask-become-pass` |

### Utility Playbooks

| Playbook | Description | Command |
|----------|-------------|---------|
| `check_ufw_config.yml` | Display UFW firewall configuration | `ansible-playbook -i inventory.yml check_ufw_config.yml --ask-become-pass` |
| `report_host.yml` | Generate inxi system report and write to reports/ directory | `ansible-playbook -i inventory.yml report_host.yml --ask-become-pass` |
| `update_system.yml` | Update system packages | `ansible-playbook -i inventory.yml update_system.yml --ask-become-pass` |
| `update_ollama_llms.yml` | Update LLM models within Ollama | `ansible-playbook -i inventory.yml update_ollama_llms.yml --ask-become-pass` |

### Key Management Playbooks

| Playbook | Description | Command |
|----------|-------------|---------|
| `create_authorized_keys.yml` | Create authorized_keys file in reports/ directory | `ansible-playbook -i inventory.yml create_authorized_keys.yml --ask-become-pass` |
| `push_authorized_keys.yml` | Push authorized_keys to managed nodes | `ansible-playbook -i inventory.yml push_authorized_keys.yml --ask-become-pass` |

### Project Setup

| Playbook | Description | Command |
|----------|-------------|---------|
| `setup_projects.yaml` | Setup project directories | `ansible-playbook -i inventory.yml setup_projects.yaml --ask-become-pass` |

## Usage

Run a playbook on all hosts:
```bash
ansible-playbook -i inventory.yml <playbook>.yml --ask-become-pass
```

Run on specific host(s):
```bash
ansible-playbook -i inventory.yml <playbook>.yml --limit hostname --ask-become-pass
```

Verbose output:
```bash
ansible-playbook -i inventory.yml <playbook>.yml --ask-become-pass -v
```