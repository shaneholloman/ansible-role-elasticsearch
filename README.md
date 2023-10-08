# Ansible Role: Elasticsearch

[![CI](https://github.com/shaneholloman-org/ansible-role-elasticsearch/actions/workflows/ci.yml/badge.svg)](https://github.com/shaneholloman-org/ansible-role-elasticsearch/actions/workflows/ci.yml)

An Ansible Role that installs Elasticsearch on RedHat/CentOS or Debian/Ubuntu.

## Requirements

Requires at least Java 8. You can use the [`shaneholloman.java`](https://github.com/shaneholloman/ansible-role-java) to easilly install Java.

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml` for default role variables, `vars/RedHat.yml` and  `vars/Debian.yml` for distribution specific variables):

    elasticsearch_version: '7.x'

The major version to use when installing Elasticsearch.

    elasticsearch_package: elasticsearch

If you want to follow the latest release in the `elasticsearch_version` major release cycle, keep the default here. Otherwise you can add `-7.13.2` (for RHEL-based systems) or `=7.13.2` (for Debian-based systems) to lock in a specific version, e.g. `7.13.2`.

    elasticsearch_package_state: present

The `elasticsearch` package state; set to `latest` to upgrade or change versions.

    elasticsearch_service_state: started
    elasticsearch_service_enabled: true

Controls the Elasticsearch service options.

    elasticsearch_network_host: localhost

Network host to listen for incoming connections on. By default we only listen on the localhost interface. Change this to the IP address to listen on a specific interface, or `"0.0.0.0"` to listen on all interfaces.

When listening on multiple interfaces, if you're setting up a single Elasticsearch server (not a cluster), you should also add `discovery.type: single-node` to `elasticsearch_extra_options`.

    elasticsearch_http_port: 9200

The port to listen for HTTP connections on.

    elasticsearch_heap_size_min: 1g

The minimum jvm heap size.

    elasticsearch_heap_size_max: 2g

The maximum jvm heap size.

    elasticsearch_extra_options: ''

A placeholder for arbitrary configuration options not exposed by the role. This will be appended as-is to the end of the `elasticsearch.yml` file, as long as your variable preserves formatting with a `|`. For example:

```yaml
elasticsearch_extra_options: |  # Dont forget the pipe!
  some.option: true
  another.option: false
```

## Dependencies

None.

## Example Playbook

    - hosts: search
      roles:
        - shaneholloman.java
        - shaneholloman.elasticsearch

## License

MIT / BSD

## Author Information

This role was created in 2023
