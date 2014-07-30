adauth
========

Ansible role to configure RHEL and derivates to use Microsoft Active Directory for authentication. 

Tested on Centos 6.5 and Centos 7.0. After configuration it allows only local users and users matching the $adauth_access_filter to login. You should probabably see templates/sssd.conf.j2 and defaults/main.yml.

Requirements
------------

It is nice for the servers to be configured to use at least the Primary and Secondary domain controlers as NTP servers for the kerberos tickets.

The role joins the server in AD with Samba to generate the Keytab for GSSAPI authentication so a user with sufficient privileges to join is required.

Role Variables
--------------

The role uses the following variables, which you should override in your playbook:
* `adauth_workgroup` - The short domain name uppercase.
* `adauth_realm` - The domain name uppercase.
* `adauth_pdc` - The primary domain controller fqdn.
* `adauth_pdc_ip` - The primary domain controller ip (for dns).
* `adauth_sdc` - The secondary domain controller fqdn.
* `adauth_sdc_ip` - The secondary domain controller ip (for dns).
* `adauth_ldap_base` - The LDAP search base.
* `adauth_server_ou` - The Organisational unit where to create the server in AD.
* `adauth_access_filter` - LDAP search query to limit who can login to the server. See defaults for examples.
* `adauth_username` - The username with join privileges in the server OU.
* `adauth_password` - The password. You can use var_prompts in your playbook for this.


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
