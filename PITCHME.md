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
@[9, zoom-12](Test scenario with implicitely defined name derived from directory, represents one test case with molecule.yml)
@[6,7, zoom-12](Using GitPitch live code presenting with optional annotations.)
@[8-9, zoom-12](This means no more switching between your slide deck and IDE on stage.)
@snapend

