# LEMP setup

This set of roles will install:
- PHP 7.2
- nginx (latest) with SSL and HTTP2 support
- MySQL (latest in the Ubuntu 16.04 APT repositories)
- Letsencrypt (latest)

Tested with: Ansible 2.5

## Support
This setup has been tested on Ubuntu 16.04.

## Inventory file
Filename: `hosts`

Required variables:
- `hostname`, hostname of the server which is set as the hostname and is used by nginx and Letsencrypt

## MySQL root password
You can define the MySQL root password in the inventory file, but that's not desirable, since the password will then be
stored unencrypted on your computer.
Better is to store the password encrypted in the `roles/mysql/vault/credentials.yml` file.

Create the file and make up a new password:
```
---
mysql_root_password: YourPasswordHere
```

Run: `ansible-vault encrypt roles/mysql/vault/credentials.yml --ask-vault-pass` and enter your (new) encryption key

## How to run it
- Create hosts file in the root directory
- `ansible-playbook -i hosts main.yml --ask-vault-pass`

## Todo
- Add support for Apache
- Create non-root user
- Make nginx setup idempotent
- Setup ufw
- Make goaccess setup idempotent
- Separate role concerns better
- Find a proper way to secure the goaccess websocket
