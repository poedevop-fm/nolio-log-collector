#Ansible Playbook to collect logs, configs and jmx data for NAC, NES and Agents 

### PreRequisite

[Ansible hello world tutorials](http://www.sanjeevnandam.com/blog/ansible-hello-world)

Specify each servers in the hosts file. If you have an agent installed in execution server, you may have to specify the instance twice. Once as a NES and once as agent

ansible-playbook -i hosts_5.5.1_LAB site.yml -v --ask-sudo-pass

### Features
1. Organize each server type by it's role. Same server can be defined in two different roles. For example a NES can also be listed as an agent
2. Specify fetch location in the master ansible server and temp location in the target nodes to store the logs
 * group_vars/all/{temp_location}
 * group_vars/all/{fetch_location}
3. Specify the location of the service
  * group_vars/agents/{nolio_agent_service}
  * group_vars/mgmt_server/{nolio_ASAP_service}
  * group_vars/execution_servers/{nolio_ASAP_service}
4. Specify the version
  * group_vars/mgmt_server/{nolio_version}
5. Collect logs and conf folder from each server type
 * group_vars/all/{collect_logs}
 * NAC
     * Run Kill -3 command three times to catch the exception in catalina.out file
     * Run top command three times to find running processes
     * Collect the threadDump and memoryDump
     * Copy conf folder
     * Copy logs folder
 * NES and Agents
     * Copy conf folder
     * Copy logs folder
6. Update logging levels (Make sure you have sufficient disk space before applying change)
 * group_vars/all/{update_logging} and group_vars/all/{log_file_count}
 * restart_services should be set to "true" when you are ready to restart the services for the change to take effect
7. Ability to restart the services
 * group_vars/all/{restart_services}
8. To cleanup temporary files 
 * logs, files_temp, files_cache, files_registry
