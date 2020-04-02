Ansible Role Promtail
=====================

This role installs [Promtail](https://github.com/grafana/loki/tree/master/docs/clients/promtail).

Promtail is an agent which ships the contents local logs to a private Loki instance or to the Grafana Cloud.
It's usually deployed to every machine that has applications needed to be monitored.  

Requirements
------------
None.

Role Variables
--------------

``` yaml
# Version of promtail that should be installed.
promtail_version: "1.3.0"

# The loki server where promtail will send the data to.
promtail_loki_server_proto: "https"
promtail_loki_server_domain:

# Promtail scrape configurations
#
# Example:
# - job_name: syslog
#   static_configs:
#     - targets:
#       - localhost
#       labels:
#         job: syslog
#         host: {{ ansible_fqdn }}
#         __path__: /var/log/syslog
promtail_scrape_configs: []

# Installation from source settings
promtail_install_from_source: false
promtail_home_dir: /opt/promtail
promtail_config_dir: /etc/promtail
promtail_executable: /usr/local/bin/promtail
promtail_executable_options:

promtail_http_listen_server: "9080"
promtail_grpc_listen_port: "0"
```

Dependencies
------------
None.

Example Playbook
----------------

``` yaml
- hosts: all
  roles:
    - { role: rhazdon.promtail, tags: promtail }
  vars:
    promtail_install_from_source: true
    promtail_loki_server_domain: my_loki_instance
    promtail_scrape_configs:
      - job_name: syslog
        static_configs:
          - targets:
            - localhost
            labels:
              job: syslog
              host: "{{ ansible_fqdn }}"
              __path__: /var/log/syslog
```

License
-------

MIT

Author Information
------------------

This role was created in 2020 by Djordje Atlialp.
