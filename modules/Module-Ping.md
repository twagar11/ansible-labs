<link rel='stylesheet' href='../assets/css/main.css'/>

# Overview

In this lab, You will learn how to confirm the connection between your control center and hosts

basically, We are going to use a module called `ping` 


## Duration

25 minutes


## Step 1 - Requirements

In our labs, are hosts are using password for authentication. 

Ansible needs another application called `sshpass` to connect to hosts.

run the following command only on your control center

```bash
$ sudo apt-get install -y sshpass
```

to confirm that `sshpass` is installed use the following command:

```bash
$ sshpass -V
```
output will look like:

```console
sshpass 1.06
(C) 2006-2011 Lingnu Open Source Consulting Ltd.
(C) 2015-2016 Shachar Shemesh
This program is free software, and can be distributed under the terms of the GPL
See the COPYING file for more information.

Using "assword" as the default password prompt indicator.
```


## Step 2 - getting to know the Module `ping`

`ping` module is use to verify connectivity between the control center and hosts

default template looks like:

```bash
$ ansible <Host-Group> -m ping
```

## Step 3 - Running a sample

run the following command to see the results

```bash
$ ansible webserver -m ping
```

output

```console
<IP 1> | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3"
    },
    "changed": false,
    "ping": "pong"
}
<IP 1> | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3"
    },
    "changed": false,
    "ping": "pong"
}

```

note the following part
```console
    SUCCESS
    "changed": false,
    "ping": "pong"
```

This means
- C&C can connect to the hosts
- nothing is changed on the hosts


## Well done! 👏