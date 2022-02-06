<link rel='stylesheet' href='../assets/css/main.css'/>

# Overview

In this lab, You will learn how to get facts from your hosts

basically, We are going to use a module called `setup`

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

## Step 2 - getting to know the Module `hosts`

`setup` module is used to pull config data from hosts

default template looks like:

```bash
$ ansible <Host-Group> -m setup
```

**NOTE:** result of this module will be very lengthy JSON string.

## Step 3 - Running a sample

run the following command to see the results

```bash
$ ansible webserver -m setup
```

output will be very long

## Step 4 - Filter Gathered Facts

to filter the received data from this module use the following template

```bash
ansible <Host-Group> -m setup -a "filter=<Your-needs>"
```

sample:

```bash
ansible webserver  -m setup -a "filter=ansible_distribution*"
```

output

```console
<IP 1> | SUCCESS => {
    "ansible_facts": {
        "ansible_distribution": "Ubuntu",
        "ansible_distribution_file_parsed": true,
        "ansible_distribution_file_path": "/etc/os-release",
        "ansible_distribution_file_variety": "Debian",
        "ansible_distribution_major_version": "20",
        "ansible_distribution_release": "focal",
        "ansible_distribution_version": "20.04",
        "discovered_interpreter_python": "/usr/bin/python3"
    },
    "changed": false
}
<IP 2> | SUCCESS => {
    "ansible_facts": {
        "ansible_distribution": "Ubuntu",
        "ansible_distribution_file_parsed": true,
        "ansible_distribution_file_path": "/etc/os-release",
        "ansible_distribution_file_variety": "Debian",
        "ansible_distribution_major_version": "20",
        "ansible_distribution_release": "focal",
        "ansible_distribution_version": "20.04",
        "discovered_interpreter_python": "/usr/bin/python3"
    },
    "changed": false
}
```

As you can see, this command will give you the info about OS of the hosts

Practice:

- Try to get time info from your hosts

**Hint:**

```bash
$ ansible webserver  -m setup -a "filter=ansible_date_time*"
```

## Well done! 👏