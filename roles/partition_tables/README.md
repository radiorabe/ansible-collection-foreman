# Ansible Role - radiorabe.foreman.partition_tables

This role creates and manages partition tables in Foreman.

## Role Variables

This role supports the [FAM Common Role Variables](https://github.com/theforeman/foreman-ansible-modules/blob/develop/README.md#common-role-variables).

The main data structure for this role is the list of `foreman_partition_tables`. Each `partition_table` requires the following fields:

- `name`: The name of the `partition_table`.

The following fields are optional in the sense that the server will use default values when they are omitted:

- `updated_name`: New partition table name. When this parameter is set, the module will not be idempotent.
- `os_family`: The OS family the partition table shall be assigned with.
- `layout`: The partition table content. Mutually exclusive with `file_name`.
- `file_name`: Path to a file on the controller containing the partition table content. Mutually exclusive with `layout`.
- `locked`: Whether the partition table is locked for editing.
- `locations`: List of locations the partition table should be assigned to.
- `organizations`: List of organizations the partition table should be assigned to.
- `state`: `present`, `present_with_defaults` or `absent`. Defaults to `present`.

## Dependencies

The `radiorabe.foreman.partition_tables` role depends on modules from the [`theforeman.foreman`](https://galaxy.ansible.com/theforeman/foreman) collection.

## Example Playbooks

```yaml
- name: add partition_table to foreman
  hosts: localhost
  gather_facts: false
  roles:
    - role: radiorabe.foreman.partition_tables
      vars:
        foreman_server_url: https://foreman.example.com
        foreman_username: admin
        foreman_password: changeme
        foreman_partition_tables:
          - name: Example Kickstart Layout
            os_family: Redhat
            locked: true
            layout: |
              clearpart --all --initlabel --disklabel=gpt
              zerombr
              part /boot/efi --fstype=fat32 --size=600
              part /boot --fstype=xfs --size=1000
              part swap --size=4000
              part / --fstype=xfs --size=14400 --grow
            locations:
              - Example Location
            organizations:
              - Example Organization
```

## License

This role is free software: you can redistribute it and/or modify it under the terms of the GNU Affero General Public License as published by the Free Software Foundation, version 3 of the License.
