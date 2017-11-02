Puppet
=========

Installs and configures hosts as either CA Masters or non-CA Masters.

Requirements
------------

None.

Role Variables
--------------

```yml
puppet_version_install: 3

puppet_ca_master:
  certname: "puppetmaster.localdomain"
  server: "puppetmaster.localdomain"
  alt_dns_names: "puppetmaster"

puppet_non_ca_masters:
  - hostname: "creation.localdomain"
    alt_dns_names: "creation"
  - hostname: "revenge.localdomain"
    alt_dns_names: "revenge"

puppet_modules:
  - name: puppetlabs-firewall
    version: 1.9.0

puppet_autosign_certificates:
  - "blade.localdomain"
  - "decapitron.localdomain"
  - "pinhead.localdomain"
  - "jester.localdomain"
```
- **puppet_version_install**: What version to install: 3, 4, or 5.
- **puppet_ca_master**: Contains configuration information pertaining to the CA master.
  - **certname**: Host name of the server.
  - **server**: The server name.
  - **alt_dns_names**: Alternative names of the server.
- **puppet_non_ca_masters**: A list containing the hostname and alternative DNS names for non-CA puppet servers.
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
