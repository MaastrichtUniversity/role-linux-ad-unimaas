# Ansible role-linux-ad-unimaas
====================

https://github.com/MaastrichtUniversity/role-linux-ad-unimaas

Ansible role for deploying SSSD for Active Directory login at UNIMAAS

## How it works
This Ansible role set and installs a number of things:

* Setup time synchronisation with AD domain controller using timesyncd (systemd replacement of ntpd)
* Install realmd, SSSD, SSSD-AD and Kerberos5 (k5)
* Authenticate as domain user (using k5) to join the computer to domain
* Setup SSSD to perform authentication against AD. Uses special UID mappings.
* Changes PAM to use SSSD authentication method

## Instructions

* Pre-register the computer-name in the AD
* Change hostname to computer-name in `/etc/hostname` and `/etc/hosts`

## Variables to set
Set these variables in your inventory or in defaults/main.yml
* `domain_user:` and `domain_pass:` of a domain user with rights to join computers to the domain

* `homedir_template:` Linux home directory to be used and created for domain users
* `login_shell:` Login shell to be used for domain users
* `require_membership_of:` Users are required to be member of this security group before they can login 

## Supported platforms
* Ubuntu 16.04

## TODO
* Support for Redhat/CentOS
