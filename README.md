# ansible-docker-roles

Ansible roles that turn a fresh Linux host into a running three-tier
application: Docker, a PostgreSQL container, a Node.js API and a React front
end, each built and started from its own role.

## Roles

| Role | What it does |
| --- | --- |
| `docker` | Replaces the distribution's Docker packages with Docker CE, enables the service and adds the default user to the `docker` group |
| `postgre` | Builds and runs a PostgreSQL container, initialised from `init.sql` |
| `nodejs` | Builds and runs the Node.js API container against the database |
| `react` | Builds and runs the React front end container against the API |

## Stack

Ansible · Docker · PostgreSQL · Node.js · React · Linux

## Design decisions

**One role per tier.** Each container is its own role with its own variables,
so a tier can be rebuilt or moved to another host without touching the others.

**Images are built on the host.** Roles copy the build context and build
locally, so a run needs no external registry.

## Usage

```bash
ansible-playbook -i inventory play-role.yml
```

`play-role.yml` applies the roles in order on the target hosts. Set real
credentials in `nodejs/files/nodejs/.env` and `postgre/tasks/main.yml` before
running; the committed values are placeholders.
