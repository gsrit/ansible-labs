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




# vars_prompt

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









