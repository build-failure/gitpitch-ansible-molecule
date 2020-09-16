# Ansible Molecule

---

## Features

- Testing framework
- Project scaffolding
- Test infrastructure management

---

## Benefits

- Standardized testing infrastructure configuration
- Fast, iterative development loops
- All-in-one, batteries included validation for syntax, style, idempotence, correctness
- Trivially add CI for your Ansible, on any platform that lets you run a container

---

## Project Structure

```console
├── defaults
│   └── main.yml
├── handlers
│   └── main.yml
├── LICENSE.md
├── meta
│   └── main.yml
├── molecule
│   ├── default
│   │   ├── converge.yml
│   │   ├── molecule.yml
│   │   ├── prepare.yml
│   │   └── verify.yml
│   └── resources
│       └── playbooks
│           ├── create.yml
│           ├── destroy.yml
│           └── INSTALL.rst
├── README.md
├── tasks
│   └── main.yml
├── templates
│   └── hello_world.txt.j2
└── vars
    └── main.yml
```
@snap[south span-100 text-gray text-08]
@[9, zoom-12](Test scenario with implicit defined name derived from the directory - represents one test case with at least molecule.yml)
@[11, zoom-12](Encapsulates test scenario configuration including inventory configuration, infrastructure setup and life cycle)
@[10, zoom-12](Contains an Ansible playbook with the actual role to run applied to the designated hosts)
@[12, zoom-12](Contains an Ansible playbook with preparation steps to establish a certain test situation)
@[13, zoom-12](Contains an Ansible playbook with verification steps to validate the role execution effects)
@snapend

## molecule.yml Structure

```yml
driver:
  name: hetznercloud
lint: |
  set -e
  yamllint .
platforms:
  - name: ${MOLECULE_TEST_SCOPE:-default}-1
    server_type: cx11
    image: ${MOLECULE_PLATFORM-debian-10}
verifier:
  name: ansible
  lint: |
    set -e
    ansible-lint
```

## molecule.yml Structure

```yml
provisioner:
  name: ansible
  config_options:
    defaults:
      interpreter_python: auto_silent
  inventory:
    group_vars:
      all:
        test_hello_world_dir: /tmp/shared/hello-world
        test_hello_world_message: Hello World!
        hello_world_dir: "{{ test_hello_world_dir }}"
        hello_world_message: "{{ test_hello_world_message }}"
  lint: |
    set -e
    ansible-lint
  playbooks:
    create: ../resources/playbooks/create.yml
    destroy: ../resources/playbooks/destroy.yml
    verify: verify.yml
```
