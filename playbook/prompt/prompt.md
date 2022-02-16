<link rel='stylesheet' href='../assets/css/main.css'/>

# Overview

In this lab, You will learn how to get input from user while running a playbook.



## Duration

45 minutes

## Step 1 — creating a playbook to prompt for input



```text
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

Save and run the playbook

```bash
$ ansible-playbook playbook.yml
```

## Well done! 👏