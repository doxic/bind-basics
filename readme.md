# Bind Basics and setup

**work in progress**
Todo:
* DNS theory
* DNS Concept
* Setup BIND
* Hardening
* Testing suite
* attacks
* DNSSEC



## Introduction

### Network Concept

Centos7 - nixsrv001  
Hostname: anssrv001.m123.local  
IP: 192.168.56.100

Centos7 - nixsrv002
Hostname: anssrv001.m123.local  
IP: 192.168.56.50

Centos7 - Ansible manager  
Hostname: anssrv001.m123.local  
IP: 192.168.56.101

## Prerequisites
### ansible_local
executing ansible-playbook directly on the guest machine.
```
Vagrantfile
provisioning
    playbook.yml              # ansible provisioner playbook
    production                # inventory file for production servers
    staging                   # inventory file for staging environment

    group_vars/
       group1                 # here we assign variables to particular groups
       group2                 # ""
    host_vars/
       hostname1              # if systems need specific variables, put them here
       hostname2              # ""

    library/                  # if any custom modules, put them here (optional)
    filter_plugins/           # if any custom filter plugins, put them here (optional)

    site.yml                  # master playbook
    webservers.yml            # playbook for webserver tier
    dbservers.yml             # playbook for dbserver tier

    roles/
        common/               # this hierarchy represents a "role"
            tasks/            #
                main.yml      #  <-- tasks file can include smaller files if warranted
            handlers/         #
                main.yml      #  <-- handlers file
            templates/        #  <-- files for use with the template resource
                ntp.conf.j2   #  <------- templates end in .j2
            files/            #
                bar.txt       #  <-- files for use with the copy resource
                foo.sh        #  <-- script files for use with the script resource
            vars/             #
                main.yml      #  <-- variables associated with this role
            defaults/         #
                main.yml      #  <-- default lower priority variables for this role
            meta/             #
                main.yml      #  <-- role dependencies
            library/          # roles can also include custom modules
            lookup_plugins/   # or other types of plugins, like lookup in this case

        webtier/              # same kind of structure as "common" was above, done for the webtier role
        monitoring/           # ""
        fooapp/               # ""
```

Add required vagrant boxes
```Bash
vagrant box add wittman/centos-7.2-ansible
vagrant box add centos/7
```

Install plugin (broken for Win10/Win2016). Updates VBoxGuestAdditions on first boot
```Bash
vagrant plugin install vagrant-vbguest
```

This plugin allows you to use putty to ssh into VMs
```Bash
vagrant plugin install vagrant-multi-putty
set PATH=%PATH%;C:\Program Files (x86)\PuTTY
```

Start up server instance with `vagrant up`


## References
* [Best Practices — Ansible Documentation](http://docs.ansible.com/ansible/playbooks_best_practices.html#how-to-differentiate-staging-vs-production)How To Configure
* [BIND as a Private Network DNS Server on CentOS 7 | DigitalOcean](https://www.digitalocean.com/community/tutorials/how-to-configure-bind-as-a-private-network-dns-server-on-centos-7)
* [DNS for Rocket Scientists](http://www.zytrax.com/books/dns/)
* [Best Practices for Internal Domain and Network Names - TechNet Articles](https://social.technet.microsoft.com/wiki/contents/articles/34981.active-directory-best-practices-for-internal-domain-and-network-names.aspx)
