# Ansible Role - radiorabe.foreman.hosts

This role creates and manages hosts in Foreman.

## Role Variables

This role supports the [FAM Common Role Variables](https://github.com/theforeman/foreman-ansible-modules/blob/develop/README.md#common-role-variables).

The main data structure for this role is the list of `foreman_hosts`. Each `host` requires the following fields:

- `name`: The name of the host

The following fields are optional in the sense that the server will use default values when they are omitted:

- `hostgroup`: Title of related hostgroup
- `location`: Name of related location
- `organization`: Name of related organization
- `build`: Whether or not to setup build context for the host
- `enabled`: Include this host within reporting
- `managed`: Whether a host is managed or unmanaged
- `ip`: IP address of the primary interface of the host
- `mac`: MAC address of the primary interface of the host
- `comment`: Comment about the host
- `owner`: Owner (user) of the host
- `owner_group`: Owner (user group) of the host
- `provision_method`: The method used to provision the host
- `image`: The image to use when provision_method=image
- `compute_attributes`: Additional compute resource specific attributes
- `interfaces_attributes`: Additional interfaces specific attributes

## Dependencies

The `radiorabe.foreman.hosts` role depends on modules from the [`theforeman.foreman`](https://galaxy.ansible.com/theforeman/foreman) collection.

## Example Playbooks

```yaml
- name: add host to foreman
  hosts: localhost
  gather_facts: false
  roles:
    - role: radiorabe.foreman.hosts
      vars: 
        foreman_server_url: https://foreman.example.com
        foreman_username: admin
        foreman_password: changeme
        foreman_hosts:
          - name: vm-0000.int.example.org
            organization: RaBe
```

## License

This role is free software: you can redistribute it and/or modify it under the terms of the GNU Affero General Public License as published by the Free Software Foundation, version 3 of the License.
