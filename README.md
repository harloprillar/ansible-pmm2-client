Ansible role: pmm2_client
=========
[![Build Status](https://travis-ci.com/harloprillar/ansible-pmm2-client.svg?branch=master)](https://travis-ci.com/harloprillar/ansible-pmm2-client)

Ansible role that installs and configures Percona Monitoring and Management client version 2. 
Currently only mysql client service supported. 
For mysql, persistence of configuration variables is only supported for version > 8.0. Otherwise, you should add options manually into your server configuration file as described in [documentation](https://www.percona.com/doc/percona-monitoring-and-management/2.x/setting-up/client/mysql.html).

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
| `pmm2_client_mysql_login_user` | root | Mysql instance login user. |
| `pmm2_client_mysql_login_password` | root | Mysql instance user password. |
| `pmm2_client_mysql_login_host` | localhost | Mysql instance host. |
| `pmm2_client_mysql_login_port` | 3306 | Mysql instance port. |
| `pmm2_client_mysql_enable_tls` | false | Mysql enable TLS connection to mysql database. |
| `pmm2_client_mysql_create_user` | true | Mysql create PMM user in mysql instance. |
| `pmm2_client_mysql_user` | pmm | Mysql user name for PMM user. |
| `pmm2_client_mysql_password` | pmm | Mysql password for PMM user. |
| `pmm2_client_mysql_host` | % | Mysql allowed hosts for PMM user. |
| `pmm2_client_mysql_privileges` | \*.\*:SELECT,PROCESS,SUPER,REPLICATION CLIENT,RELOAD | Mysql privileges defined for PMM user. |
| `pmm2_client_mysql_query_source` | perfschema | Mysql the query source. Currently only "perfschema" is supported |
| `pmm2_client_mysql_enable_query_response_time` | true | Enable query response time metrics for mysql |
| `pmm2_client_mysql_disable_tablestats` | false | Disables tablestats collection when the default limit is reached (mysql) |
| `pmm2_client_mysql_disable_tablestats_limit` | 1000 | Number of tables for which tablestats collection is disabled. 0 means no limit. (mysql) |
| `pmm2_client_mysql_enable_user_statistics` | true | Enable user statistics for mysql |


Example Playbook
----------------

An example playbook that installs and conigures pmm-client with mysql service:

    - hosts: mysql-servers
      vars:
        pmm2_client_server_host: instance-pmm-server
        pmm2_client_server_user: admin
        pmm2_client_server_password: admin
        pmm2_client_enabled_services:
          - mysql
        pmm2_client_mysql_login_host: instance-mysql
        pmm2_client_mysql_login_user: root
        pmm2_client_mysql_login_password: root
      roles:
         - harloprillar.pmm2_client

License
-------

MIT
