Puppet
=========

Installs and configures hosts as either CA Masters or non-CA Masters.

Requirements
------------

None.

Role Variables
--------------

```yml
puppet_install: yes
puppet_version_install: 3
puppet_db_install: no

puppet_ca_masters:
  - puppetmaster:
      certname: "puppetmaster.localdomain"
      server: "puppetmaster.localdomain"
      alt_dns_names: "puppetmaster"

puppet_non_ca_masters:
  - creation:
      hostname: "creation.localdomain"
      alt_dns_names: "creation"
  - revenge:
      hostname: "revenge.localdomain"
      alt_dns_names: "revenge"

puppet_modules:
  - name: puppetlabs-firewall
    version: 1.9.0

puppet_autosign_certificates:
  - "blade"
  - "decapitron"
  - "pinhead"
  - "jester"
```
- **puppet_install**: Whether or not to install puppet.
- **puppet_version_install**: What version to install: 3, 4, or 5.
- **puppet_ca_masters**: A dictionary of CA masters to configure with each key being the name of the host in the inventory file.
  - **certname**: Host name of the server.
  - **server**: The server name.
  - **alt_dns_names**: Alternative names of the server.
- **puppet_non_ca_masters**: Follows the same structure as **puppet_ca_masters**.
- **puppet_modules**: A dictionary of puppet modules to install using `puppet module install {{ name }} --version={{ version }}`
- **puppet_autosign_certificates**: A list of a hosts that the master should sign the certificate for automatically.

Dependencies
------------

None.

Example Playbook
----------------

**Inventory File**
```
[puppetmasters]
puppetmaster
creation
revenge
```

**Playbook Example**
```
- name: Puppetmaster Playbook
  hosts: puppetmasters
  roles:
    - puppet
```

License
-------

BSD
