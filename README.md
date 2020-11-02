# Ansible Role for Sinai Omeka

This repository contains an ansible playbook for provisioning an [Omeka-S](https://omeka.org) based server with both a production and staging website. 

Clone this repository

> Note: currently this is oriented towards a Ubuntu.

## Roles

The following roles are included.

| Role | Description |
|-------|------------|
| apache | installs and Apache Webserver with bare configuration and needed by the PHP role | 
| perconadb | Installs `perconadb` and `python-mysqldb`, sets up root password for all root accounts, creates .my.cnf with root password creds (to `/root/.my.cnf` on the server), deletes anonymous mysql server user for server hostname and for local host and removes the mysql test database. |
| php | Installs PHP 7.2 and all necessary php extensions Omeka-S needs.  Also modifies the php configuration |
| omeka | Downloads and creates a generic local Omeka.  You will end up with working vanilla Omeka download for the domains on the server |
| omeka_sites | Sets up a new site and domain on your server |

## Usage

To get started, you just need to do the following:

### 1. Create a server that has a sudo user account already set up.

Make sure that whatever machine you are connecting from as the ansible host has its public key setup on any hosts you are deploying to.

It is assumed there's already some familiarity with how [Ansible](https://ansible.com) works.

### 2. Copy `hosts.example` to `hosts` and modify it to match the new server(s)

### 3. Copy any thing with `*_example.yml` to a new file called `your_site.yml` and add your own values for the variables.

So for example we use a bastion host so go to [group_vars/gcp/bastion_example.yml](group_vars/gcp/bastion_example.yml) with a phony IP address. Create a copy of that file and make a new one that contains your bastion host

### 4 Create a new directory for your new site's variables with by using the `omeka_site_example`

rename the file in your new directory to say `sitename.yml`

### 5. Change anything with `*_example.yml` on `playbooks/omeka_sites_example.yml` to your own newly created files.

You are best served to make a copy of of `playbooks/omeka_sites_example.yml` into a new file. Make sure the new file refers to the correct variable files and not the ones that contain `example` in there



### 6. Execute ansible.

Run your new playbook by doing this:

```
ansible-playbook playbooks/your_new_site.yml
```
