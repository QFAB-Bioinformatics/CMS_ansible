# CMS_ansible
Ansible deployment for Cromwell/MySQL/SLURM stack on Debian based systems.

# Setup
To install Ansible, it is highly recommended to use a virtual environment. The easiest way to do so is via Conda. Install [Conda](https://conda.io/docs/user-guide/install/index.html), and then create a new environment for Ansible with:
    
    conda create -n ansible -c conda-forge ansible

Once installed, you can load the environment using:

    source activate ansible

This ansible repo uses several DebOps roles available on Ansible Galaxy.
Install the dependencies with the following command:

    ansible-galaxy install --force -r requirements.yml

This repo also uses Ansible Vault to manage all the private variables (passwords, keys e.g.). Human readable versions of these variables are included in the plain text vars files, sourcing from the vault files as per [best practices](https://docs.ansible.com/ansible/latest/playbooks_best_practices.html#variables-and-vaults). It is recommended to use this structure for your own vault files. Instructions for creating, viewing and editing vault files can be found [here](https://docs.ansible.com/ansible/2.4/vault.html).

# Usage
Playbooks are in the `playbooks` directory. Run them as follows:

    ansible-playbook -i inventory/hosts playbooks/{{ playbook }}.yml --ask-vault-pass

Ansible uses the `ssh-agent` to connect to remote machines. If connecting with SSH keys, load them into the agent with:

    ssh-add {{ ssh key }}

If using username/password logins to connect, add `--ask-pass` to the `ansible-playbook` command to trigger it to prompt for a password:

    ansible-playbook -i inventory/hosts playbooks/{{ playbook }}.yml --ask-vault-pass --ask-pass

## Current playbooks
| Filename      | Description |
| --------      | ----------- |
| cms_stack.yml | Generic Cromwell/MySQL/SLURM provisioning of hosts in the cms group   |

## Current roles
| Name      | Description |
| --------      | ----------- |
| common | Common tasks, e.g. security hardening, user management, system updates, environment setup    |
| cms | Installs each of the components in the CMS stack and configures them accourdingly   |


### Authors
Thom Cuddihy, QFAB