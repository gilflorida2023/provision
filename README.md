

###  install ollama to machine3
	ansible-playbook -i inventory.yml install_ollama.yml --limit machine3 --ask-become-pass -vvv
###  install ollama to machine1,machine2
	ansible-playbook -i inventory.yml install_ollama.yml --limit machine1,machine2 --ask-become-pass 
### invoke a shell command with ansible
	ansible all -i inventory.yml -m shell -a "cat /proc/loadavg"
