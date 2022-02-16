<link rel='stylesheet' href='../assets/css/main.css'/>

# Overview

In this lab, You will learn how to use ansible vault to store your sensitive data securely.

## Duration

45 minutes

## Step 1 - creating a secure file

First we are going to need a file that we are going to encrypt. This can either be a new file created in the vault process, or we can encrypt a file that already exists. Let’s look at a new file first.

Enter the command 

```bash
$ ansible-vault create test-vault.yml
```

In this example we created a file called test-vault.yml

We entered some data in the file and saved it.

Now if we look at the file

```bash
$ cat test.yml
```

You can see that the contents of the file is now encrypted.

If we want to view that file we just enter the command:

```bash
$ ansible-vault view test-vault.yml
```

You will be prompted for a password, and then you can see the contents of the file.

## Step 2 — What if you wanted to encrypt a file that already exists?

So you already have all your passwords and sensitive information in a file — in this case it is in `group_vars/all.yml`

This is the file

```text
ansible_user: "roger"
ansible_ssh_pass"cisco"
ansible_network_os: "ios" 
```

We are going to encrypt it and then design a playbook that needs that password information and see what happens.

First we will encrypt the file with the `ansible-vault encrypt group_vars/all.yml` command

```bash
$ ansible-vault encrypt group_vars/all.yml
```

You are prompted for a password, and the file is now encrypted.

To verify if we view the file we just see the encrypted data.

```bash
$ cat group_vars/all.yml
```



## Step 3 - Using Ansible Vault in Playbook

Now we will design playbook called `backup.yml`, which will need to access the data in `group_vars/all.yml`

So let’s see what happens when we run the playbook?

```text
We get an error: Attempting to decrypt but no vault secrets found
```

The reason for this is the `all.yml` file is now encrypted, and you need a password to access the data, however we did not tell Ansible how to get the password.

You can do this in a few ways


- Prompt for the password during the playbook run
- Specify the location to a password file during the playbook run.
- Specify the location to the password in ansible.cfg

Let’s look at all first options


## Option 1 — Prompt for the password during the playbook run

Just add `--ask-vault-pass` this to the end of your playbook run command e.g.

```bash
$ ansible-playbook backup.yml --ask-vault-pass 
```

## Option 2 — Using Ansible Vault with a Password File

You can also have another file, which contains your password. This file does need to be secured either by on machine permissions and kept out of your Git repository.

You then specify where this file is with this command

```bash
$ ansible-playbook backup.yml --vault-password-file vault-pass.txt
```

## Option 3 - Specify the location of a password file in `ansible.cfg`

You can also specify the location of this file in the `ansible.cfg` file.

```text
vault_password_file = vault-pass.txt
```

## Step 4 — Decrypting Encrypted Files

If you no longer want your file to be encrypted, you can easily decrypt it using the following code.

```bash
$ ansible-vault decrypt <filename> 
```


## Well done! 👏