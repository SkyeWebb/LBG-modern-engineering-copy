# ![](https://ga-dash.s3.amazonaws.com/production/assets/logo-9f88ae6c9c3871690e33280fcf557f33.png) Ansible

| Title   | Type | Duration | Author    |
| ------- | ---- | -------- | --------- |
| Ansible | Lab  | 0:30     | Ben Piper |

- [ Ansible](#-ansible)
  - [Install Ansible](#install-ansible)
  - [Install the Visual Studio Code Ansible extension from Red Hat](#install-the-visual-studio-code-ansible-extension-from-red-hat)
  - [Review the playbook](#review-the-playbook)
  - [Run the playbook](#run-the-playbook)
  - [Stretch goal](#stretch-goal)

The goal of this lab is to learn how to use Ansible to install some utilities we'll be using in upcoming labs. Some of these utilities include:

- The AWS CLI
- Terraform

## Install Ansible

Open up your terminal and type the following:

```
sudo amazon-linux-extras install epel -y
sudo yum -y install ansible
```

Verify the version by typing:

```
ansible --version
```

Ensure the version is 2.9.27 or later.

## Install the Visual Studio Code Ansible extension from Red Hat

Open up VS Code.

In VS Code, type Ctrl+P (PS) or Command+P (Mac), and enter `ext install redhat.ansible`.

Close VS Code and reopen it.

## Review the playbook

Load [playbook.yml](playbook.yml) in VS Code.

The playbook installs several tools you'll use throughout the labs, including:

- The AWS command line interface (CLI)
- Terraform

Refer to the [syntax documentation](https://docs.ansible.com/ansible/latest/playbook_guide/playbooks_intro.html#playbook-syntax) and the [plugin documentation](https://docs.ansible.com/ansible/latest/collections/ansible/builtin/index.html#plugins-in-ansible-builtin) to understand what the playbook will do when executed.

## Run the playbook

You must run this playbook from the repo that you cloned earlier so ensure you are inside lab-00 directory:

```
cd <path to the week3_lesson2/02-ansible directory>

ansible-playbook playbook.yml
```

## Stretch goal

Try to think of some other things you can add to the playbook, such as installing additional packages or creating a file.

Implement your ideas in the playbook, then try running it again using `ansible-playbook playbook.yml`.
