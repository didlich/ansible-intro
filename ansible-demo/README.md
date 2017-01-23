# This repo contains all the resource and instructions to create a jenkins VM in azure and provision the VM. The setup is performed using ansible provisioning tool.

## Ansible Vault
For further information see: [Ansible Vault Doc](http://docs.ansible.com/ansible/playbooks_vault.html)

You need this, because credentials which are used in tasks are encrypted, at least the 
**group_vars/all/secrets.yml**. You can edit the vars by:

    ansible-vault edit group_vars/all/secrets.yml

You can create the password file by:

    echo "YOUR_PASSWORD" > ~/.ansible_vault_pass.txt
    chmod 0600 ~/.ansible_vault_pass.txt
    echo "export ANSIBLE_VAULT_PASSWORD_FILE=${HOME}/.ansible_vault_pass.txt" > /etc/profile.d/ansible-vault-pass.sh
    source /etc/profile.d/ansible-vault-pass.sh

# Ansible Setup 

see the tutorial for setup and the first steps: [ansible-tutorial](https://serversforhackers.com/an-ansible-tutorial)

for use with ubuntu:

    sudo apt-get install python-pip

    sudo apt-add-repository -y ppa:ansible/ansible
    sudo apt-get update
    sudo apt-get install -y ansible

## Ping test

for the first test you can execute:

    ansible wildfly -i hosts --private-key=~/.ssh/id_rs -m ping

this command uses the [inventory](http://docs.ansible.com/ansible/intro_inventory.html) 
file "hosts" to connect to other hosts and the module "ping" to ping a host

the result should look like this:

    localhost | SUCCESS => {
      "changed": false, 
      "ping": "pong"
    }

## Install dependencies

command to install roles from a requirements file

    ansible-galaxy install --roles-path ./library -r requirements.yml

command to install python dependencies:

    pip install -r requirements.txt


# Playbooks

## Wildfly

    ansible-playbook wildfly.yml -i hosts -t java --key-file=~/.ssh/id_rs