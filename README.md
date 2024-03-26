# Ansible role [go](https://galaxy.ansible.com/ui/standalone/roles/buluma/go/documentation)

Go (language) installation for Linux.

|GitHub|Version|Issues|Pull Requests|Downloads|
|------|-------|------|-------------|---------|
|[![github](https://github.com/buluma/ansible-role-go/actions/workflows/molecule.yml/badge.svg)](https://github.com/buluma/ansible-role-go/actions/workflows/molecule.yml)|[![Version](https://img.shields.io/github/release/buluma/ansible-role-go.svg)](https://github.com/buluma/ansible-role-go/releases/)|[![Issues](https://img.shields.io/github/issues/buluma/ansible-role-go.svg)](https://github.com/buluma/ansible-role-go/issues/)|[![PullRequests](https://img.shields.io/github/issues-pr-closed-raw/buluma/ansible-role-go.svg)](https://github.com/buluma/ansible-role-go/pulls/)|[![Ansible Role](https://img.shields.io/ansible/role/d/buluma/go)](https://galaxy.ansible.com/ui/standalone/roles/buluma/go/documentation)|

## [Example Playbook](#example-playbook)

This example is taken from [`molecule/default/converge.yml`](https://github.com/buluma/ansible-role-go/blob/master/molecule/default/converge.yml) and is tested on each push, pull request and release.

```yaml
---
- name: Converge
  hosts: all
  become: yes
  gather_facts: yes

  pre_tasks:
    - name: Update apt cache.
      ansible.builtin.apt: update_cache=yes cache_valid_time=600
      when: ansible_os_family == 'Debian'
      changed_when: false

  roles:
    - role: buluma.go

  tasks:
    - name: Verify that Go is installed and available in the $PATH.
      ansible.builtin.command: go version
      environment:
        PATH: /usr/local/go/bin:{{ ansible_env.PATH }}
      changed_when: false
```

The machine needs to be prepared. In CI this is done using [`molecule/default/prepare.yml`](https://github.com/buluma/ansible-role-go/blob/master/molecule/default/prepare.yml):

```yaml
---
- name: Prepare
  hosts: all
  become: yes
  gather_facts: no

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
go_version: "1.21.6"
go_platform: linux
go_arch: amd64
go_tarball: go{{ go_version }}.{{ go_platform }}-{{ go_arch }}.tar.gz
go_download_url: https://dl.google.com/go/{{ go_tarball }}
go_checksum: '3f934f40ac360b9c01f616a9aa1796d227d8b0328bf64cb045c7b8c4ee9caea4'
```

## [Requirements](#requirements)

- pip packages listed in [requirements.txt](https://github.com/buluma/ansible-role-go/blob/master/requirements.txt).

## [State of used roles](#state-of-used-roles)

The following roles are used to prepare a system. You can prepare your system in another way.

| Requirement | GitHub | Version |
|-------------|--------|--------|
|[buluma.bootstrap](https://galaxy.ansible.com/buluma/bootstrap)|[![Ansible Molecule](https://github.com/buluma/ansible-role-bootstrap/actions/workflows/molecule.yml/badge.svg)](https://github.com/buluma/ansible-role-bootstrap/actions/workflows/molecule.yml)|[![Version](https://img.shields.io/github/release/buluma/ansible-role-bootstrap.svg)](https://github.com/shadowwalker/ansible-role-bootstrap)|
|[buluma.core_dependencies](https://galaxy.ansible.com/buluma/core_dependencies)|[![Ansible Molecule](https://github.com/buluma/ansible-role-core_dependencies/actions/workflows/molecule.yml/badge.svg)](https://github.com/buluma/ansible-role-core_dependencies/actions/workflows/molecule.yml)|[![Version](https://img.shields.io/github/release/buluma/ansible-role-core_dependencies.svg)](https://github.com/shadowwalker/ansible-role-core_dependencies)|
|[buluma.buildtools](https://galaxy.ansible.com/buluma/buildtools)|[![Ansible Molecule](https://github.com/buluma/ansible-role-buildtools/actions/workflows/molecule.yml/badge.svg)](https://github.com/buluma/ansible-role-buildtools/actions/workflows/molecule.yml)|[![Version](https://img.shields.io/github/release/buluma/ansible-role-buildtools.svg)](https://github.com/shadowwalker/ansible-role-buildtools)|
|[buluma.ca_certificates](https://galaxy.ansible.com/buluma/ca_certificates)|[![Ansible Molecule](https://github.com/buluma/ansible-role-ca_certificates/actions/workflows/molecule.yml/badge.svg)](https://github.com/buluma/ansible-role-ca_certificates/actions/workflows/molecule.yml)|[![Version](https://img.shields.io/github/release/buluma/ansible-role-ca_certificates.svg)](https://github.com/shadowwalker/ansible-role-ca_certificates)|

## [Context](#context)

This role is a part of many compatible roles. Have a look at [the documentation of these roles](https://buluma.github.io/) for further information.

Here is an overview of related roles:

![dependencies](https://raw.githubusercontent.com/buluma/ansible-role-go/png/requirements.png "Dependencies")

## [Compatibility](#compatibility)

This role has been tested on these [container images](https://hub.docker.com/u/buluma):

|container|tags|
|---------|----|
|[Fedora](https://hub.docker.com/r/buluma/fedora)|all|
|[Amazon](https://hub.docker.com/r/buluma/amazonlinux)|2023, Candidate|
|[Debian](https://hub.docker.com/r/buluma/debian)|all|
|[Ubuntu](https://hub.docker.com/r/buluma/ubuntu)|all|

The minimum version of Ansible required is 2.12, tests have been done to:

- The previous version.
- The current version.
- The development version.

If you find issues, please register them in [GitHub](https://github.com/buluma/ansible-role-go/issues)

## [Changelog](#changelog)

[Role History](https://github.com/buluma/ansible-role-go/blob/master/CHANGELOG.md)

## [License](#license)

[Apache-2.0](https://github.com/buluma/ansible-role-go/blob/master/LICENSE)

## [Author Information](#author-information)

[Shadow Walker](https://buluma.github.io/)
