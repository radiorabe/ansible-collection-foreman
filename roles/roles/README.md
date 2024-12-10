# Ansible Role - radiorabe.foreman.roles

This role creates and manages roles in Foreman.

## Role Variables

This role supports the [FAM Common Role Variables](https://github.com/theforeman/foreman-ansible-modules/blob/develop/README.md#common-role-variables).

The main data structure for this role is the list of `foreman_roles`. Each `role` requires the following fields:

- `name`: The name of the role.

The following fields are optional in the sense that the server will use default values when they are omitted:

- `description`: Description of the role.
- `filters`: Filters with permissions for this role.
- `state`: The state of the role. Can be `present` or `absent`.

## Dependencies

The `radiorabe.foreman.roles` role depends on modules from the [`theforeman.foreman`](https://galaxy.ansible.com/theforeman/foreman) collection.

## Example Playbooks

```yaml
- name: add role to foreman
  hosts: localhost
  gather_facts: false
  roles:
    - role: radiorabe.foreman.roles
      vars:
        foreman_server_url: https://foreman.example.com
        foreman_username: admin
        foreman_password: changeme
        foreman_roles:
          - name: Default role
            description: Role that is automatically assigned to every user in the system. Adding a permission grants it to everybody
            state: present
            filters:
              - permissions:
                  - view_foreman_tasks
                search: 'owner.id = current_user'
              - permissions:
                  - view_job_invocations
                search: 'user = current_user'
```

## License

This role is free software: you can redistribute it and/or modify it under the terms of the GNU Affero General Public License as published by the Free Software Foundation, version 3 of the License.
