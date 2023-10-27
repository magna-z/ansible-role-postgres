postgres
---

Configure and run vanila PostgreSQL as Docker container into systemd.service.


### Links
- <https://postgresql.org>
- <https://hub.docker.com/_/postgres/>


### Variables
- **`postgres_superuser_password`** *(type=string, mandatory)* - Password for default `postgres` role.

- **`postgres_docker_image`** *(type=string, default="postgres:latest")* - Docker image for run as systemd.service.

- **`postgres_docker_network`** *(type=string, default="bridge")* - Docker nerwork used as `docker run --network=...`.

- **`postgres_uid`** & **`postgres_gid`** *(type=number, default=70)* - System user and group for run PostgreSQL and store data.

- **`postgres_config`** *(type=string, default="see defaults/main.yml")* - Multiline string with options for `postgresql.conf`.
- **`postgres_config_hba`** *(type=string, default="see defaults/main.yml")* - Multiline string with options for `pg_hba.conf`.
- **`postgres_config_ident`** *(type=string, default="")* - Multiline string with options for `pg_ident.conf`.

- **`postgres_roles`** *(type=list, default=[])* - Object list with roles in PostgreSQL. Delete object from list not delete role from PostgreSQL.  
  Object struct: `{*username: "", *password: "", attributes: [""], state: "present|absent"}` (`*` - require).

- **`postgres_databases`** *(type=list, default=[])* - Object list with databases in PostgreSQL. Delete object from list not delete database from PostgreSQL.  
  Object struct: `{*name: "", owner: "", encoding: "", collate: "", ctype: "", template: "", schemas: [{name: "", owner: ""}], extensions: [{name: ""}], state: "present|absent"}` (`*` - require).


### Examples
```yaml
# postgres
postgres_docker_image: postgres:15.4-alpine3.18
postgres_docker_network: host
postgres_superuser_password: !vault |
  $ANSIBLE_VAULT;1.1;AES256
  ...
postgres_roles:
  - username: example
    password: !vault |
      $ANSIBLE_VAULT;1.1;AES256
      ...
postgres_databases:
  - name: example
    owner: example
postgres_config: |
  max_connections = '100'
  shared_buffers = '128MB'
  dynamic_shared_memory_type = 'posix'
  max_wal_size = '1GB'
  min_wal_size = '80MB'
  log_timezone = 'UTC'
  datestyle = 'iso, mdy'
  timezone = 'UTC'
  lc_messages = 'en_US.utf8'
  lc_monetary = 'en_US.utf8'
  lc_numeric = 'en_US.utf8'
  lc_time = 'en_US.utf8'
  default_text_search_config = 'pg_catalog.english'
  autovacuum_max_workers = '1'
  autovacuum_vacuum_scale_factor = '0.1'
  autovacuum_vacuum_threshold = '100'
  shared_preload_libraries = 'pg_stat_statements'
  pg_stat_statements.track = 'all'
postgres_config_hba: |
  # localhost
  local all all trust
  host all all 127.0.0.1/32 trust
  host all all ::1/128 trust
  # other
  host all all all scram-sha-256
```
