# Ansible-OpenLDAP-Basic
Easy OpenLDAP, Cyrus SASL, OpenSSL, for compiled source setups. 

## Quick Start

To run this playbook clone the repository and change the variables found within roles/upgrade/vars/main.yml (defaults in brackets:

Update the included hosts file. Then run the playbook:

    ansible-playbook -i hosts upgrade_openldap.yml -t "all,debug"

## Variables 

    base_dir - Location of the working directory [/apps]
    src_dir - Location of where the source file will be copied to [/apps/src]
    openldap_version - Version of OpenLDAP to install [2.4.49]
    openldap_install_dir - Location of where OpenLDAP will be installed [/apps/openldap]
    openldap_configs_args - OpenLDAP installation flags 
      [--prefix={{ openldap_install_dir }} --disable-bdb --disable-hdb --enable-ldap --enable-meta --enable-overlays --enable-module]
    openssl_version - [1.1.1g]
    openssl_install_dir - [/appl/openssl/]
    openssl_config_args - [-fPIC -DPIC --prefix={{ openssl_install_dir }}]
    unixodbc_version - [2.3.7]
    unixodbc_install_dir - [/appl/unixodbc/]
    unixodbc_config_args - [--prefix={{ unixodbc_install_dir }}]
    cyrus_sasl_version - [2.1.27]
    cyrus_sasl_install_dir - [/appl/cyrus_sasl/]
    cyrus_sasl_config_args - [--prefix={{ cyrus_sasl_install_dir }} --with-plugindir=/appl/cyrus_sasl/lib/sasl2 --with-configdir=/appl/cyrus_sasl/lib/sasl2 --with-saslauthd=/appl/cyrus_sasl/var/run --with-ldap --disable-checkapop --disable-cram --disable-digest --disable-scram --disable-otp --disable-gssapi --disable-anon]
    working_env - Compilation flags 
      CC - [gcc]
      CFLAGS - [-O -g]
      CPPFLAGS - [-I/appl/openldap/include -I/usr/include -DF00=42]
      LDFLAGS - [-L/appl/openldap/lib -L/usr/lib]
      LIBS - [-lpthread -ldl]
      LDAP_HOME - [/appl/openldap]

## Setup Instructions

1. Clone the repository
2. Modify the variable file 
3. From the parent directory, run the following command:

To upgrade all packages:

    ansible-playbook -i hosts upgrade_openldap.yml -t "all,debug"

To upgrade openldap:

    ansible-playbook -i hosts upgrade_openldap.yml -t "copy:source,upgrade:openldap:1,debug-upgrade:openldap:1"

To upgrade cyrus sasl:

    ansible-playbook -i hosts upgrade_openldap.yml -t "copy:source,upgrade:cyrussasl,debug-upgrade:cyrus_sasl"

To upgrade openssl:

    ansible-playbook -i hosts upgrade_openldap.yml -t "copy:source,upgrade:openssl,debug-upgrade:openssl"

To upgrade unixodbc:

    ansible-playbook -i hosts upgrade_openldap.yml -t "copy:source,upgrade:unixodbc,debug-upgrade:unixodbc"

