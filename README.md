# docker_service_configs

Prepares configs for the docker_swarm_service module.

The docker config name will contain the prefix and version suffix, ex.
'foo_v1'. The configuration version is automatically incremented by 1.

## Input vars

- service_name - The service name.
- service_configs
  - prefix - The config prefix.
  - content - The expected content of the config.
  - filename - Name of the file containing the config.

## Output vars

- docker_service_configs

## Examples

``` yml
- hosts: all
  tasks:
    - name: create foo configs
      include_role:
        name: docker_service_configs
      vars:
        service_name: foo
        service_configs:
          - prefix: foo_config
            content: "{{ lookup('template', template.j2 ) }}"
            filename: /etc/foo.conf

    - name: run foo service
      docker_swarm_service:
        name: foo
        configs: "{{ docker_service_configs }}"
```
