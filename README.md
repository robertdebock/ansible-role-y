# [y](#y)

Process images

|Travis|GitHub|Quality|Downloads|Version|
|------|------|-------|---------|-------|
|[![travis](https://travis-ci.com/robertdebock/ansible-role-y.svg?branch=master)](https://travis-ci.com/robertdebock/ansible-role-y)|[![github](https://github.com/robertdebock/ansible-role-y/workflows/Ansible%20Molecule/badge.svg)](https://github.com/robertdebock/ansible-role-y/actions)|[![quality](https://img.shields.io/ansible/quality/)](https://galaxy.ansible.com/robertdebock/y)|[![downloads](https://img.shields.io/ansible/role/d/)](https://galaxy.ansible.com/robertdebock/y)|[![Version](https://img.shields.io/github/release/robertdebock/ansible-role-y.svg)](https://github.com/robertdebock/ansible-role-y/releases/)|

## [Example Playbook](#example-playbook)

This example is taken from `molecule/resources/converge.yml` and is tested on each push, pull request and release.
```yaml
---
- name: converge
  hosts: all
  become: yes
  gather_facts: yes

  roles:
    - role: robertdebock.y
      y_import_from: /data/in
      y_export_to: files/out
      y_presets:
        - name: monochrome
```

The machine may need to be prepared using `molecule/resources/prepare.yml`:
```yaml
---
- name: prepare
  hosts: all
  become: yes
  gather_facts: no

  roles:
    - role: robertdebock.bootstrap
    - role: robertdebock.epel

  tasks:
    - name: create directories in container
      file:
        path: "{{ item }}"
        state: directory
      with_items:
        - /data
        - /data/in
        - /data/out

    - name: copy samples files to /data/in
      copy:
        src: in/
        dest: /data/in
```

For verification `molecule/resources/verify.yml` run after the role has been applied.
```yaml
---
- name: Verify
  hosts: all
  become: yes
  gather_facts: yes

  tasks:
    - name: check if connection still works
      ping:
```

Also see a [full explanation and example](https://robertdebock.nl/how-to-use-these-roles.html) on how to use these roles.

## [Role Variables](#role-variables)

These variables are set in `defaults/main.yml`:
```yaml
---
# defaults file for y

# y_presets is a list of presets that will be applied to images.
# y_presets:
#   - name: monochrome

# y_import_from defines the path where to pickup files from.
# This could be /dev/sdb1 (for some SD-card) for example.
y_import_from: /tmp/import

# y_export_to is the path where the images will be saved.
y_export_to: /tmp/export
```

## [Requirements](#requirements)

- Access to a repository containing packages, likely on the internet.
- A recent version of Ansible. (Tests run on the current, previous and next release of Ansible.)

The following roles can be installed to ensure all requirements are met, using `ansible-galaxy install -r requirements.yml`:

```yaml
---
- robertdebock.bootstrap
- robertdebock.epel

```

## [Context](#context)

This role is a part of many compatible roles. Have a look at [the documentation of these roles](https://robertdebock.nl/) for further information.

Here is an overview of related roles:
![dependencies](https://raw.githubusercontent.com/robertdebock/drawings/artifacts/y.png "Dependency")

## [Compatibility](#compatibility)

This role has been tested on these [container images](https://hub.docker.com/u/robertdebock):

|container|tags|
|---------|----|
|alpine|all|
|amazon|2018.03|
|el|7, 8|
|debian|buster, bullseye|
|fedora|31, 32|
|opensuse|all|
|ubuntu|focal, bionic, xenial|

The minimum version of Ansible required is 2.8 but tests have been done to:

- The previous version, on version lower.
- The current version.
- The development version.



## [Testing](#testing)

[Unit tests](https://travis-ci.com/robertdebock/ansible-role-y) are done on every commit, pull request, release and periodically.

If you find issues, please register them in [GitHub](https://github.com/robertdebock/ansible-role-y/issues)

Testing is done using [Tox](https://tox.readthedocs.io/en/latest/) and [Molecule](https://github.com/ansible/molecule):

[Tox](https://tox.readthedocs.io/en/latest/) tests multiple ansible versions.
[Molecule](https://github.com/ansible/molecule) tests multiple distributions.

To test using the defaults (any installed ansible version, namespace: `robertdebock`, image: `fedora`, tag: `latest`):

```
molecule test

# Or select a specific image:
image=ubuntu molecule test
# Or select a specific image and a specific tag:
image="debian" tag="stable" tox
```

Or you can test multiple versions of Ansible, and select images:
Tox allows multiple versions of Ansible to be tested. To run the default (namespace: `robertdebock`, image: `fedora`, tag: `latest`) tests:

```
tox

# To run CentOS (namespace: `robertdebock`, tag: `latest`)
image="centos" tox
# Or customize more:
image="debian" tag="stable" tox
```

## [License](#license)

Apache-2.0


## [Author Information](#author-information)

[Robert de Bock](https://robertdebock.nl/)

Please consider [sponsoring me](https://github.com/sponsors/robertdebock).
