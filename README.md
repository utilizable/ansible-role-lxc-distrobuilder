LXC - DISTROBUILDER
============
Always wished for something like a Dockerfile but for LXC containers -  recently i discovered [distrobuilder](https://linuxcontainers.org/distrobuilder/docs/latest/) – it lets you whip up LXC containers effortlessly using a YAML config. I've wrapped it into Ansible playbook and GitHub Actions setup. 

## Table of Contents
- [Requirements](#-requirements)
- [Quick start](#%EF%B8%8F-quick-start)
- [Playbook Options](#-playbook-options)
- [Makefile stages](#-make-stages)
- [Repository structure](#-repository-structure)
- [Versioning model](#-versioning-model)

## 🧰 Requirements
<sup>[(Back to top)](#table-of-contents)</sup>

Make sure you have installed both - latest docker and gnu make!

  - `Docker` - https://docs.docker.com/desktop/install/
  - `Make` - https://ftp.gnu.org/gnu/make/

## ⚡️ Quick start
<sup>[(Back to top)](#table-of-contents)</sup>

  1. Clone repository
  2. execute `make prepare`

## 📔 Playbook Options
<sup>[(Back to top)](#table-of-contents)</sup>

#### Input Variables
```yml
#!/usr/bin/env ansible-playbook
#---
- name: playbook 
  hosts: localhost 

  roles:
    - role: distrobuilder 
      packages:
      - curl
      - vim-tiny
      actions:
      - | 
        #!/bin/sh
        # Install docker engine
        set -eux
        curl -fsSL https://get.docker.com | sh
...
```

## 📒 Make stages
<sup>[(Back to top)](#table-of-contents)</sup>

Stages definied in makefile.

- `make prepare` - Execute `ansible-playbook`,
- `make execute` - Execute `distrobuilder`,
- `make show` - Show running containers,
- `make prune` - Prune project related containers,

## 🗄 Repository structure
<sup>[(Back to top)](#table-of-contents)</sup>

- `./ansible` ansible related resources, workdir for compose-containers,
- `./build` each step contains its own docker container,
- `./Makefile` entrypoint,

## 🔖 Versioning model
<sup>[(Back to top)](#table-of-contents)</sup>

Versions have the format `<MAJOR>.<MINOR>(.<PATCH>)?` where:

- `<MAJOR>` Triggered manualy from default branch,
- `<MINOR>` Triggered automaticly after each push from default branch,
- `<PATCH>` Triggered automaticly after each push from fix/[0-9].[0-9].x branch.
