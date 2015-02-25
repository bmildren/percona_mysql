# An ansible role for Percona Server

Version: 0.1

This role aims to install Percona Server using a dynamic configuration, whilst being mindful of selinux & apparmor.  Every element of the my.cnf is dynamic, and additional plugins such as TokuDB and Audit Logging can be added on-demand.

Basic variables can be seen in defaults/main.yml.  Lower level variables can be seen in the vars directory.  If you'd like to dynamically edit the dictionaries used by the my.cnf, for your own sanity ensure you set hash_behaviour = merge in the ansible configuration file.

If no passwords are supplied for the root or percona users, the role uses the password lookup to generate a random password, however it's recommended you use ansible vault to store the passwords.

The role will continue to be actively developed, pull requests are of course welcomed.

Example usage:

  roles:
  
      - { role: percona_mysql, percona_mysql_include_tokudb_variables: true, percona_mysql_include_auditlog_variables: true }

There are several tags used in the role, mostly this are useful if you want to skip sections:

- percona_mysql_additional_pkgs (Skip to avoid installing additional_pkgs defined in vars/{{ ansible_os_family }}.yml)
- percona_mysql_backup_pkgs (Skip to avoid installing backup_pkgs defined in vars/{{ ansible_os_family }}.yml)
- percona_mysql_manage_init_script (Skip to avoid replacing the default init script)
- percona_mysql_manage_logs (Skip to avoid logrotate)
- percona_mysql_manage_security (Skip to avoid selinux / apparmor actions)
- percona_mysql_optional_pkgs (Skip to avoid installing optional_pkgs defined in vars/{{ ansible_os_family }}.yml)
- percona_mysql_tokudb_prereq (Skip to avoid performing TokuDB prereqs, such as disabling Transparent HugePages - useful if this is picked up by another role)
