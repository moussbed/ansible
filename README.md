#### Ad hoc commands 

```bash
  $ ansible all -i inventory -m ping
  $ ansible droplet -i inventory -m ping
  $ ansible 167.99.128.151 -i inventory -m ping
```

#### Disable host key checking 
This deactivation is useful when we have ephemeral servers that are created or deleted frequently 
Create a file .ansible.cfg and put this content : 
[defaults]
host_key_checking = False

```bash
  $ vim ~/.ansible.cfg
```  
or we can create it for a specific projet. In this case we touch ansible.cfg file in the root projet.

#### Launch playbook 

```bash
   $ ansible-playbook -i inventory  playbook.yaml
```

#### How to find the version of package 
https://launchpad.net/ubuntu

#### How to find ansible module
https://docs.ansible.com/ansible/2.9/modules/modules_by_category.html

#### Using collections 
https://docs.ansible.com/ansible/2.9/user_guide/collections_using.html
https://docs.ansible.com/ansible/latest/collections/index.html
Collections are a distribution format for Ansible content that can include playbooks, roles, modules, and plugins. You can install and use collections through Ansible Galaxy.

#### Ansible Galaxy
Ansible galaxy is the online hub for finding and sharing Ansible community content like collections.
We can type this command to list collections on local environment:

```bash
   $ ansible-galaxy collection list
```
How do we install collections ? In this case for instance AWS

```bash
   $ ansible-galaxy collection install amazon.aws
```

#### Notice 
shell and command module ignore current state.
They are not idempotent. You have to manage them yourself in using for instance condition with 'when' 

#### Why do we use all
Because in terraform we specfic ip comming from instance created 

 provisioner "local_exec" {
      working_dir = "where ansible project is located"
      command = "ansible-playbook --inventory ${self.public_ip}, --private-key ${var.ssh_private_key} --user ec2-user deploy-docker.yaml"
}

#### Use aws_ec2 plugin  to get infrastructure info

##### Requirements

- boto3
- botocore  

```bash
 $ ansible-inventory -i inventory_aws_ec2.yaml --list
 or 
 $ ansible-inventory -i inventory_aws_ec2.yaml --grap # return list of ec2 instances running
 @all:
  |--@aws_ec2:
  |  |--ec2-18-116-28-84.us-east-2.compute.amazonaws.com
  |  |--ec2-18-117-93-152.us-east-2.compute.amazonaws.com
  |  |--ec2-3-17-110-123.us-east-2.compute.amazonaws.com
  |--@ungrouped:
```
Use now aws_ec2 like hosts in your ansible configuration

#### Launch ansible-playbook with dynamic inventory 

```bash
    $ ansible-playbook -i inventory_aws_ec2.yaml deploy-docker.yaml
    or 
    $ ansible-playbook deploy-docker.yaml # if set inventory with inventory_aws_ec2.yaml in the ansible.cfg
```

#### k8s 

##### Requirements
The below requirements are needed on the host that executes this module.

- python >= 3.6
- kubernetes >= 12.0.0
- PyYAML >= 3.11
- jsonpatch

 
##### kubeconfig paramater:
Path to an existing Kubernetes config file. If not provided, and no other connection options are provided, the Kubernetes client will attempt to load the default configuration file from ~/.kube/config. Can also be specified via K8S_AUTH_KUBECONFIG environment variable.
The kubernetes configuration can be provided as dictionary. This feature requires a python kubernetes client version >= 17.17.0. Added in version 2.2.0.
Before that we have to connect to our cluster with kubectl with this command:

```bash
   $ aws eks update-kubeconfig --name myapp-eks-cluster --region us-east-2
```








