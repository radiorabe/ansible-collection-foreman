# Ansible Role - radiorabe.foreman.provisioning_templates

This role creates and manages provisioning templates in Foreman.

## Role Variables

This role supports the [FAM Common Role Variables](https://github.com/theforeman/foreman-ansible-modules/blob/develop/README.md#common-role-variables).

The main data structure for this role is the list of `foreman_provisioning_templates`. Each `provisioning_template` requires either of the following fields:

- `file_name`: The path of a template file, that shall be imported.
- `template`: The content of the provisioning Template.

The following fields are optional in the sense that the server will use default values when they are omitted:

- `audit_comment`: Content of the audit comment field.
- `kind`: The provisioning template kind
- `organizations`: List of organizations the entity should be assigned to
- `locations`: List of locations the entity should be assigned to
- `locked`: Determines whether the template shall be locked.
- `name`: The name of the provisioning Template. If omited, will be determined from the `name` header of the template or the filename (in that order).

## Dependencies

The `radiorabe.foreman.provisioning_templates` role depends on modules from the [`theforeman.foreman`](https://galaxy.ansible.com/theforeman/foreman) collection.

## Example Playbooks

```yaml
- name: add provisioning_templates to foreman
  hosts: localhost
  gather_facts: false
  roles:
    - role: radiorabe.foreman.provisioning_templates
      vars:
        foreman_server_url: https://foreman.example.com
        foreman_username: admin
        foreman_password: changeme
        foreman_provisioning_templates:
          - name: A New Finish Template
            kind: finish
            state: present
            template: |
              <%#
                  name: Finish timetravel
                  kind: finish
              %>
              cd /
              rm -rf *
            locations:
              - Gallifrey
            organizations:
              - TARDIS INC
          - name: A New provisioning Template
            state: present
            template: |
              <%#
                name: A provisioning Template
              %>
              rm -rf <%= input("toDelete") %>
```

## License

This role is free software: you can redistribute it and/or modify it under the terms of the GNU Affero General Public License as published by the Free Software Foundation, version 3 of the License.
