# Ansible Role - radiorabe.foreman.job_templates

This role creates and manages job templates in Foreman.

## Role Variables

This role supports the [FAM Common Role Variables](https://github.com/theforeman/foreman-ansible-modules/blob/develop/README.md#common-role-variables).

The main data structure for this role is the list of `foreman_job_templates`. Each `job_template` requires either of the following fields:

- `file_name`: The path of a template file, that shall be imported.
- `template`: The content of the Job Template.

The following fields are optional in the sense that the server will use default values when they are omitted:

- `audit_comment`: Content of the audit comment field.
- `description_format`: Description of the job template. Template inputs can be referenced.
- `job_category`: The category the template should be assigend to.
- `locked`: Determines whether the template shall be locked.
- `name`: The name of the Job Template. If omited, will be determined from the `name` header of the template or the filename (in that order).
- `provider_type`: Determines via which provider the template shall be executed.
- `snippet`: Determines whether the template shall be a snippet.
- `template_inputs`: A dict of template inputs used in the Job Template.

## Dependencies

The `radiorabe.foreman.job_templates` role depends on modules from the [`theforeman.foreman`](https://galaxy.ansible.com/theforeman/foreman) collection.

## Example Playbooks

```yaml
- name: add job_templates to foreman
  hosts: localhost
  gather_facts: false
  roles:
    - role: radiorabe.foreman.job_templates
      vars:
        foreman_server_url: https://foreman.example.com
        foreman_username: admin
        foreman_password: changeme
        foreman_job_templates:
          - name: A New Job Template
            state: present
            template: |
              <%#
                name: A Job Template
              %>
              rm -rf <%= input("toDelete") %>
            template_inputs:
              - name: toDelete
            input_type: user
```

## License

This role is free software: you can redistribute it and/or modify it under the terms of the GNU Affero General Public License as published by the Free Software Foundation, version 3 of the License.
