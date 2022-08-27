# Ansible Labs with Most Common Modules

This repository contains ansible labs with necessary modules.

1. vars_prompt
2. Shell
3. Set fact
4. Register
5. Copy
6. Command and configuration
7. Vault
8. Facts and information
9. Template
10. URI




# 1. vars_prompt

If you want your playbook to prompt the user for certain input, add a ‘vars_prompt’ section. Prompting the user for variables lets you avoid recording sensitive data like passwords. In addition to security, prompts support flexibility. For example, if you use one playbook across multiple software releases, you could prompt for the particular release version.

```yml
---
- hosts: all
  vars_prompt:

    - name: username
      prompt: What is your username?
      private: no

    - name: password
      prompt: What is your password?

  tasks:

    - name: Print a message
      ansible.builtin.debug:
        msg: 'Logging in as {{ username }}'
        
```


## Another Example of var_prompt


```yml
---
- hosts: alpha
  vars:
  company: vogo
  tasks:
     - name: debugging
       debug:
         msg: "{{ansible_hostname}}"
  vars_prompt:
     - name: "company"
       prompt: "Where do you work"
       private: no

- hosts: webservers
  vars_prompt:
     - name: "fathercompany"
       prompt: "Where your father works"
       private: no
  tasks:
     - name: test
       debug:
         msg: just testing "{{company2}}"

```




# 2. shell 
We can run the commands on `ad-hoc` as well as using the module inside the `playbook`

## a. Example of shell Command using an `ad-hoc` method

Ansible shell module can run a single command on a remote host. To do this, a one-line command on your Ansible controller will work. For example, let’s run a simple command on a remote host to print the PATH environment variable‘s value on a remote machine.

Log onto your Ansible controller and run the following command. This command uses the shell module (-m) to connect to the webserver machine and pass an argument (-a) which is the command to execute. In this instance, it’s running echo $PATH to return the PATH environment variable’s value.

The hostname we are using here for test is lab-vm-host01  

The given command will use the shell module (-m) to connect to the ubuntu@kube-worker-001 machine and pass an argument (-a) which is the command to execute. 
In this instance, it’s running echo $PATH to return the PATH environment variable’s value.

```
ubuntu@kube-worker-001:~$ansible lab-vm-host01 -m ansible.builtin.shell -a 'echo $PATH' 
```
Output

```
ubuntu@kube-worker-001:~$ansible lab-vm-host01 -m ansible.builtin.shell -a 'echo $PATH' 
/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/snap/bin
ubuntu@kube-worker-001:~$
```


## b. Example of shell Command Inside a `Module`

In this example 
we will create a text file on an Ansible managed node at /test/file.txt on a Linux host using an Ansibe Module.


### Steps:
a. Login to the Ansible controller host using SSH.

b. Create a directory called ansible_shell_module_test the home directory of Ansible Controller Machine. 
This directory will contain the `playbook` to run the `shell` module

c. Create a file called `exampleplaybook.yml` using vi editor in the `~/ansible_shell_module_test` directory and paste in the following YAML playbook contents.
This playbook has a single task that uses the Ansible shell module to send some text (any text content) to the /test/file.txt text file.
Since the playbook will be creating the file in the /test directory, Ansible will need to run with sudo permissions using the become attribute.

```yml
tasks:
     - name: Create a text file in opt directory using /bin/sh shell
         ansible.builtin.shell: echo "adding test file contents " > /test/file.txt
         become: true   # To make sure highest permissions are used on the remote host
```


# 4. Register

Ansible registers can be  used when we need to capture the output of a task and store it in a variable.
It can be used for below use cases.

Conditional statement

Logging

Service Status Check

System Uptime


The variables will contain the value returned by the task.














