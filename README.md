adauth
========

Ansible role to configure RHEL and derivates to use Microsoft Active Directory for authentication. 

Tested on Centos 6.5 and Centos 7.0. After configuration it allows only local users and users in the UnixServers group in the $server_ou to login. You should probabably see templates/sssd.conf.j2.

Requirements
------------

It is nice for the servers to be configured to use at least the Primary and Secondary domain controlers as NTP servers for the kerberos tickets.

The role joins the server in AD with Samba to generate the Keytab for GSSAPI authentication so a user with sufficient privileges to join is required.

Role Variables
--------------

The role uses the following variables, which you should override in your playbook:
* `adauth_workgroup` - The short domain name uppercase.
* `adauth_realm` - The domain name uppercase.
* `adauth_pdc` - The primary domain controller fqdn
* `adauth_pdc_ip` - The primary domain controller ip (for dns)
* `adauth_sdc` - The secondary domain controller fqdn
* `adauth_sdc_ip` - The secondary domain controller ip (for dns)
* `adauth_ldap_base` - The LDAP search base
* `adauth_server_ou` - The Organisational unit where to create the computer in AD
* `adauth_username` - The username with join privileges in the server OU
* `adauth_password` - The password


Example Playbook
-------------------------

    - hosts: ad-servers
      vars_files:
        - site_vars/adauth.yml

      roles:
         - glisha.adauth

Where site_vars/adauth.yml is defaults/main.yml modifed to your needs.


License
-------

MIT

Author Information
------------------

Georgi Stanojevski
[GitHub project page](https://github.com/glisha/ansible-adauth)
