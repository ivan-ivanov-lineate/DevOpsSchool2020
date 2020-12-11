Filebeat role
=========

This ansible role install and configure [filebeat](https://www.elastic.co/products/beats/filebeat)

Requirements
------------

This role need Ansible 2.1. It's also supposed that
you are using the merge behaviour for variables (please, see about
[hash_behaviour=merge](http://docs.ansible.com/ansible/intro_configuration.html#hash-behaviour)
for details). Tested on Centos 6.5/7 and Debian 7/8

Dependencies
------------

This role doesn't depend from other ansible roles



Role Variables
--------------

Default config variables are described in */filebeat/defaults/main.yml*.
If you need an extended configuration you can specify it in the variables for each environment in section *filebeat.options*. Structure of section *filebeat.options* repeats *filebeat.yml*, you can insert any parameters described in official filebeat [documentation](https://www.elastic.co/guide/en/beats/filebeat/current/filebeat-configuration-details.html)

Example Playbook
----------------

An example of how to use filebeat role:

    - hosts: all
      roles:
        - role: filebeat
          filebeat:
            options:
              filebeat:
                config_dir: /etc/filebeat/conf.d/
                prospectors:
                -
                  paths:
                  - /var/log/*.log
                  - /var/log/messages
                  - /var/log/cron
                  - /var/log/dmesg
                  - /var/log/secure
                  - /var/log/syslog
                  - /var/log/apt/history.log
                  - /var/log/dpkg.log
                  - /var/log/auth.log
                  - /var/log/user.log
                  - /var/log/yum.log
              logging:
                files:
                  name: filebeat.log
                  path: /var/log/filebeat/
                  rotateeverybytes: 10485760
                level: info
                to_files: true
                to_syslog: true
              output:
                elasticsearch:
                  bulk_max_size: 50
                  flush_interval: 1
                  hosts: "[{{ '\"' + groups[  'elasticsearch'  ] | join(':9200\", \"')  + ':9200\"' }}]"
                  index: filebeat
                  max_retries: 3
                  save_topology: false
                  timeout: 90
                  topology_expire: 15
                  index: "filebeat"
                file:
                  filename: filebeat
                  number_of_files: 7
                  path: /tmp/filebeat
                  rotate_every_kb: 10000


License
-------

MIT


Author Information
------------------

Alexander Matyuhin <amatyuhin@thumbtack.net>