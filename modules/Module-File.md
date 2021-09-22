<link rel='stylesheet' href='../assets/css/main.css'/>

# Overview

In this lab, You will learn how to create, copy and delete files and folders on your hosts using `file` module

## Duration

25 minutes

## Step 1 - getting to know the Module `file`

`file` module is used manipulate files and folders on your hosts, this module takes two arguments:

- `src`  where your file/folder is on the `C&C`
- `dest` where the file/fo will be placed on your hosts.

Optional arguments:

- `owner`, the owner user on hosts
- `group`, the owner group on hosts
- `state`, to remove, or create folder/file on hosts.

default template looks like:

```bash
$ ansible <Host-Group> -m file -a "src=<FULL-PATH> dest=<Host-FULL-PATH>"
```

## Step 2 - Copy a file

run the following command to create a file on `C&C`

```bash
$ cd ~
#create file
$  touch hello.txt
edit the file
$ nano hello.txt 
```

write `Hello World` to `hello.txt` and save the file

now, to copy the file to our `webserver` group,

```bash
$ ansible webserver -m copy -a "src=~/hello.txt dest=~"
```

output

```console
<IP 1> | CHANGED => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3"
    },
    "changed": true,
    "checksum": "22596363b3de40b06f981fb85d82312e8c0ed511",
    "dest": "/home/ubuntu/hello.txt",
    "gid": 1000,
    "group": "ubuntu",
    "md5sum": "6f5902ac237024bdd0c176cb93063dc4",
    "mode": "0664",
    "owner": "ubuntu",
    "size": 12,
    "src": "/home/ubuntu/.ansible/tmp/ansible-tmp-1632300992.231955-212575269716511/source",
    "state": "file",
    "uid": 1000
}
<IP 2> | CHANGED => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3"
    },
    "changed": true,
    "checksum": "22596363b3de40b06f981fb85d82312e8c0ed511",
    "dest": "/home/ubuntu/hello.txt",
    "gid": 1000,
    "group": "ubuntu",
    "md5sum": "6f5902ac237024bdd0c176cb93063dc4",
    "mode": "0664",
    "owner": "ubuntu",
    "size": 12,
    "src": "/home/ubuntu/.ansible/tmp/ansible-tmp-1632300992.229054-251911723793302/source",
    "state": "file",
    "uid": 1000
}
```

note the status:

```console
CHANGED
```

it means something on your hosts is changed,
**NOTE:** ever file/folder that you put on your hosts that are without specified `user` or `group` takes the authenticated ones from your `hosts` file

Login to each host and verify that the file is there

## Step 2 - Delete a file

to delete a file on your hosts use the following command

```bash
$ ansible webserver -m file -a "dest=~/hello.txt state=absent"
```

**NOTE:**

- module is `file`
- `src` is not necessary

output

```console
<IP 1> | CHANGED => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3"
    },
    "changed": true,
    "path": "/home/ubuntu/hello.txt",
    "state": "absent"
}
<IP 2> | CHANGED => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3"
    },
    "changed": true,
    "path": "/home/ubuntu/hello.txt",
    "state": "absent"
}
```

Login to each host and verify that the file is deleted

## Step 3 - Create Directory

to create directory, first create it on `C&C`

```bash
$ cd ~
#create directory
$  mkdir test
#create file in the directory
$ cd test 
$ touch hello.txt
#edit the file
$ nano hello.txt 
```

write "Hello File" to the file, save and exit

```bash
$ ansible webserver -m file -a "dest=~/test state=directory"
```

output

```console
<IP 1> | CHANGED => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3"
    },
    "changed": true,
    "gid": 1000,
    "group": "ubuntu",
    "mode": "0775",
    "owner": "ubuntu",
    "path": "/home/ubuntu/test",
    "size": 4096,
    "state": "directory",
    "uid": 1000
}
<IP 2> | CHANGED => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3"
    },
    "changed": true,
    "gid": 1000,
    "group": "ubuntu",
    "mode": "0775",
    "owner": "ubuntu",
    "path": "/home/ubuntu/test",
    "size": 4096,
    "state": "directory",
    "uid": 1000
}
```

login to each host, you'll notice that directories are there, but the file you've created is not there, now you have to copy the file

```bash
$ ansible webserver -m copy -a "src=~/test/ dest=~/test"
```

**NOTE:** notice that we are not mentioning a specific file thus copying everything inside the directory.


login to each host, to verify the folder and file

## Step 4 - Delete Directory

Delete a specific directory from all hosts in the `websever` group with the following command:

```bash
$ ansible webserver -m file -a "dest=~/test state=absent"
```

## Step 5 - Practice

using what you just learned, try to:
- create a directory in `~/<Your-Name>/<Your-Family>`
- create two `txt` files inside the directory and write your email and name into them
- use ansible to push all these files to your hosts




## Well done! 👏