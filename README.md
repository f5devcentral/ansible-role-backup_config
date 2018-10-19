# Ansible Role: Backup Config

Role to collect the current device configurations and store it on the Ansible controller
with a user specific backup filename and path.

## Requirements

None.

## Role Variables

Available variables are listed below. For their default values, see `defaults/main.yml`:

    provider_server: localhost
    provider_server_port: 443
    provider_user: admin
    provider_password: secret
    provider_validate_certs: no
    provider_transport: rest
    provider_timeout: 120

Establishes initial connection to your BIG-IQ. These values are substituted into
your ``provider`` module parameter.

    filename

Specifies the filename to store configurations. Since this role backs up multiple files, the
multiple files created will be named the value specified here, however the extensions will
differ for the backed up files. For example, if ``filename`` is "backup", this role will
create ``backup.qkview`` and ``backup.ucs``.

    path

Absolute or relative path of folder where config will be stored.

    backup

Boolean flag to indicate if we need to backup configurations before overwriting it with new
configurations.

## Dependencies

None.

## Example Playbook

    - name: Backup config
      hosts: bigip
      vars:
        backup_config:
          filename: "config_{{ ansible_host }}"
          path: "~/network_configs_1/"
          backup: yes
      roles:
        - { role: f5devcentral.backup_config }

## License

Apache

## Author Information

This role was created in 2018 by [Tim Rupp](https://github.com/caphrim007), with the help of
[Forrest Crenshaw](https://github.com/focrensh).
