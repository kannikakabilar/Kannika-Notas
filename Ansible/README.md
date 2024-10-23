What is Ansible?

A tool that automates IT tasks - configuration management system. It allows to execute tasks from your own machine instead of ssh'ing into each remote servers to perform the same tasks

Tasks that can automated using Ansible
- create user
- assign groups, update persmissions
- system reboots

- Configuration/Installation/Deployment steps can be setup in a single YAML file instead of shell script, and terminal commands performed manually
- Re-use same files for different environments 

Support
- os level updates
- cloud level updates (AWS, Azure)

Ansible is agentless
- You just need ssh access to all the remote servers and have Ansible installed in your local machine, which will act as the control machine. [no need to install Ansible in the remote servers] => no update or deployment of ansible versions need to be concerned

Ansible Architecture
modules (small tasks) get pushed to the remote servers - they do their specified task and then gets removed

module = one small specific task (ie: 
	- create a file
	- rename db table name
	- start docker container
	- install/start nginx server)
On using Python programing, Ansible helps in allowing users to create their own custom modules.

```yml
- hosts: database
  remote_user: root

  tasks:
    - name: Task1 Name
      base_module:
	arg1: val1
	arg2: val2
```

Play = which task should be executed on which host using which user

Playbook = 1 or more plays - you can have multiple plays in 1 *.yaml file

```yml
- name: Add container to networks
    docker_container:
        name: sleepy
        networks:
            - name: TestingNet
              ipv4_address: 172.1.1.18
              links:
                  - sleeper
            - name: TestingNet2
              ipv4_address: 172.1.10.20
```

Ansible inventory list contains the ip_addresses/hostname of the host where the tasks get executed - this is located in Hosts file

By default, Ansible looks for an inventory file at /etc/ansible/hosts

[database]
10.24.0.1
10.24.0.2

[webservers]
10.24.0.7
10.24.0.8

[webservers2]
web1.myserver.com
web2.myserver.com

Grouping multiple servers here like this can help execute the same tasks in many servers at the same time

Usage in Playbooks: When you run a playbook, you specify the inventory file (if it’s not the default) and the playbook file. For example:

[command line or bash]

ansible-playbook -i my_inventory_file hosts playbook.yml


Ansible playbook can be used to manage the storeage of the host as well as the Docker container which docker alone cannot do

Ansible Tower
- An UI dashboard from RedHat
- A place to centrally store automation tasks across teams
- Configure permissions and manage inventory

**Shell Environment Variables**

- you can lookup

```yml
- name: Get an environment variable
  debug:
    msg: "The value of MY_VAR is {{ lookup('env', 'MY_VAR') }}"
```

- using ansible_env
Ansible automatically populates the ansible_env variable with all the environment variables available to the Ansible process

```yml
- name: Print a specific environment variable
  debug:
    msg: "The value of MY_VAR is {{ ansible_env.MY_VAR }}"
```

- can access it in the bash shell with base shell module

```yml
- name: Run a shell command that uses an environment variable
  shell: "echo $MY_VAR"
```

**Accessing a Variable**

```yml
---
- hosts: localhost
  vars:
    my_variable: "Hello, Ansible!"
    my_dict:
      key_name: "This is a dictionary value"

  tasks:
    - name: Print a simple variable
      debug:
        msg: "The value of my_variable is {{ my_variable }}"

    - name: Print a dictionary variable
      debug:
        msg: "The value is {{ my_dict.key_name }}"
```

**Copying files recursively in Ansible**

```yml
- hosts: target_host
  tasks:
    - name: Copy files recursively to target host
      copy:
        src: /path/to/source/directory/  # Trailing slash indicates contents - tells Ansible to copy the contents of the directory rather than the directory itself
        dest: /path/to/destination/directory/
        recursive: yes
```

comments: copy module is idempotent, meaning that running the same playbook multiple times will not result in additional copies unless there are changes in the source files

**Adhoc Commands**

In Ansible, ad-hoc commands are one-off commands that allow you to perform simple tasks on remote hosts without the need to write a full playbook.

ansible [host-pattern] -m [module] -a "[module options]"

ping hosts: ansible all -m ping
run shell cmd: ansible webservers -m shell -a "uname -a"
copy a file: ansible appservers -m copy -a "src=/local/path/file.txt dest=/remote/path/"
install a pkg: ansible all -m yum -a "name=httpd state=present"

**Ansible Facts**

Accessing Facts: Facts can be accessed using the ansible_facts variable. For example, to access the operating system name, you would use ansible_facts['os_family'].

Custom Facts: You can define custom facts by placing scripts in specific directories on the target host, such as /etc/ansible/facts.d/. These scripts should return JSON data and can be used to extend the default facts collected by Ansible.

```yml
---
- hosts: all
  tasks:
    - name: Gather facts
      setup:

    - name: Print the operating system
      debug:
        msg: "The operating system is {{ ansible_facts['os'] }}"

    - name: Print memory information
      debug:
        msg: "Total RAM: {{ ansible_facts['memtotal_mb'] }} MB"

    - name: Print network interfaces
      debug:
        msg: "Network interfaces: {{ ansible_facts['interfaces'] }}"
```

ansible_facts['distribution']: The name of the Linux distribution (e.g., Ubuntu, CentOS).
ansible_facts['os_family']: The family of the operating system (e.g., Debian, RedHat).
ansible_facts['architecture']: The system architecture (e.g., x86_64).
ansible_facts['hostname']: The hostname of the target machine.
ansible_facts['ip_addresses']: List of IP addresses assigned to the host.
ansible_facts['memtotal_mb']: Total memory in megabytes.

**How to see all variables for a host**

ansible -m debug -a "var=hostvars[inventory_hostname]"

**Create Empty file in hosts module**

```yml
---
- hosts: all
  tasks:
    - name: Create an empty file using the command module
      command: touch /path/to/your/file.txt
```

**Ansible Galaxy** is a platform providing the features of sharing and downloading Ansible roles.

**plugins** are reusable components that extend Ansible's functionality. They allow users to customize and enhance how Ansible operates without modifying the core code.

```yml
- hosts: localhost
  tasks:
    - name: Read a password from a file
      debug:
        msg: "The password is {{ lookup('file', 'path/to/password.txt') }}"
```

**Callback plugins** are used for logging, notifications, or any post-playbook actions.

**Handlers**

Handlers in Ansible are tasks that are triggered by other tasks, usually used to respond for the changes that require start , stop , reload or restart the service actions. They are defined in the playbook and executed as per need.

```yml
---
- hosts: webservers
  tasks:
    - name: Install nginx
      apt:
        name: nginx
        state: present
      notify: restart nginx  # Notify the handler to restart nginx if this task changes

    - name: Copy nginx configuration file
      copy:
        src: /path/to/nginx.conf
        dest: /etc/nginx/nginx.conf
      notify: restart nginx  # Notify the handler to restart nginx if this task changes

  handlers:
    - name: restart nginx
      service:
        name: nginx
        state: restarted
```


**Ansible Vault** provides a secured way for encrypting sensitive data such as passwords, so that they can be stored safely for usage in your playbooks

ansible-vault encrypt_string --vault-id @prompt --name 'ansible_become_pass' 'mypassword'

**Installing something using Ansible**

```yml
- name: Install Nginx
   hosts: web_servers
   become: true  # To execute tasks with sudo privileges
   tasks:
   - name: Update package cache
      apt:
        update_cache: yes  # For Ubuntu/Debian systems
   - name: Install Nginx
      apt:
        name: nginx
        state: present
   - name: Start Nginx service
      service:
        name: nginx
        state: started
        enabled: yes  # Ensures Nginx starts on boot
```

**Looping over a list of Hosts**

In Ansible playbooks, you can implement looping over a list of hosts in a group using the with_items directive or the loop keyword in tasks. This is useful for performing actions on multiple hosts within a specific group.

```yml
---
- hosts: webservers
  tasks:
    - name: Ensure a package is installed
      apt:
        name: "{{ item }}"
        state: present
      loop:
        - nginx
        - git
        - curl
```

loop/with_items: This keyword is used to iterate over the list of packages. Ansible will execute the task for each item in the list.

**Ansible registry** is a mechanism to store variables persistently, enabling data to be passed between different parts of a playbook or even between plays.

Management inside EC2 can be accelerated by leveraging dynamic EC2 inventory scripts. These scripts automatically fetch information about EC2 instances, ensuring dynamic and efficient management of hosts in an Ansible environment.

**Top 20 commonly used modules**

- apt - Manages packages for Debian-based systems.
- yum - Manages packages for Red Hat-based systems.
- copy - Copies files from the control machine to the target hosts.
- template - Jinja2 template processing for files.
- file - Manages file attributes (permissions, ownership, etc.).
- service - Manages services (start, stop, restart, enable).
- command - Executes commands on remote hosts.
- shell - Executes shell commands on remote hosts.
- git - Manages git repositories.
- user - Manages user accounts and groups.
- group - Manages groups on the target hosts.
- lineinfile - Manages lines in text files.
- cron - Manages cron jobs.
- wait_for - Waits for a condition before proceeding.
- synchronize - Synchronizes files between the control machine and remote hosts.
- blockinfile - Manages block of multi-line text in files.
- get_url - Downloads files from URLs to remote machines.
- fetch - Retrieves files from remote machines to the control machine.
- debug - Prints statements during playbook execution for debugging.
- setup - Gathers facts about remote hosts.
