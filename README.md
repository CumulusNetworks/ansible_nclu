# Configuration Backup and Restore

These example playbooks can be used to perform a backup and restoration of configuration using the Network Command Line Utility (NCLU)

## Prereqs
* Ansible 2.0+
* Cumulus 3.3.0+

## Assumptions
This example was built to work with the [cldemo-vagrant](https://github.com/CumulusNetworks/cldemo-vagrant) reference topology.

## How to Run
There are two playbooks included in this Git repo.  You can choose to just copy the code down or do a git clone to your local machine (preferred)

1). Clone this repo.
```
cumulus@oob-mgmt-server:$ git clone https://github.com/CumulusNetworks/ansible_nclu.git
cumulus@oob-mgmt-server:$ cd ./ansible_nclu
```

## Backup Your Configurations
2). Run the Configuration Backup Playbook
```
cumulus@oob-mgmt-server:$ ansible-playbook pull_nclu.yml
```
At this point, the playbook will create a directory called configuration_storage with subdirectories for each switch. The directory for each switch will be populated with two files, one containing the NCLU commands required to restore the present state, and the other with the output of `net show config files` which will archive the flat files required to restore the state as well.

Two copies of the files will be created, one that is timestamped and another version which is always prepended with the name "current".

## Restore Your Configurations
3). Run the Configuration Restore Playbook
```
cumulus@oob-mgmt-server:$ ansible-playbook push_nclu.yml
```
This playbook will restore your configurations using the NCLU commands prepended with the name "current"

## Background Info

Prior to the Cumulus Networks NCLU Module for Ansible there was a Knowledge Base article on backup and restoring configs on Cumulus Linux here: [https://support.cumulusnetworks.com/hc/en-us/articles/209620358-Ansible-Backing-up-Existing-Configurations](https://support.cumulusnetworks.com/hc/en-us/articles/209620358-Ansible-Backing-up-Existing-Configurations).  This method will still work but for those who want to use the NCLU module and `net` command soley and not keep track of which files they are touching this provides an alternate method.
