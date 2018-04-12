# Ansible role-linux-ad-unimaas

https://github.com/MaastrichtUniversity/role-linux-ad-unimaas

Ansible role for deploying SSSD for Active Directory login at UNIMAAS. Feel free to fork this repository and change to 
your own needs. We recommend to keep the UID mappings defined in sssd.conf the same, to have universal UIDs accross UNIMAAS.

## How it works
This Ansible role set and installs a number of things:

* Setup time synchronisation with AD domain controller using timesyncd (systemd replacement of ntpd)
* Install realmd, SSSD, SSSD-AD and Kerberos5 (krb5)
* Authenticate as domain user (using krb5) to join (using adcli) the computer to domain
* Setup SSSD to perform authentication against AD. Uses special UID mappings.
* Changes PAM to use SSSD authentication method

## Instructions

* Pre-register the computer-name in the AD
* Change hostname to computer-name in `/etc/hostname` and `/etc/hosts`
* Add this Ansible role to your playbook and run your playbook

## Variables to set
Set these variables in your inventory or in defaults/main.yml

* `ad_user:` and `ad_user_pass:` of a domain user with rights to join computers to the domain
* `ad_homedir:` Linux home directory to be used and created for domain users
* `ad_shell:` Login shell to be used for domain users
* `ad_allowed_security_groups:` Security groups that are allowed access (by default no one is allowed)
* `ad_allowed_security_users:` Users that are allowed access (by default no one is allowed)

## Supported platforms
* Ubuntu 16.04

## TODO
* Support for Redhat/CentOS
* sudo access via security group
* support for setting pam_mkhomedir