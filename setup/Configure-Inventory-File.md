<link rel='stylesheet' href='../assets/css/main.css'/>

# Overview

In the previous lab, you defined your hosts in the ansible default's place,

Let's define them in a better file/folder structure

We are going to create some directories and define our hosts there.

## Duration

30 minutes


## Step 1 - Create project

Create your project folder.

```bash
$ mkdir ~/our-big-project/
```

to follow a practice coding advices, we'll create a folder to store our inventories there,

```bash
$ mkdir ~/our-big-project/inventories/
```
 
as a sample, we are going to define our hosts in production group.

```bash
$ mkdir ~/our-big-project/inventories/production/
```

and for the last step, create your inventory file

**NOTE:** Inventory file is extensionless.

```bash
$ touch ~/our-big-project/inventories/production/webserver
```

## Step 2 - Add Hosts

Just like [this](Configure-Inventory.md) lab, add your hosts.

**BEST PRACTICE:** Only add one group per file.

## Step 3 - Test the Host file

try to ping the hosts in the new inventory

```bash
$ cd ~/our-big-project/inventories/production/

$ ansible -i webserver -m ping
```

## Exercise

Try to define some domains and try to add them to your hosts


## Well done! 👏