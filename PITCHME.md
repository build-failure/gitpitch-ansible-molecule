@title[Anisble Molecule]

![height=500px, width=500px, alt=Anisble Molecule](assets/img/molecule_logo.png)

---

@snap[north]
## Motivation
@snapend

- Readability
- Correctness
- Reliability
- Reusability
- Extendability
- Flexibility
- Efficiency

---

@snap[north]
## Benefits
@snapend

- Clear test workflow based on infrastructure configuration automation specifics
- Consistent well-written code, easy to understand and maintain
- Unified test infrastructure management will support for various providers
- Support for continuous integration	
- Short development iteration cycles
---
@title[Project Structure]

@snap[north]
## ./
@snapend

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
@[1-7,19-26, zoom-12](Standard Ansible role directory structure)
@[8-18, zoom-12](Molecule directory structure)
@[9, zoom-12](Test scenario with implicit defined name derived from the directory - represents one test case with at least molecule.yml)
@[11, zoom-12](Test scenario configuration including inventory configuration, infrastructure setup and lifecycle)
@[10, zoom-12](The Ansible playbook with the actual role to run applied to the designated hosts)
@[12, zoom-12](The Ansible playbook with preparation steps to establish a certain test situation)
@[13, zoom-12](The Ansible playbook with verification steps to validate the role execution effects)
@snapend

---
@title[Configuration Structure - Basics]

@snap[north]
## ./molecule/default/molecule.yml
@snapend

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
provisioner:
  name: ansible
  inventory:
    group_vars:
      all:
        foo: bar
  lint: |
    set -e
    ansible-lint
  playbooks:
    create: ../resources/playbooks/create.yml
    destroy: ../resources/playbooks/destroy.yml
    verify: verify.yml
verifier:
  name: ansible
  lint: |
    set -e
    ansible-lint
```

@snap[south span-100 text-gray text-08]
@[1-2, zoom-12](The test infrastructure provider - major cloud and local providers supported (Azure, DigitalOcean, AWS, GCP, Hetzner Cloud, Docker, Vagrant))
@[3-5, zoom-12](The linter configuration)
@[6-9, zoom-12](The test target platform hosts)
@[10-22, zoom-12](The provisioner configuration, including inventory and playbook definitions)
@[11, zoom-12](The provisioner - currently Ansible only)
@[12-15, zoom-12](Host and group inventory variables available within the global scope for all lifecycle playbooks)
@[16-18, zoom-12](The Linter configuration)
@[19-22, zoom-12](Test lifecycle playbooks)
@[23-27, zoom-12](The verifier configuration)
@snapend

---

@title[Configuration Structure - Lifecycle Management 1]

@snap[north]
## ./molecule/default/molecule.yml
@snapend

```yml
scenario:
  create_sequence:
    - dependency
    - create
    - prepare
  check_sequence:
    - dependency
    - cleanup
    - destroy
    - create
    - prepare
    - converge
    - check
    - destroy
  converge_sequence:
    - dependency
    - create
    - prepare
    - converge
  destroy_sequence:
    - dependency
    - cleanup
    - destroy
```

@snap[south span-100 text-gray text-08]
@[2-5, zoom-12](Create goal phase sequence)
@[6-14, zoom-12](Check goal phase sequence)
@[15-19, zoom-12](Converge goal phase sequence)
@[20-24, zoom-12](Destroy goal phase sequence)
@snapend

---

@title[Configuration Structure - Lifecycle Management 2]

@snap[north]
## ./molecule/default/molecule.yml
@snapend

```yml
scenario:
  test_sequence:
    - dependency
    - lint
    - cleanup
    - destroy
    - syntax
    - create
    - prepare
    - converge
    - idempotence
    - side_effect
    - verify
    - cleanup
    - destroy
```

@snap[south span-100 text-gray text-08]
@[2-15, zoom-12](Test goal phase sequence)
@snapend

---
@title[Development Lifecycle]

@snap[north]
## Development Lifecycle
@snapend

```console
molecule create -s default
molecule converge -s default
molecule verify -s default
molecule destroy -s default
```

---
@title[Continuous Integration]

@snap[north]
## Continuous Integration
@snapend

```console
molecule test
```

---
@title[Hands-On]

@snap[north]
## Hands-On
@snapend

[ansible-role-hello-world](https://github.com/build-failure/ansible-role-hello-world)
