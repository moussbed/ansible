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





