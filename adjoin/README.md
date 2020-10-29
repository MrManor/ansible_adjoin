=======
# AD domain join
Automate Linux Machine join AD using Ansible. This module is inspired from the work of 
  * https://github.com/rahulinux/ansible-domain-join 
  * https://github.com/riponbanik/ansible-role-domain-join

The group Domain Administrators is configured with sudo enabled

Note: expect is used to supply the password for join. Please make sure your LANG settings dont mess 
up the password prompt

### Ansible
Tested using the following versions:
 * ansible 2.9.6 runnning on openSUSE

### Operating systems

Tested with Centos 8

## Example Playbook

Clone the repository in the roles directory in ansible as adjoin and include this role in your list.
For example

```
---
- hosts: all
  # replace vars below with variables from your vault if you like
  become: yes
  vars_prompt:
    - name: ad_user
      prompt: "AD user for join?"
      private: no
    - name: ad_pass
      prompt: "AD join password?"
  roles:
    - adjoin
```

## Variables

Variables neeeded:
```
---
# OU to place target in (must exist)
ou_membership: "OU=Nix Computers,DC=itu,DC=local"
# usergroups given access ti target
ad_access_groups:
  - domain admins
  - some department
  - helpdesk
# used for Kerberos setup - may not be nessesary 
ad_server:
  fqdn: dc3.itu.local
  domain: ITU.LOCAL
```

## Leaving the domain
If you want to reverse the process and remove the machine from the domain, simply run the ‘realm leave’ command followed by the domain name, as shown below. <br/>
**realm leave example.com**
