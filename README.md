# [Ansible role go](#ansible-role-go)

Go (language) installation for Linux.

|GitHub|Issues|Pull Requests|Version|Downloads|
|------|------|-------------|-------|---------|
|[![github](https://github.com/buluma/ansible-role-go/actions/workflows/molecule.yml/badge.svg)](https://github.com/buluma/ansible-role-go/actions/workflows/molecule.yml)|[![Issues](https://img.shields.io/github/issues/buluma/ansible-role-go.svg)](https://github.com/buluma/ansible-role-go/issues/)|[![PullRequests](https://img.shields.io/github/issues-pr-closed-raw/buluma/ansible-role-go.svg)](https://github.com/buluma/ansible-role-go/pulls/)|[![Version](https://img.shields.io/github/release/buluma/ansible-role-go.svg)](https://github.com/buluma/ansible-role-go/releases/)|[![Ansible Role](https://img.shields.io/ansible/role/d/buluma/go)](https://galaxy.ansible.com/ui/standalone/roles/buluma/go/documentation)|

## [Example Playbook](#example-playbook)

This example is taken from [`molecule/default/converge.yml`](https://github.com/buluma/ansible-role-go/blob/master/molecule/default/converge.yml) and is tested on each push, pull request and release.

```yaml
---
- name: Converge
  become: true
  gather_facts: true
  hosts: all
  pre_tasks:
    - name: Update apt cache.
      ansible.builtin.apt:
        update_cache: "true"
        cache_valid_time: "600"
      changed_when: false
      when: ansible_os_family == 'Debian'
  roles:
    - role: buluma.go
  tasks:
    - name: Verify that Go is installed and available in the $PATH.
      ansible.builtin.command: go version
      changed_when: false
      environment:
        PATH: /usr/local/go/bin:{{ ansible_env.PATH }}
```

The machine needs to be prepared. In CI this is done using [`molecule/default/prepare.yml`](https://github.com/buluma/ansible-role-go/blob/master/molecule/default/prepare.yml):

```yaml
---
- name: Prepare
  become: true
  gather_facts: false
  hosts: all
  roles:
    - role: buluma.bootstrap
    - role: buluma.core_dependencies
    - role: buluma.buildtools
    - role: buluma.ca_certificates
```

Also see a [full explanation and example](https://buluma.github.io/how-to-use-these-roles.html) on how to use these roles.

## [Role Variables](#role-variables)

The default values for the variables are set in [`defaults/main.yml`](https://github.com/buluma/ansible-role-go/blob/master/defaults/main.yml):

```yaml
---
go_arch: amd64
go_checksum: 3f934f40ac360b9c01f616a9aa1796d227d8b0328bf64cb045c7b8c4ee9caea4
go_download_url: https://dl.google.com/go/{{ go_tarball }}
go_platform: linux
go_tarball: go{{ go_version }}.{{ go_platform }}-{{ go_arch }}.tar.gz
go_version: 1.21.6
```

## [Requirements](#requirements)

- pip packages listed in [requirements.txt](https://github.com/buluma/ansible-role-go/blob/master/requirements.txt).

## [State of used roles](#state-of-used-roles)

The following roles are used to prepare a system. You can prepare your system in another way.

| Requirement | GitHub |
|-------------|--------|
|[buluma.bootstrap](https://galaxy.ansible.com/buluma/bootstrap)|[![Build Status GitHub](https://github.com/buluma/ansible-role-bootstrap/workflows/Ansible%20Molecule/badge.svg)](https://github.com/buluma/ansible-role-bootstrap/actions)|
|[buluma.core_dependencies](https://galaxy.ansible.com/buluma/core_dependencies)|[![Build Status GitHub](https://github.com/buluma/ansible-role-core_dependencies/workflows/Ansible%20Molecule/badge.svg)](https://github.com/buluma/ansible-role-core_dependencies/actions)|
|[buluma.buildtools](https://galaxy.ansible.com/buluma/buildtools)|[![Build Status GitHub](https://github.com/buluma/ansible-role-buildtools/workflows/Ansible%20Molecule/badge.svg)](https://github.com/buluma/ansible-role-buildtools/actions)|
|[buluma.ca_certificates](https://galaxy.ansible.com/buluma/ca_certificates)|[![Build Status GitHub](https://github.com/buluma/ansible-role-ca_certificates/workflows/Ansible%20Molecule/badge.svg)](https://github.com/buluma/ansible-role-ca_certificates/actions)|

## [Context](#context)

This role is part of many compatible roles. Have a look at [the documentation of these roles](https://buluma.github.io/) for further information.

Here is an overview of related roles:

![dependencies](https://raw.githubusercontent.com/buluma/ansible-role-go/png/requirements.png "Dependencies")

## [Compatibility](#compatibility)

This role has been tested on these [container images](https://hub.docker.com/u/robertdebock):

|container|tags|
|---------|----|
|[Fedora](https://hub.docker.com/r/robertdebock/fedora)|all|
|[Amazon](https://hub.docker.com/r/robertdebock/amazonlinux)|all|
|[Debian](https://hub.docker.com/r/robertdebock/debian)|all|
|[Ubuntu](https://hub.docker.com/r/robertdebock/ubuntu)|all|

The minimum version of Ansible required is 2.12, tests have been done on:

- The previous version.
- The current version.
- The development version.

If you find issues, please register them on [GitHub](https://github.com/buluma/ansible-role-go/issues).

## [License](#license)

[Apache-2.0](https://github.com/buluma/ansible-role-go/blob/master/LICENSE).

## [Author Information](#author-information)

[buluma](https://buluma.github.io/)

