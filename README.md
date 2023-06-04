postgres
---

Configure and run vanila PostgreSQL as Docker container into systemd.service.


### Links:
- <https://hub.docker.com/_/postgres/>


### Variables:
- **`postgres_superuser_password`** *(type=string, mandatory)* - Default `postgres` role password.

- **`postgres_docker_image`** *(type=string, default="postgres:latest")* - Docker image for run as systemd.service.
- **`postgres_docker_network`** *(type=string, default="bridge")* - Docker nerwork used as `--network=...`.
- **`postgres_uid`** & **`postgres_uid`** *(type=number, default=70)* - System user and group for run PostgreSQL and store data.

- **`postgres_config`** *(type=string, default="see defaults/main.yml")* - Options for `postgresql.conf`.
- **`postgres_config_hba`** *(type=string, default="see defaults/main.yml")* - Options for `pg_hba.conf`.
- **`postgres_config_ident`** *(type=string, default="")* - Options for `pg_ident.conf`.

- **`postgres_roles`** *(type=list, default=[])* - Object list with roles in PostgreSQL. Delete object from list not delete role from PostgreSQL.  
  Object struct: `{*username: "...", *password: "...", attributes: ["..."], state: "present|absent"}`. `*` - is required parameters.
- **`postgres_databases`** *(type=list, default=[])* - Object list with databases in PostgreSQL. Delete object from list not delete database from PostgreSQL.  
  Object struct: `{*name: "...", owner: "...", encoding: "...", collate: "...", ctype: "...", template: "...", schemas: [{name: "...", owner: "..."}], extensions: [{name: "..."}], state: "present|absent"}`. `*` - is required parameters.
