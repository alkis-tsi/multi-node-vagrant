### Creation of multiple nodes without having to type the same configuration blocks over and over. It also installs Ansible.

#### Requirements
- Virtual Box (latest version)
- Vagrant (latest version)

#### Instructions - Usage
At you command line simply clone this repository and then run:
```
$ vagrant status  ## it will show you which boxes are running
$ vagrant up      ## the current configuration will spin up two boxes with CentOS installed. The OS and the amount of nodes can be modified.
$ vagrant ssh     ## it will give you ssh access to that box
```
