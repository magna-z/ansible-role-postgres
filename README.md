postgres
---

Configure and run vanila PostgreSQL from docker image as systemd.service.

### Links:
- <https://hub.docker.com/_/postgres/>


### Variables:
- **postgres_superuser_password** *(mandatory)* - Default `postgres` role password.

- **postgres_docker_image:** *(default=postgres:latest)* - Docker image for run as systemd.service.
- **postgres_docker_network:** *(default=bridge)* - Docker nerwork used as `--network=...`.
- **postgres_uid**, **postgres_uid** *(default=70)* - System user and group for run PostgreSQL and store data.

- **postgres_config:** *(default="see defaults/main.yml")* - Options for `postgresql.conf`.
- **postgres_config_hba:** *(default="see defaults/main.yml")* - Options for `pg_hba.conf`.
- **postgres_config_ident:** *(default="")* - Options for `pg_ident.conf`.

- **postgres_roles** *(default=[])* - Object list with roles in PostgreSQL. Delete object from list not delete role from PostgreSQL.  
  Object format: `{*username: "...", *password: "...", attributes: ["..."]}`. `*` - is required parameters.
- **postgres_databases** *(default=[])* - Object list with databases in PostgreSQL. Delete object from list not delete database from PostgreSQL.  
  Object format: `{*name: "...", owner: "...", encoding: "...", collate: "...", ctype: "..."}`. `*` - is required parameters.
