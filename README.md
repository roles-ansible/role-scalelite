[![MIT License](https://raw.githubusercontent.com/roles-ansible/role-scalelite/master/.github/license.svg?sanitize=true)](https://github.com/roles-ansible/role_scalelite/blob/master/LICENSE)
[![Ansible Lint check](https://github.com/roles-ansible/role-scalelite/workflows/Ansible%20Lint%20check/badge.svg)](https://github.com/roles-ansible/role-scalelite/actions?query=workflow%3A%22Ansible+Lint+check%22)
[![Ansible check debian:buster](https://github.com/roles-ansible/role-scalelite/workflows/Ansible%20check%20debian:buster/badge.svg)](https://github.com/roles-ansible/role-scalelite/actions?query=workflow%3A%22Ansible+check+debian%3Abuster%22)

# role-scalelite
Ansible role to deploy scalelite without docker

**IN DEVELOPMENT - NOT FOR PRODUCTION USE!**

The scalelite repository can be found there:
https://github.com/blindsidenetworks/scalelite.git

We recomend to use this role together with https://github.com/n0emis/ansible-role-bigbluebutton.git

 What is this role doing?
--------------------
 + First we do a simple version check, if this is enabled in the config. (disabled by default)
 + We use some external roles for managing a specific ruby version, installing postgresql and adding a user and a database.
 + Next, we install some dependencies needed for scalelite.
 + We set up the scalelite user and group.
 + We clone the scalelite git and checkout the release we wrote in our variables.
 + We set up some global ruby parameter like /etc/gemrc
 + We install some ruby gems and the part from the scalelite-Gemfile
 + We set up some systemd files for the scalelite api and starting them
 + We adding servers to the API (in progress)

 OPEN ToDos:
-------
+ Setup and configure Webserver **(important, HIGH PRIO)**
+ Manage Servers with the API *(started in tasks/cluster*.yml)
+ Improve Database and make it optional/better configurable
+ Test it
+ Test it with more clients and servers
+ documentation
+ Publish on galaxy
+ ggf. more testing options (molecule, travis-ci etc.)

 DEVELOPEMENT
---------
We use this setup for testing:
 + https://github.com/DO1JLR/testing_bbb.git


 Minimum Server Requirements
-----------------------
For the Scalelite Server, the minimum recommended server requirements are:

 + 4 CPU Cores
 + 8 GB Memory

For **each** BigBlueButton server, the minimum requirements can be found [here](http://docs.bigbluebutton.org/2.2/install.html#minimum-server-requirements).

**For the external Postgres Database, the minimum recommended server requirements are:**
- 2 CPU Cores
- 2 GB Memory
- 20 GB Disk Space (should be good for tens of thousands of recordings)

 Dependency
------
 + geerlingguy.ruby
   * *we need this role to install the ruby version we want*
 + geerlingguy.postgresql
   * *we use this role to install and create a postgresql user and database.*
   * It could be a good idea to make this dependency optional and allow the use of external postgres servers/clusters. **HELP-WANTED!**


```bash
ansible-galaxy install -r requirements.yml
```

 Variables:
------------
The variables are currently not well documentated. But the can be found all in the defaults folder.

Some of the variables contain ugly default secrets. For production use you have to change them!

