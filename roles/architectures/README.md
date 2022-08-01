# Ansible Role - radiorabe.foreman.architectures

This role creates and manages architectures in Foreman.

## Role Variables

This role supports the [FAM Common Role Variables](https://github.com/theforeman/foreman-ansible-modules/blob/develop/README.md#common-role-variables).

The main data structure for this role is the list of `foreman_architectures`. Each `architecture` requires the following fields:

- `name`: The name of the architecture.

The following fields are optional in the sense that the server will use default values when they are omitted:

- `operatingsystems`: List of operatingsystems the architecture should be assigned to.
- `state`: The state of the architecture. Can be `present` or `absent`.

## Dependencies

The `radiorabe.foreman.architectures` role depends on modules from the [`theforeman.foreman`](https://galaxy.ansible.com/theforeman/foreman) collection.

## Example Playbooks

```yaml
- name: add architecture to foreman
  hosts: localhost
  gather_facts: false
  roles:
    - role: radiorabe.foreman.architectures
      vars:
        foreman_server_url: https://foreman.example.com
        foreman_username: admin
        foreman_password: changeme
        foreman_architectures:
          - name: i386
            state: absent
          - name: x86_64
            operatingsystems:
              - CentOS Stream 8
```

## License

This role is free software: you can redistribute it and/or modify it under the terms of the GNU Affero General Public License as published by the Free Software Foundation, version 3 of the License.
