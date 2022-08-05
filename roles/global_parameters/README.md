# Ansible Role - radiorabe.foreman.global_parameters

This role creates and manages global parameters in Foreman.

## Role Variables

This role supports the [FAM Common Role Variables](https://github.com/theforeman/foreman-ansible-modules/blob/develop/README.md#common-role-variables).

The main data structure for this role is the list of `foreman_global_parameters`. Each `global_parameter` requires the following fields:

- `name`: The name of the `global_parameter`.

The following fields are optional in the sense that the server will use default values when they are omitted:

- `updated_name`: New full global parameter name. When this parameter is set, the module will not be idempotent.
- `value`: Value of the Global Parameter.
- `hidden_value`: Whether the value should be hidden in the GUI
- `parameter_type`: Type of value. Choices are string, boolean, integer, real, array, hash, yaml, or json. Default is string.

## Dependencies

The `radiorabe.foreman.global_parameters` role depends on modules from the [`theforeman.foreman`](https://galaxy.ansible.com/theforeman/foreman) collection.

## Example Playbooks

```yaml
- name: add global_parameters to foreman
  hosts: localhost
  gather_facts: false
  roles:
    - role: radiorabe.foreman.global_parameters
      vars:
        foreman_server_url: https://foreman.example.com
        foreman_username: admin
        foreman_password: changeme
        foreman_global_parameters:
          - name: foreman_organizations
            state: present
            parameter_type: yaml
            value: |
              - name: RaBe
                state: present
                description: Radio Bern RaBe
```

## License

This role is free software: you can redistribute it and/or modify it under the terms of the GNU Affero General Public License as published by the Free Software Foundation, version 3 of the License.
