#Ansible Playbook to collect logs, configs and jmx data for NAC, NES and Agents 

### PreRequisite

[Ansible hello world tutorials](http://www.sanjeevnandam.com/blog/ansible-hello-world)

Specify each servers in the hosts file. If you have an agent installed in execution server, you may have to specify the instance twice. Once as a NES and once as agent

ansible-playbook -i hosts_5.5.1_LAB site.yml -v --ask-sudo-pass