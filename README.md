## Ansible for eventual system consistency :)
- basic_packages.yml - install basic packages : pass git htop terminator vim gawk jq vlc xclip rustc ufw
```
ansible-playbook -i inventory.yml  basic_packages.yml --limit machine1   --ask-become-pass -v
```

- check_ufw_config.yml - display ufw config on the specified hosts.
```
ansible-playbook -i inventory.yml  check_ufw_config.yml --limit machine1   --ask-become-pass -v
```

- configure_ufw.yml - setup ufw  firewall rules based on the inventory inventory.yml file
```
ansible-playbook -i inventory.yml  configure_ufw.yml --limit machine1   --ask-become-pass -v
ansible-playbook -i inventory.yml  configure_ufw.yml   --ask-become-pass -v
```

- install_docker.yml - install docker
```
ansible-playbook -i inventory.yml  install_docker.yml --limit machine1   --ask-become-pass -v
```

- install_moosefs.yml - Deprecated - install moosefs on each managed node 
```
ansible-playbook -i inventory.yml  install_moosefs.yml --limit machine1   --ask-become-pass -v
```

- install_newsboat.yml - installs newsboat. need to add  the config and urls file and integrte into this playbook.
```
ansible-playbook -i inventory.yml  install_newsboat.yml --limit machine1   --ask-become-pass -v
```

- install_ollama.yml - install latest and greatest ollama to specified hosts.
```
ansible-playbook -i inventory.yml  install_ollama.yml --limit machine1   --ask-become-pass -v
```

- install_vagrant.yml - install vagrant to specified hosts
```
ansible-playbook -i inventory.yml  install_vagrant.yml --limit machine1   --ask-become-pass -v
```

- install_virtualbox.yml - install virtualbox to specified hosts
```
ansible-playbook -i inventory.yml  install_virtualbox.yml --limit machine1   --ask-become-pass -v
```

- install_vscode.yml - install vscode
```
ansible-playbook -i inventory.yml  install_vscode.yml --limit machine1   --ask-become-pass -v
```

- install_yt-dlp.yml
```
ansible-playbook -i inventory.yml  install_yt-dlp.yml --limit machine1   --ask-become-pass -v
```

- inventory.yml - sample inventory file
```
---
all:
  hosts:
    machine1:
      ansible_host: 192.168.0.10
      ansible_user: machine1
      ansible_ssh_private_key_file: ~/.ssh/id_rsa
      ansible_python_interpreter: /usr/bin/python3
    machine2:
      ansible_host: 192.168.0.5
      ansible_user: machine2
      ansible_ssh_private_key_file: ~/.ssh/id_rsa
      ansible_python_interpreter: /usr/bin/python3
      is_control_host: true 
    machine3:
      ansible_host: 192.168.0.8
      ansible_user: machine3
      ansible_ssh_private_key_file: ~/.ssh/id_rsa
      ansible_python_interpreter: /usr/bin/python3
```

- create_authorized_keys.yml - Create an authorized_key file in the reports directory. - Not Idempotent
- push_authorized_keys.yml - call create and then push 
```
# do not limit create_authorized_keys.yml
ansible-playbook -i inventory.yml  create_authorized_keys.yml    --ask-become-pass -v
ansible-playbook -i inventory.yml  push_authorized_keys.yml --limit machine1,machine2   --ask-become-pass -v
```

- report_host.yml - gather info about specified host and write to local reports directory
```
ansible-playbook -i inventory.yml  report_host.yml --limit machine1 --ask-become-pass -v
```
- sample report from report_host.yml
```
$ cat reports/machine1_report.txt 
========================================
HOST: machine1
========================================
System:
  Kernel: 6.1.0-41-amd64 arch: x86_64 bits: 64
  Distro: LMDE 6 faye

Machine:
  Model: 11JN002AUS
  Serial: ZZZZZZZZ
  BIOS: M47KT28A (02/05/2023)

CPU:
  Model: AMD Ryzen 7 PRO 5750GE with Radeon Graphics
  Cores: 16 (SMT: enabled)
  Speed:   2730
 MHz (avg)

Memory:
  Total: 62.18 GiB
  Used: 33.51 GiB (53.9%)

Network:
        IF: enp2s0f1 state: down mac: FF:FF:FF:FF:FF:FF
            IF: wlp3s0 state: up mac: FF:FF:FF:FF:FF:FF
    IP: 192.168.0.5          IF: xxxxxxxxxxxxxxx state: down mac: FF:FF:FF:FF:FF:FF
      
Drives:
    /dev/mapper/lvmlmde-root (ext4) size: 1345.8 GiB
    Mount: / used: 464.82 GiB (34.5%)
    /dev/nvme0n1p1 (vfat) size: 0.28 GiB
    Mount: /boot/efi used: 0.01 GiB (2.0%)
  
Swap:
  Total: 62.18 GiB
  Used: 0.0 GiB

Uptime:         200d 11h  1m  5s
Processes: 372

Control Host: No

```

- setup_pass.yml - not sure yet
```
```

- update_ollama_llms.yml -update llms wthin ollama on specified host.
```
ansible-playbook -i inventory.yml  update_ollama_llms.yml --limit machine1,machine2   --ask-become-pass -v
```

- update_system.yml - update system
```
ansible-playbook -i inventory.yml  update_system.yml --limit machine1,machine2   --ask-become-pass -v
```
