# ScummVM Infrastructure

This infrastructure uses [Ansible](https://www.ansible.com/).

## Requirements

* Python 2.7+/3.5+
* A copy of Ansible 2.4+ (`pip install ansible`)
* A VM running Debian, for local testing changes to deployments

## Provisioning a new server

1. Install your SSH key for bootstrapping Ansible in the remote account
2. Ensure the remote user account is in sudoers
3. Add the new server to an appropriate group in `production.yml`
4. If the server is part of a new group, add the roles for the new group to
   `site.yml`
5. Run `ansible-playbook -i production.yml -l new-host.example site.yml`
