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
@snap[south span-100 text-gray text-01]
@[1-5](You can step-and-ZOOM into fenced-code blocks, source files, and Github GIST.)
@[6,7, zoom-13](Using GitPitch live code presenting with optional annotations.)
@[8-9, zoom-12](This means no more switching between your slide deck and IDE on stage.)
@snapend

