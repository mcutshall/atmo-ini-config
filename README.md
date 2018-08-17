This plugin is currently designed to integrate with clank. Future plans are to replace the configure script for atmosphere-ansible and move all atmosphere-ansible templating into clank, along with this plugin. 

How it works:

This plugin creates database entries of completion times for ansible tasks. Each entry consistst of the task name and the time in seconds. The plugin creates a database named 'metrics' and consists of one table. 

The playbook for this plugin can be configured to profile any other ansible playbook, and is currently configured for 'instance_deploy'. The PLAYBOOK_TO_PROFILE variable in this playbook will create a 'callback_plugins' directory in the specified playbook to house the python and ini files. All variables for this plugin reside in defaults/main.yml. 

To run this plugin with clank the playbook and role must be added to clank/playbooks and clank/roles. Also, clank calls the deploy_stack.yml playbook to configure atmo and tropo, so a line must be added to this playbook. Add the line:  "include_playbook: ./setup_ansible_metrics.yml" to clank/playbooks/depoy_stack.yml. 

  1. Add setup_ansible_metrics.yml playbook to clank/playbooks
  2. Add configure-atmo-metrics role to clank/roles
  3. Add "include_playbook: ./setup_ansible_metrics.yml" to clank/playbooks/depoy_stack.yml

Once the deploy_stack finishes and the services are running, create a new instance and allow it to run until the 'deploying' phase, upon which database entries to the metrics db will be created. This is because we are profiling the 'instance_deploy' playbook, but will vary based on the specified playbook. 

This was developed using atmo-local: https://gitlab.cyverse.org/cutshall/atmo-local. 


TO DO: 

-Replace the configure script for atmosphere-ansible

-Move all atmosphere-ansible templating into clank

-Modify variables_templates.json to include the new plugin
