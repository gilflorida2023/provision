

###  install ollama to machine3
	ansible-playbook -i inventory.yml install_ollama.yml --limit machine3 --ask-become-pass -vvv
###  install ollama to machine1,machine2
	ansible-playbook -i inventory.yml install_ollama.yml --limit machine1,machine2 --ask-become-pass 
### invoke a shell command with ansible
	ansible all -i inventory.yml -m shell -a "cat /proc/loadavg"
## machine3 | CHANGED | rc=0 >>
## 1.56 1.78 1.51 1/939 6522
## machine1 | CHANGED | rc=0 >>
## 0.00 0.00 0.00 1/422 1500590
## machine2 | CHANGED | rc=0 >>
## 0.00 0.00 0.00 1/305 10643



##  Check cpu types
	ansible-playbook -i inventory.yml report_cpu.yml --limit machine1,machine2 

## PLAY [Get detailed CPU information from /proc/cpuinfo] ************************************************************
## 
## TASK [Read and parse /proc/cpuinfo] *******************************************************************************
## ok: [machine1]
## ok: [machine2]
## 
## TASK [Display detailed CPU information] ***************************************************************************
## ok: [machine1] => {
##     "msg": [
##         "Host: machine1",
##         "Processor Vendor: AuthenticAMD",
##         "Processor Model: AMD Ryzen 5 PRO 5650GE with Radeon Graphics",
##         "Physical Cores: 6",
##         "vCPUs/Threads: 12",
##         "CPU Family: 25",
##         "CPU Model Number: 80",
##         "CPU Stepping: 0",
##         "Cache Size: 512 KB"
##     ]
## }
## ok: [machine2] => {
##     "msg": [
##         "Host: machine2",
##         "Processor Vendor: AuthenticAMD",
##         "Processor Model: AMD Ryzen 5 PRO 8500GE w/ Radeon 740M Graphics",
##         "Physical Cores: 6",
##         "vCPUs/Threads: 12",
##         "CPU Family: 25",
##         "CPU Model Number: 120",
##         "CPU Stepping: 0",
##         "Cache Size: 1024 KB"
##     ]
## }
## 
