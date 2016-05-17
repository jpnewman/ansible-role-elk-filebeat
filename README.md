# jpnewman.elk-filebeat

[![Ansible Role](https://img.shields.io/ansible/role/9588.svg?maxAge=2592000)](https://galaxy.ansible.com/jpnewman/elk-filebeat/)
[![Build Status](https://travis-ci.org/jpnewman/ansible-role-elk-filebeat.svg?branch=master)](https://travis-ci.org/jpnewman/ansible-role-elk-filebeat)

This Ansible role installs elastic [Filebeat](https://www.elastic.co/products/beats/filebeat)

## Requirements

Ansible 2.x

## Role Variables
|Variable|Description|Default|
|---|---|---|
|```libpcap_package```||'libpcap0.8'|
|```filebeat_version```||1.2.1|
|```filebeat_version_check```||1.2.1|
|```filebeat_platform```||amd64|
|```filebeat_elasticsearch_output```||false|
|```filebeat_elasticsearch_host```||'localhost:9200'|
|```filebeat_logstash_output```||true|
|```filebeat_logstash_host```||'localhost:5044'|
|```ssl_cert_local_directory```||files/certs|
|```ssl_cert_directory```||/etc/pki/tls/certs|
|```ssl_cert```||logstash-forwarder.crt|
|```certificate_authorities```||'["/etc/pki/tls/certs/logstash-forwarder.crt"]'|
|```apt_cache_valid_time```||600|
|```prospectors```|Contains a list of 'prospector' classes||

|'prospector' class variables|Description|
|---:|---|
|id|Id of prospector|
|paths|Contains a list of 'path' classes|
|type|prospector type|


|'path' class variables|Description|
|---:|---|
|log_paths|Contains a list of log file paths|

e.g.

~~~
prospectors:
  - id: syslog
    paths:
    - log_paths:
        - /var/log/syslog
        - /var/log/auth.log
      document_type: syslog
    type: syslog

  - id: varlog
    paths:
    - log_paths:
        - /var/log/*.log
      exclude_files:
        - "^syslog$"
        - "^auth.log$"
        - "^filebeat.log*$"
        - "^topbeat.log*$"
      document_type: log
~~~

## Dependencies

none

## Example Playbook

    - hosts: servers
      roles:
         - { role: jpnewman.elk-filebeat, tags: ["filebeat"] }

## Testing

For more information on testing the template review readme ```./tests/templates/README.md```

## License

MIT / BSD

## Author Information

John Paul Newman
