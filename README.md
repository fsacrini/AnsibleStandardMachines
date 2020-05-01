Ansible Playbook Ubuntu Setup
==============================

This playbook is used to deploy configuration to target devices running Ubuntu 14.04 and 16.04

Tested on Ubuntu 14.04 and 16.04 64bits, patches are welcome.

## Installation

Clone this repo to your Ansible roles directory

    git clone https://github.com/jhernandezcsc/ansible-ubuntu-config-jlh.git


## Usage

The user must have root permissions in order to install system packages and start services.

Example Playbook:
```
  ---
  - hosts: gss-wks
    become: yes
    become_method: sudo

    roles:
      - { role: common, tags: common }
      - { role: teamviewer, tags: teamviewer }
```

## Important notes

This playbook has been tested by deploying configuration on local virutal machines as well as
remote desktops running Ubuntu 14.04 and 16.04 64bits.
Installation packages and configuration are organized in roles as instalaltion steps.

To execute this playbook the destination PC should be accessible via SSH (This means that the IP,
admin user account and ssh service need to be set before execute this script).

This playbook assumes the following installation files are going to be included into the files folder
  - roles/teamviewer/files/teamviewer_i386.deb

The destination hosts will be rebooted at the end of the execution of this playbook.

After running this playbook, the workstation will be deployed with the following packages:
  - Unetbootin
  - openjdk 7 for ubuntu 14.04
  - openjdk 8 for ubuntu 16.04
  - Libreoffice 5.2
  - Teamviewer 10
  - Clamtk
  - Twinkle softphone
  - AdobeFlash pluggin
  - It will also be configured with the required security settigns to comply with csra standards.

Example Playbook run:

A typical run of this playbook might look like this, but could vary based on your local ~/.ssh/config and DNS.

     - ansible-playbook -i wks-inv linux-setup.yml -u [admin-user] -k -K
     - ansible-playbook -i wks-inv linux-setup.yml -u [admin-user] -k -K

## Contributing

1. Fork it
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Added some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create new Pull Request
