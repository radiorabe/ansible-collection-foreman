# Ansible Role - radiorabe.foreman.realms

This role creates and manages realms in Foreman.

## Role Variables

This role supports the [FAM Common Role Variables](https://github.com/theforeman/foreman-ansible-modules/blob/develop/README.md#common-role-variables).

The main data structure for this role is the list of `foreman_realms`. Each `realm` requires the following fields:

- `name`: The name of the realm.
- `realm_proxy`: Proxy to use for this realm.
- `realm_type`: Realm type, one of "Red Hat Identity Management", "FreeIPA", or "Active Directory"

## Dependencies

The `radiorabe.foreman.realms` role depends on modules from the [`theforeman.foreman`](https://galaxy.ansible.com/theforeman/foreman) collection.

## Example Playbooks

```yaml
- name: add realm to foreman
  hosts: localhost
  gather_facts: false
  roles:
    - role: radiorabe.foreman.realms
      vars:
        foreman_server_url: https://foreman.example.com
        foreman_username: admin
        foreman_password: changeme
        foreman_realms:
          - name: INT.EXAMPLE.ORG
            state: present
            realm_proxy: foreman.int.example.org
            realm_type: FreeIPA
```

## License

This role is free software: you can redistribute it and/or modify it under the terms of the GNU Affero General Public License as published by the Free Software Foundation, version 3 of the License.
