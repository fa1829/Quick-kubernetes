
# Roles

These roles are called from their corresponding **playbook**. both of them have a similar directory structure that goes:

role_dir/
|_files/ 
|_tasks/
|_vars/

### Directory Structure Explanation
 
#### Files Directory
`files/` : You should put static files that are needed for configuration purposes and are always going to be the same. You should also use a similar directory structure as in the OS. 
##### For example: 
  role/files/
  |_etc/
  |__defaults/
  |___kubelet.conf

The `role/files/etc/defaults/kubelet.conf` is the configuration file for the kubelet service that is located in `/etc/deafults/kubelet.conf` inside the provisioned node.

#### Tasks Directory
`tasks/` :  Here lies the tasks that ansible will perform for the configuration of the node. Ansible by default looks inside the `tasks/` dir for the `main.yaml` file and executes the configuration inside it.
##### For example: 
  role/tasks/
  | main.yaml
  | additional_config.yaml (referenced in the main.yaml file)

***Note:** You can have different configuration files inside the `tasks/` dir, but you need to reference said files in the `main.yaml` file.*

#### Vars Directory
`vars/` :  Here lies the variables that ansible will use when performing for the configuration of the node, which are referenced inside the `tasks/` dir. Ansible by default looks inside the `vars/` dir for the `main.yaml` file and gets the values of the variables from inside it.
##### For example: 
  role/vars/
  | main.yaml
  | additional_vars.yaml (referenced in the main.yaml file)

***Note:** You can have different variables files inside the `vars/` dir, but you need to reference said files in the `main.yaml` file.*

## Master Role

Configures the `k8s-master` node which will be the orchestrator for the other nodes that will be configured in the **Node Role**.

## Node Role

Configures the `k8s-node-*` nodes which will be the workers for the  `k8s-master` node.