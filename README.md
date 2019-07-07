# Ansible Role: Postfix

Installs postfix

## Requirements


## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):

    postfix_config_file: /etc/postfix/main.cf

The path to the Postfix `main.cf` configuration file.

    postfix_service_state: started
    postfix_service_enabled: true

The state in which the Postfix service should be after this role runs, and whether to enable the service on startup.

    configuration_items:
        - name: inet_interfaces
          value: localhost
        - ...
    
Options for values in the `main.cf` file. This can be any configuration item from `POSTCONF(5)`.

## Dependencies

None.

## Example Playbook
This playbook shows an example of an SMTP relay

    - hosts: all
      roles:
        - role: postfix
          vars:
            configuration_items:
              - name: inet_interfaces
                value: localhost
              - name: inet_protocols
                value: all
              - name: relayhost
                value: '[mail.com]:587'
              - name: smtp_sasl_auth_enable
                value: 'yes'
              - name: smtp_sasl_security_options
                value: noanonymous
              - name: smtp_sasl_password_maps
                value: static:username@mail.com:password
              - name: smtp_use_tls
                value: 'yes'
              - name: smtp_generic_maps
                value: static:username@mail.com

## License

MIT / BSD
