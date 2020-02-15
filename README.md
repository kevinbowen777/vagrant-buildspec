# vagrant-buildspec

    A simple template to streamline populating a Vagrantfile for use with
    VirtualBox and Ansible.

## Installation ##

        git clone https://github.com/kevinbowen777/vagrant-buildspec.git

## Requirements ##
    Vagrant
    VirtualBox
    Ruby
    A Linux Host

## Description ##
    The build_spec.yml file contains the details of the Vagrant build
    specifications. When the command `vagrant up` is run, the Vagrantfile
    loads build_spec.yml and populates the fields with values to build
    the Virtual Machine.
    Both the Ansible inventory and playbook.yml files will need to be 
    manually updated with values appropriate to the build.

    Currently, the following values are supported for build customisation:
        VirtualBox Name
        VirtualBox Guest Hostname 
        Vagrant Box Name
        Ansible Host
        CPU
        Memory
        Private IP Address
        Public IP Address
        Forwarding Ports
            Guest Port
            Host Port  
        Synced Folders
            Guest Directory
            Host Directory
        Ansible Inventory File Location
        Ansible Playbook Location           

    In order for the build to complete successfully, all fields in the 
    build_spec.yml need to be populated. If a particular value is not 
    required for the build, then the line containing its variable name
    must be commented out in the Vagrantfile file.


## License
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
