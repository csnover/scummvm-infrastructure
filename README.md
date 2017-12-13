# ScummVM Infrastructure

This infrastructure uses [Ansible](https://www.ansible.com/).

## Requirements

* Python 2.7+/3.5+
* A copy of Ansible 2.4+ (`pip install ansible`)
* A VM running Debian, for local testing changes to deployments

## Testing changes locally

1. Create a VM running Debian 8 (vm2) or 9 (vm1). **To prevent accidental
   production deployment, do *not* use the same password for this account that
   you use in production.**
2. Install your SSH key into the default account in the VM
3. Update `staging.yml` with the correct hosts for your dev environment
4. Run `ansible-playbook -i staging.yml site.yml`

## Provisioning a new server

1. Install your SSH key into the remote user account
2. Ensure the remote user account is in sudoers
3. Add the new server to an appropriate group in `production.yml`
4. If the server is part of a new group, add the roles for the new group to
   `site.yml`
5. Run `ansible-playbook -i production.yml -l new-host.example site.yml`
