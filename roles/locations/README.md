# Ansible Role - radiorabe.foreman.locations

This role creates and manages locations in Foreman.

## Role Variables

This role supports the [FAM Common Role Variables](https://github.com/theforeman/foreman-ansible-modules/blob/develop/README.md#common-role-variables).

The main data structure for this role is the list of `foreman_locations`. Each `location` requires the following fields:

- `name`: The name of the location.

The following fields are optional in the sense that the server will use default values when they are omitted:

- `parent`: Title of a parent Location for nesting.
- `organizations`: List of organizations the location should be assigned to.
- `state`: The state of the location. Can be `present` or `absent`.

## Dependencies

The `radiorabe.foreman.locations` role depends on modules from the [`theforeman.foreman`](https://galaxy.ansible.com/theforeman/foreman) collection.

## Example Playbooks

```yaml
- name: add location to foreman
  hosts: localhost
  gather_facts: false
  roles:
    - role: radiorabe.foreman.locations
      vars: 
        foreman_server_url: https://foreman.example.com
        foreman_username: admin
        foreman_password: changeme
        foreman_locations:
          - name: Randweg
            origanizations:
              - RaBe
            state: present
```

## License

This role is free software: you can redistribute it and/or modify it under the terms of the GNU Affero General Public License as published by the Free Software Foundation, version 3 of the License.
