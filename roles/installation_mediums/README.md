# Ansible Role - radiorabe.foreman.installation_mediums

This role creates and manages installation mediums in Foreman.

## Role Variables

This role supports the [FAM Common Role Variables](https://github.com/theforeman/foreman-ansible-modules/blob/develop/README.md#common-role-variables).

The main data structure for this role is the list of `foreman_installation_mediums`. Each `installation_medium` requires the following fields:

- `name`: The name of the `installation_medium`.

The following fields are optional in the sense that the server will use default values when they are omitted:

- `updated_name`: New full installation medium name. When this parameter is set, the module will not be idempotent.
- `os_family`: The OS family the template shall be assigned with. If no `os_family` is set but a operatingsystem, the value will be derived from it.
- `operatingsystems`: Dict of operatingsystems. See, `os_family` for options.
- `path`: Path or URL to the installation medium.

## Dependencies

The `radiorabe.foreman.installation_mediums` role depends on modules from the [`theforeman.foreman`](https://galaxy.ansible.com/theforeman/foreman) collection.

## Example Playbooks

```yaml
- name: add installation_medium to foreman
  hosts: localhost
  gather_facts: false
  roles:
    - role: radiorabe.foreman.installation_mediums
      vars:
        foreman_server_url: https://foreman.example.com
        foreman_username: admin
        foreman_password: changeme
        foreman_installation_mediums:
          - name: CentOS 7 mirror
            state: present
            os_family: Redhat
            path: http://mirror.centos.org/centos/$major/os/$arch
          - name: CentOS 8 mirror
            state: present
            os_family: Redhat
            path: http://mirror.centos.org/centos/$major/BaseOS/$arch/kickstart
          - name: CentOS Stream
            state: present
            os_family: Redhat
            path: http://mirror.centos.org/centos/$major-stream/BaseOS/$arch/os
          - name: CoreOS mirror
            state: present
            os_family: Coreos
            path: http://$release-temporary-archive.release.core-os.net
          - name: Debian mirror
            state: present
            os_family: Debian
            path: http://ftp.debian.org/debian
          - name: Fedora Atomic mirror
            state: present
            os_family: Redhat
            path: http://dl.fedoraproject.org/pub/alt/atomic/stable/Cloud_Atomic/$arch/os/
          - name: Fedora CoreOS mirror
            state: present
            os_family: Fcos
            path: https://builds.coreos.fedoraproject.org
          - name: Fedora mirror
            state: present
            os_family: Redhat
            path: http://dl.fedoraproject.org/pub/fedora/linux/releases/$major/Server/$arch/os/
          - name: Flatcar mirror
            state: present
            os_family: Coreos
            path: http://$release.release.flatcar-linux.net
          - name: FreeBSD mirror
            state: present
            os_family: Freebsd
            path: http://ftp.freebsd.org/pub/FreeBSD/releases/$arch/$version-RELEASE/
          - name: OpenSUSE mirror
            state: present
            os_family: Suse
            path: http://download.opensuse.org/distribution/leap/$version/repo/oss
          - name: RancherOS mirror
            state: present
            os_family: Rancheros
            path: https://github.com/rancher/os/releases/download/v$version
          - name: Red Hat CoreOS mirror
            state: present
            os_family: Rhcos
            path: http://mirror.openshift.com
          - name: Ubuntu mirror
            state: present
            os_family: Debian
            path: http://archive.ubuntu.com/ubuntu
```

## License

This role is free software: you can redistribute it and/or modify it under the terms of the GNU Affero General Public License as published by the Free Software Foundation, version 3 of the License.
