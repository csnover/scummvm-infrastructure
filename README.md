# ScummVM Infrastructure

This infrastructure uses [Ansible](https://www.ansible.com/) ([docs](http://docs.ansible.com/ansible/latest/index.html)).

## Requirements

* Python 2.7+/3.5+
* A copy of Ansible 2.4+ (`pip install ansible`)
* Vagrant 2+ and VirtualBox 5.1+, for local testing changes to deployments

## Testing changes locally

1. Run `vagrant up` to create a control virtual machine (ansible) and two deployment targets (vm1 and vm2)
2. Run `vagrant ssh ansible` to connect to the control virtual machine
3. Run `cd /vagrant && ansible-playbook -b --ask-vault-pass -i staging.yml site.yml`

## Provisioning a new server

1. Install your SSH key into the remote user account
2. Ensure the remote user account is in sudoers
3. Add the new server to an appropriate group in `production.yml`
4. If the server is part of a new group, add the roles for the new group to
   `site.yml`
5. Run `ansible-playbook -i production.yml -l new-host.example site.yml`
