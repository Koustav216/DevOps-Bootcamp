## Brief
Here, we have two ec2 instances. In one of those, we shall install **ansible**, and perform various tasks in the other instance using **ansible** .

[Ansible Docs](https://docs.ansible.com/ansible/latest/getting_started/index.html)

## Installation in Ubuntu

```
sudo apt update
sudo apt install ansible
```

## Ansible Playbook
A script written in Bash is called Bash Script. A script written in Python is called Python Script. Similarly, a file containing Ansible script in YAML is called Ansible Playbook. Playbooks are reusable and can be version-controlled.

## Ansible Adhoc Commands
If we need to run some basic commands say, `ls` or `echo hello world`, we don't create a bash file for it. Similarly, for simple tasks, we need not write Ansible Playbooks, we can directly run Ansible CLI commands. Such commands are called [ad-hoc commands](https://docs.ansible.com/ansible/latest/command_guide/intro_adhoc.html) .

Default syntax to write ad-hoc command is as follows:
```bash
ansible -i path-to-inventory-file host_pattern -m module -a args 
```
The targeted **host** must reside in the provided inventory file.

## Inventory File

To get started with Ansible, first, we need to create an inventory file. An inventory is a single file with a list of hosts and groups. It is generally structured in INI or YAML format.

The default inventory file is `/etc/ansible/hosts`. We can use it, but, for convenience, we can also specify a different inventory file at the command line using the `-i <path>` option.

e.g., 
- First we create an inventory file in current working dir: `touch inventory`

- we specify hosts in it, as we need to specify the user for logging in.
- `ansible_host` — tells Ansible which network address to connect to for that host (IP or FQDN).
- `ansible_user` — tells Ansible which remote user to use when establishing the connection. By default, Ansible tries to connect with the username we are using on the control node.

  ```bash
  # inventory file: inventory.ini (INI format)

  # explicit syntax
  ansible_host=10.38.23.212 ansible_user=ubuntu
  ansible_host=10.38.24.215 ansible_user=harry
  
  # or, using shorthand syntax (not recommended for real usage)
  ubuntu@10.38.23.212
  harry@10.38.24.215
  ```

- now, we execute an ad-hoc command: ` ansible -i ./inventory.ini all -m 'shell' -a 'touch testFile.txt' `.

  - **all** is a pattern specifying all the hosts in **inventory** , i.e. the command will execute for all of the hosts. For details, check [patterns](https://docs.ansible.com/ansible/latest/inventory_guide/intro_patterns.html#intro-patterns).

  - Instead of **all**, we can also specify a single host, like: ` ansible -i ./inventory.ini w.x.y.z -m 'shell' -a 'touch testFile.txt' `. But the host must reside in **inventory** .

- **-m** flag is used to specify module (As we use shell command, we use 'shell'). This module is responsible for execution of any assigned task. To listing all the modules use `ansible-doc -l`. The default module for the ansible command-line utility is the `command` module. For details, check [all modules](https://docs.ansible.com/ansible/2.9/modules/list_of_all_modules.html).

- **-a** flag is used to specify the argument/command.

Learn more about connection variables (e.g. `ansible_host`, `ansible_user`) from the  [docs](https://docs.ansible.com/ansible/latest/inventory_guide/intro_inventory.html#connecting-to-hosts-behavioral-inventory-parameters)

### Small Diagnostics

- See what Ansible will connect to and with what vars for a specific host. Use `--list` flag (with no args) instead to get info about all hosts:
  ```bash
  ansible-inventory -i inventory --host web1
  ```
- Confirm connection and the user (quick "whoami" test):
  ```bash
  ansible web1 -i inventory -m command -a "whoami"
  ```
- Show gathered facts and verify connectivity (useful to confirm SSH):
  ```bash
  ansible web1 -i inventory -m setup
  ```

## Grouping hosts in Inventory
To perform actions on a particular set of hosts, we create groups in inventory file.

e.g., here we have two hosts under **dbservers** group and one host under **webservers** group.
```bash
  # inventory file: inventory.ini (INI format)
  
  [dbservers]
  a.b.c.d
  e.f.g.h
  [webservers]
  w.x.y.z

```

Now, we can run a command for all the hosts under a particular group (here, **webservers**),

`ansible -i ./inventory.ini webservers -m 'shell' -a 'touch hello.html'`

Learn about [Grouping groups](https://docs.ansible.com/ansible/latest/inventory_guide/intro_inventory.html#grouping-groups-parent-child-group-relationships)

## Write Playbook
A playbook consists of one or more ‘plays’ in an ordered list. Each play executes part of the overall goal of the playbook, running one or more tasks. A playbook runs in order from top to bottom. Within each play, tasks also run in order from top to bottom.

In the following playbook, we install nginx and start nginx.

- First, we need to create an yaml file, say *playbook.yml* . 


  ```yaml
  ---  # This indicates the start of a playbook

  - name: Install and Start Nginx  # we can give any name to the play

    hosts: all  # execute the play for all hosts in inventory

    become: true # for using root privileges

    tasks: # now we specify tasks to be performed

    - name: Install nginx   # we can give any name to the task
      apt:    # we want to use the apt module
	      name: nginx   # name of the package
        state: present # to install nginx

    - name: Start nginx  # this is the name our second task
      service:  # we want to use service module
        name: nginx  # we are interested about nginx service
        state: started  # to start the service

  # we can write multiple plays in single file as shown

  - name: Second play
    [...]

  ```

- Now, we execute this playbook in the main server using **ansible-playbook** command:

  `ansible-playbook -i ./inventory.ini playbook.yml`

In the managed node,
- Check the status of nginx by `systemctl status nginx`

- Stop nginx by `sudo systemctl stop nginx`.

### Privilege Escalation

```yaml
become: yes
```
is shorthand for:

```yaml
become: yes
become_user: root  # Who to become (default is root)
become_method: sudo # How to become (sudo, su, pbrun, doas, etc.)
become_flags: "" # Extra options passed to the become_method command; none by default 
```
If we write
```yaml
become: yes
become_method: su
```
the final effective settings are:
```yaml
become: yes

become_method: su # ← we overrode this

become_user: root # ← still default (not reset)

become_flags: "" # ← still default
```

Learn more about it [here](https://docs.ansible.com/ansible/latest/playbook_guide/playbooks_privilege_escalation.html#become)







 
