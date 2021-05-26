pmm2_client
=========

Ansible role that installs and configures Percona Monitoring and Management client 2 

Requirements
------------

Ansible 2.5.0 or higher.

Role Variables
--------------
| Name | Default Value | Description                        |
| --- | --- | ---|
| `pmm2_client_server_user` | admin | PMM server user name |
| `pmm2_client_server_password` | admin | PMM server user password |
| `pmm2_client_server_host` | localhost | PMM server host |
| `pmm2_client_server_port` | 443 | PMM server port |
| `pmm2_client_node_address` | | Node address (autodetected by pmm-admin if not defined) |
| `pmm2_client_node_type` | | Node type, one of: generic, container (default to generic by pmm-admin if not defined) |
| `pmm2_client_node_name` | | Node name (autodetected by pmm-admin if not defined) |
| `pmm2_client_disable_log` | false | Disable logging to prevent littering system log file |
| `pmm2_client_enabled_services` | [] | List of services to configure. Currently only "mysql" is supported. |
| `pmm2_client_mysql_login_user` | root | Mysql service: instance login user. |
| `pmm2_client_mysql_login_password` | root | Mysql service: instance user password. |
| `pmm2_client_mysql_login_host` | localhost | Mysql service: instance host. |
| `pmm2_client_mysql_login_port` | 3306 | Mysql service: instance port. |
| `pmm2_client_mysql_enable_tls` | false | Mysql service: enable TLS connection to mysql database. |
| `pmm2_client_mysql_create_user` | true | Mysql service: create PMM user in mysql instance. |
| `pmm2_client_mysql_user` | pmm | Mysql service: user name for PMM user. |
| `pmm2_client_mysql_password` | pmm | Mysql service: password for PMM user. |
| `pmm2_client_mysql_host` | % | Mysql service: allowed hosts for PMM user. |
| `pmm2_client_mysql_privileges` | \*.\*:SELECT,PROCESS,SUPER,REPLICATION CLIENT,RELOAD | Mysql service: privileges defined for PMM user. |
| `pmm2_client_mysql_query_source` | perfschema | Mysql service: the query source. Currently only "perfschema" is supported |


Example Playbook
----------------

An example playbook that installs and conigures pmm-client with mysql service:

    - hosts: mysql-servers
      roles:
         - harloprillar.pmm2_client
      vars:
        pmm2_client_server_host: instance-pmm-server
        pmm2_client_server_user: admin
        pmm2_client_server_password: admin
        pmm2_client_enabled_services:
          - mysql
        pmm2_client_mysql_login_host: instance-mysql
        pmm2_client_mysql_login_user: root
        pmm2_client_mysql_login_password: root

License
-------

MIT
